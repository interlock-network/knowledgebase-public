# NixOS

NixOS is part of a family of systems that are fully reproducible. This
means that regardless of the time of the day, the temperature outside,
the position of the sun, the software will compile. The environment is
extremely reliable and dependable.

NixOS provides a useful environment to develop and deploy containers.

There are a couple of facilities that make NixOS particularly
attractive for usage in deployment:

## Rollbacks

All upgrades because they are declarative and functional can be rolled
back. This means that you don't have to worry about failed
upgrades. Your hardware will never be left in an irrecoverable state.

## Reproducible configurations

You can ensure that any software you build on your machine will build
exactly the same on any other machine. By building the system in a
completely functional way, all installs are exactly the same. You will
not be bitten by unexpected compatibilities between systems.

## Atomic Upgrades

Updating NixOS does not destroy a previous configuration. You will
find that you are able to go back in time to any previous
configuration. As with databases, atomicity strongly increases the
reliability of the system.
