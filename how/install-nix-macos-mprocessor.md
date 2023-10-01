# How to install nix on M1 mac computer?

_Created: 10/30/23
_Last updated: 10/30/23

## Problem overview

Following the standard Nix installation process for Macintosh computers with M1 processors fails. The following instructions work.

If you experience this problem, then you will encounter 

```
-bash: nix-shell: command not found
```

## Install Nix

Run

```
bash <(curl -L https://nixos.org/nix/install)
```

then in new terminal verify installation:

```
nix --version
```

## Set up binary caches

This will include IOG and cachix substitutes. [Learn more about Nix / IOG / IOHK binary caches in this knowledgebase piece here.](../what/iog-iohk-binary-cache.md)

Create a nix config file:

```
sudo vim /etc/nix/nix.conf
```

It must include this text:

```
build-users-group = nixbld

substituters = https://cache.iog.io https://iog.cachix.org https://cache.nixos.org/

trusted-public-keys = cache.iog.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iog.cachix.org-1:nYO0M9xTk/s5t1Bs9asZ/Sww/1Kt/hRhkLP0Hhv/ctY= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=

system = x86_64-darwin
# system = aarch64-darwin

extra-platforms = x86_64-darwin aarch64-darwin
```
Save and exit file.

Finally, get cache info for nix store.

```
curl cache.iog.io/nix-cache-info
```

## That is it

When you the run `nix-shell` to launch shell for whatever application you are trying to run for the first time, you will see Nix build the relevant derivations, fetch paths, create symlinks. This will look something like this:

```
these 2 derivations will be built:
  /nix/store/akch1jy6h8k3icxfdchvy50hf9xr0jnl-builder.pl.drv
  /nix/store/myjlxfnlrcqh770a5x6z4f5ik0wc1jsc-python3-3.11.4-env.drv
these 146 paths will be fetched (171.51 MiB download, 982.87 MiB unpacked):
  /nix/store/wsq8qi2cl2mf75vwj8v6r8j8q1m105s6-Libsystem-1238.60.2
  /nix/store/00pc3kx1hc3ynwx5gc0c1j990hnh3bc2-Security-55471.14.18
...
copying path '/nix/store/3ln9yvs9pg78qvabh89y0a4m1hqzyl1h-bash-5.2-p15' from 'https://cache.nixos.org'...
copying path '/nix/store/a8rwng1223bqibn10zsij7pkfqh05p90-adv_cmds-119-locale' from 'https://cache.nixos.org'...
copying path '/nix/store/wsq8qi2cl2mf75vwj8v6r8j8q1m105s6-Libsystem-1238.60.2' from 'https://cache.nixos.org'...
...
copying path '/nix/store/mwjdyhkhkcjk7jxqzwg8fyxzvj9jcagd-make-binary-wrapper-hook' from 'https://cache.nixos.org'...
copying path '/nix/store/rz54rq2civz8a7hlqgw30japnycv4d0q-stdenv-darwin' from 'https://cache.nixos.org'...
building '/nix/store/myjlxfnlrcqh770a5x6z4f5ik0wc1jsc-python3-3.11.4-env.drv'...
created 433 symlinks in user environment
```

If this process succeeds, the shell will be active:

```
[nix-shell:~/_ROOT/interlock/galactus]$ 
```

## Important notes / troubleshooting

- If you are not using Rosetta 2 on your machine, then you will need to use the `aarch64-darwin` setting for the `system` parameter in nix.conf, while commenting out the `x86_64-darwin` architecture.

## Miscellaneous context

The issues with installing Nix on M1 Macs (Apple Silicon) originate from several factors, including differences in architecture and Apple's security measures. Here are the primary reasons:

1. **Different Architecture**: The M1 chip is based on ARM architecture (specifically ARM64 or `aarch64`), whereas most Macs before it were using Intel x86_64 architecture. This fundamental difference means that binary packages built for the older architecture won't run natively on the M1. As a result, software like Nix, which relies on precompiled binaries, will need to have ARM64-compatible binaries available or build from source, which can be more time-consuming.

2. **Rosetta 2 Limitations**: While M1 Macs come with Rosetta 2, which translates x86_64 instructions to ARM64, there are some limitations. Not everything runs perfectly under Rosetta, and there can be nuances, especially when dealing with system-level tools like Nix.

3. **System Integrity Protection (SIP)**: M1 Macs come with macOS Big Sur, which has heightened security measures, including SIP. Nix traditionally wants to install itself in `/nix`, a root-level directory, but SIP prevents such installations. There are workarounds involving creating a synthetic firmlink, but these steps go beyond the standard installation process.

4. **Incomplete Tooling & Binaries**: Even if you manage to install Nix on an M1 Mac, there's another challenge: not all packages available in the Nix repositories have ARM64 binaries. This means that even if you get Nix working, some packages might not be readily available or might need to be built from source.

5. **Rapid Development Environment**: The situation around Nix and M1 Macs is rapidly evolving. The Nix community has been working to improve compatibility, so while early adopters faced many challenges, the situation has been improving over time as more fixes and binaries become available.

The above challenges made the standard installation process for Nix not directly applicable or efficient for M1 Macs. However, the Nix community and other open-source communities are known for their resilience and adaptability, so workarounds and improvements are continually being developed.
