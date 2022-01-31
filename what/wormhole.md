# Wormhole

Wormhole is a network that makes it possible for Solana an Ethereum
(among others) to interoperate. The way it works is that each
blockchain runs a `wormhole` contract. When you want to send an
asset from SOL->ETH, you invoke the `wormhole` contract, giving it
your asset, which it stores in its own account. Then, the wormhole-network
(which is snooping on all transactions involving wormhole-contracts)
invokes the corresponding wormhole-contract on the target-chain, and it
transfers those assets into a target account.

In a way, it is basically cross-chain message-passing. Projects use
wormhole in order to take advantage of the strengths of different
chains. Apparently, a project has used Wormhole to offload transactions
from ETH to SOL, when the ETH gas-fees get too high.

These kinds of applications are arguably neither ETH nor SOL apps,
but rather Wormhole apps.

We use Wormhole to allow users to use/choose ETH or SOL as the backend.
This means that it is yet another point-of-failure for us, but the strategic
flexibility it affords us is too valuable.

#BaseTech