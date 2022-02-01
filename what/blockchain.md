# Blockchain

Invented (or at least popularized) by Bitcoin's Satoshi Nakamoto.
It is (effectively) an append-only data-structure that operates
and is updated globally. It depends on consensus between the peers
to maintain the consistency of its data, which is under threat from
entropy and malicious actors.

Given that the consensus is expensive, it is very slow when compared to
actual transaction-processing systems. The first consensus-mechanism
depended on [proof-of-work](./proof-of-work.md), in which computers
solved cryptographic-puzzles to earn the right to broadcast a block
to the network (which is in turn verified by other nodes). Newer
blockchains use [proof-of-stake](./proof-of-stake.md) in which nodes
get voting-power that is proportional to the coins that you own on the
network.
