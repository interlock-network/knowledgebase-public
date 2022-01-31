# Blockhash Pipeline

This is a centrally managed system that uses the same
[threat-indicators](./visual-threat-indicator.md) as
the [interlock-extension](./interlock-extension.md) to crawl
and classify web-pages. Instead of using [TOFU](./trust-on-first-use.md)
it uses a harmonic centrality measure computed by the common-crawl
project since its last crawl over the web.

#InterlockTech