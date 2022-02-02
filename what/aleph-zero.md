# Aleph Zero

A Level-1 Blockchain that could conceivably compete with Solana in the future.
They are privacy-focused, in the sense that data can be hidden, and
transaction-meta-data (i.e. recipient, sender, funds, etc) can also be
hidden from public scrutiny.

They do not _quite_ support smart-contracts. They released experimental
support on Jan 27, 2022. They also have a system called `substrate` which
allows writing of smart-contracts in the `ink` language. They are
compatible with polkadot, but they use their own consensus-protocol.

Their consensus-protocol is peer-reviewed, and based on DAGs
(directed-acyclic-graphs), whereas other chains usually just use a
linear sequence of blocks (therefore, a block _chain_).

It is the difference between having a line and having many parallel lines
that occaisionally criss-cross with each other.

They have a privacy system named `liminal` which is accessible from Ethereum
and Solana, among others. We should explore how we could/would integrate
with this system (which appears unique  -- something no other
chain has).

Also, they will not be EVM compatible because of the poor performance of
EVM. But they might change course, if it makes business sense. They use
a rotating-selection-method for selecting validator-nodes. See:
[validator-election](./validator-election.md).

