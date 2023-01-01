End users usually want more software than what is actually in the project source tree. These pieces of software that do not belong in the source tree of the DragonFlyBSD project are called ports, or DPorts in our case. A DPort is basically a receipe that a maintainer writes, to make it easier for someone else to build the source code of that particular piece of sofware on DragonFlyBSD. And as a lot of different languages and softwares exist, many receipes are required, thus many DPorts lie in the DPort repository. 

A port that has been compiled or just packaged (not all are compiled actually) is call a *package*. That is what one user installs when he or she needs to use a software.

Packages can be installed through 2 different processes.

One can build them from the sources, using the [DragonFly Ports (DPorts)](https://gitweb.dragonflybsd.org/dports.git), or one can install binary packages pre-built by the DragonFlyBSD team and available through different mirrors.

It should be noted that building from sources requires a substantial amount of resources (CPU, RAM, storage) and having a dedicated machine for that purpose is recommended, so for most users using the binary packages is the easiest and fastest solution.

Even if you decide to use the binary packages it can be useful and interesting to read about [DPorts](/user-guide/install-software/#dports).

## Binary packages

These are just pre-built DPorts packages made available for users that don't have the opportunity or do not want to build their own ports. They are released once having been built on DragonFlyBSD owned machines, from the files one can find in the public DPort repository.

They are always available both for the current release and for bleeding-edge.

Two servers are used for the building process: 

- [Loki](https://loki.dragonflybsd.org/dports/) for the release target
- [Thor](https://thor.dragonflybsd.org/dports/) for the bleeding-edge one

The [primary mirror](https://avalon.dragonflybsd.org/dports/) is based in the USA and can be quite slow for people living far away. But there are mirrors available all over the world.

To setup a new mirror, the configuration file `/usr/local/etc/pkg/df-latest.conf` has to be edited. It's usually just a matter of enabling or disabling the desired mirrors.

New sets of packages are published more or less every quarters, and it has to be noted that mirrors are usually lagging for one or two days when the new set is released, depending on how frequently they synchronize with the primary mirror.


## DPorts

Building from sources is interesting as one can change options of said software to fit one's needs for example. It is also required in order to contribute to the DPorts.

In order to achieve building the ports properly, the official method is the following :

- Clone the Dports git repository
```bash
root@dfly# cd /usr && make dports-create
```

- Update the dports if needed
```bash
root@dfly# cd /usr && make dports-update
```

- Configure dsynth and carefully read [dsynth's manpage](https://man.dragonflybsd.org/?command=dsynth&section=ANY)
```bash
root@dfly# dsynth init
root@dfly# mkdir -p /build/synth/{live_packages/All,options,distfiles,build,logs}
root@dfly# ln -s /usr/dports /build/synth/dports
```

- Start a port build
```bash
# One can easily find the list of installed packages with pkg prime-list and feed it to dsynth
root@dfly# dsynth build www/firefox
```

- Configure your own repository as a source of packages
```
Local: {
	url		: file:///build/dsynth/packages,
	mirror_type	: NONE,
	enabled		: yes
}
```

- (Re-)Create the repo
```bash
root@dfly# dsynth rebuild-repository
```

## pkg usage

Once setup by either of the two methods, the only tool to use is `pkg` which has many features that you can check using `pkg help`.

To get you started quickly :

- Search for software
```bash
user@dfly% % pkg search firefox
```

- Install software
```bash
root@dfly# pkg install doas
```

- List volontarily installed software (not installed as dependencies)
```bash
user@dfly% pkg prime-list
```

## Contribute

Soon to be filled.
