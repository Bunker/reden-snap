# Reden snap

Snap pacakge for the `reden-cli`, `reden-tx`, `redend`, and `reden-qt` binaries for easy installation on Linux systems. Check the [Reden repostory](https://github.com/RedenCore/Reden) for more information about the Reden project.

It's currently only tested on Ubuntu 18.04 with X11, so please test on other desktop environments if you will.

<details>
  <summary>What is Reden?</summary>
  <p>Reden is a fully decentralised cryptocurrency built on the premise of providing anonymity, speed, fair mining by being ASIC-resistant and reliability by the usage of masternodes.</p>
</details>

<details>
  <summary>What is a snap?</summary>
  <p>Snaps are containerised software packages that are simple to create and install. They auto-update and are safe to run. And because they bundle their dependencies, they work on all major Linux systems without modification.</p>
</details>


> **DISCLAIMER**
>
> This repository is purely intended as an exercise in creating snap packages. Don't use this wallet to store crypto without a proper audit of both the snap and the upstream Reden repository. In other words: don't trust random code on the interwebs!

# Installing

On any snap enabled Linux system:

```
$ snap install reden-cimm --edge
$ reden-cimm.reden-qt
```

You can now see all installed applications by running `snap info reden-cimm`.

Note: the final package should obviously be named `reden` and not `reden-cimm` but I don't want to squat that name, I'll leave that up to the Reden team.

# Building

You normally don't need this part. This part explains building the snap, which you don't need as a user of the software.

The snap is build in a "cleanbuild" LXD container to make sure the build instructions are not polluted by random libraries installed on my system. It's slower (no caching) but makes sure you don't forget to include packages you might have on your system but are not available by default on an Ubuntu 16.04 system.

From the root directory of this repository run:

```bash
$ snapcraft cleanbuild
$ snap install reden-cimm_0.1_amd64.snap --dangerous
```

You can use `snapcraft cleanbuild --debug` to be dropped in the container's shell if the build fails.

# Known issues

- You need to pick a custom data directory at first boot since the snap is confined and can't use the default one.
- URL opening doesn't work on Ubuntu 18.04. This is a confirmed bug and has been fixed in snapd: https://github.com/snapcore/snapd/pull/4495
- Starting reden-qt throws an AppArmor warning related to dbus, needs fixing.

# License

This repository is licensed under the [MIT license](LICENSE). The Reden application icon is a cropped copy of the [splash.png](https://github.com/RedenCore/Reden/blob/master/splash.png) image from the [Reden project](https://github.com/RedenCore/Reden) and also MIT licensed.
