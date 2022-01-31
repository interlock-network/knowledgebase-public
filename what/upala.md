# Upala

[Upala](https:://upala.id) is a [proof-of-personhood](./proof-of-personhood.md)
system developed by [Peter Porobov](../who/peter-porobov.md). It is decentralized
and blockchain powered. It was first written for Ethereum, but has been ported to
Solana.

It uses photographs and random-handshakes to verify that people are who they say
they are. It even requires twins to verify that they _each_ exist. Basically,
someone sends a picture and their id-info, and another person in the same
geography (usually a city), is tasked with staking that the picture matches
and the person is who they say they are. Much like with our own staking
mechanism, if the person-to-be-verified is lying his stake gets confiscated.
If the verifier is lying (or just incompetent), his stake also get confiscated.
The idea is that a single verifier can lie, can most of them won't. If you get
caught lying your credibility goes down, and you get less opportunities to lie
in the long term.

We are looking at this system (and at many other like this) to protect against
[sybil-attacks](./sybil-attack.md).