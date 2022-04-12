# Blockhash Pipeline

This is a centrally managed system that uses the same
[threat-indicators](./visual-threat-indicator.md) as
the [interlock-extension](./interlock-extension.md) to crawl
and classify web-pages. Instead of using [TOFU](./trust-on-first-use.md)
it uses a harmonic centrality measure computed by the common-crawl
project since its last crawl over the web.

## Operation and Architecture

The pipeline was designed with managed message-queue services like
SQS and PubSub in mind. However, it also has a Postgres backend to
make testing, debugging, and inspection easier. It also performs
much better than the (current) SQS code, because SQS transmits the
same message multiple times (and we batch+compress objects into
each message), causing the throughput to drop by the duplication-factor
(i.e. by half or more). This might be the result of misuse of SQS.

Either way, there are 4 phases: domains, icons, hashes, etl. The
domains phase simply takes an unprocesses domain or URL, and passes
it along to icons phase. The icons phase takes each domain/URL, and
asks `besticon` for a list of all detectable favicon-urls. The hashes
phase takes the favicon-urls, fetches the actual favicons, computes
4 blockhashes, and passes that along. Finally the ETL phase, takes the
blockhash-records, and writes them into the DB.

When operating in Postgres-mode, the ETL phase does nothing, because each
previous phase acts directly on the data-base, and uses set-intersection
and set-difference to get the next batch of records to process (implemented
as LEFT-JOINS in SQL).

Each phase has 1 input queue, and 2 output queues: one of the output-queues
contains results, while the other contains errors.

```
        +---<---<---<--+
	|              |
 +------+--------+     |
 | +----++-----+ |     ^
 | | OUT | ERR | |     |
 | |     |     | |     |
 | +-----+-----+ |     ^
 +-------|-------+     |
         |             |
         +-<---<---<---+
      +--+--+          |
      |     |          |
      |     |          |
 +----v-----v----+     ^
 | +--+--+--+--+ |     |
 | | OUT | ERR | |     |
 | |     |     +-+-->--+
 | +-----+-----+ |     |
 +-------|-------+     |
         |             |
         +-<---<---<---+
      +--+--+          |
      |     |          |
      |     |          |
 +----v-----v----+     ^
 | +-----+-----+ |     |
 | | OUT | ERR | |     |
 | |     |     +-+-->--+
 | +-----+-----+ |
 +---------------+
```








## Typescript Code

The typescript code is a bit strange. There is not "beginning" and "end",
unlike your typical program. Because it is meant to run all the time,
crawling and re-crawling the internet, it written in an event-oriented style.

So, when a phase starts up, it calls `pullAll`, which emits a `pull` event,
which in turn pulls a batch from the input-queue, and start processing it.
Once it finishes processing, it emits another `pull` event, and does this in
a loop. If it experience an error when pulling, or receives an empty-batch,
the phase will sleep for a few minutes, so as not to saturate the connection
with needless requests.

Each `pullAll` invocation takes the callback: `is_success`, `on_success`,
`on_error`, and `on_empty`. Each phase, thus, has its own way of detecting
and reacing to successes and errors.

When running in Postgres mode, each phase checks the queue-id to determine
which how to query the database, in order to emulate a queue-pull/push.
All of the postgres-related functions begin with: `pgInsert`, `pgFind`,
and `pg_`.

## Data Layout

Here are only the tables that are relevant to the pipeline (so not including any of
the web3 tables).

  * domains
  * target_urls
  * besticon_url
  * besticon_err
  * favicon_metadata
  * hashing_err

The domains-table contains all of the domains from Common Crawl. They have
various ranking data (i.e. page-rank, harmonic-centrality), and the domains
themselves are stored in reverse order (i.e. network.interlock instead of
interlock.network).

Here is the schema for this table:

XXX-TODO

The target_urls-table contains only a single column of URL strings. They
are derived from the domains-table (by one of the pipeline phases), and
can also be added by other means (i.e. from the interlock extension).

Here is the schema for this table:

XXX-TODO

The besticon_url-table contains a table of 3 columns: time, input_url, besticon_url.
A single input_url can map to multiple besticon_urls (i.e. a page might have many
favicons). And the time-column is just a timestamp without a timezone, so that we
know when the URL has been last-crawled -- and we can also prioritize re-crawling
by staleness.

Here is the schema for this table:

XXX-TODO

The besticon_err-table contains three columns: id, time, input_url, error. The id
is just a UUID to help us distinguish errors, and the timestamp is there so that
we can get an idea of how recent an error was. The error itself is just a string
that contains a JSON.stringify'ed Error-object. We could probably use PG's built-in
JSON-type, but wasn't sure if we wanted to use our own error-format or not.

Here is the schema for this table:

XXX-TODO

## DB Selection

Right now, the process for changing the DB is pretty manual.
The credentials are located in `shared/queue.ts` (for the PG backend),
and in `etl/index.ts` for the (ETL phase). Yes, they have to be
separate, in order to facilitate testing of the ETL phase (using
the PG backend as an input queue -- but not output queue).

## Backend Selection

Each phase has -- in their respective `index.ts` files -- a global
`BACKEND` variable, which can be set to: `Backend.SQS`, `Backend.PG`, or
`Backend.PubSub`.

The PubSub backend has bitrotted and is unusable/broken.

## How The Pipeline 'Detects' Grey Area Entities

In addition to the extension being able to report unlock/flagged sites as grey-area
entities, the pipeline can interpret some sites as being grey-area.

  * If a site has zero favicons
  * If a site has 0x0000... or 0xffff... as a blockhash
  * If a site has a high rank, but many overlapping blockhashes (i.e. maybe it uses
    the wordpress favicon, maybe it has one of those colored-squares-plus-letter favicons).
  * If a site has experienced a hashing error
  * If a site has experienced a besticon (favicon discovery) error


## Planned Features

### Per Phase Parallelism

When using services like PubSub and SQS, one of the selling points is that
parallel delivery is handled for you "for free". With the DB-backend,
running multiple instances of the same phase, can result in queries that
return the _same_ batch to different instances. We want to fix this by assigning
an `offset` argument to each instace. This way, we query the DB with an additional
`OFFSET N` clause, forcing each instance to get a _different_ page of data.

### DB Inspector

The DB Inspector is a CLI utility that takes parameters and lets you query the
DB for domain-relevant information (i.e. which websites have overlapping blockhashes,
which websites have experienced hashing-errors or besticon-errors, and what were
those errors). The Inspector can also act as an injector and inject "fake" errors
so that we can test the various code-paths.

### Discord Bot For Pipeline

We can create a discord bot that is basically just a wrapper around the DB Inspector
and can accept commands and return output (or links to stored outputs if they are too
big). Definitely a very exciting possibility. Even simple things like getting the
status and health of the pipeline could prove to be immensely useful.

#### More Blockhash Algorithms

Support other hashing algorithms like pHash. For this it might make sense to
actually have separate tables for each hashing algorithm, keyed by the MD5 of
the favicon.

#InterlockTech