# Reden snap

First shot at packaging `reden-cli`, `reden-tx`, `redend`, and `reden-qt` in a snap for easy installation on Linux systems.

It's currently only tested on Ubuntu 18.04 with X11, so please test on other desktop environments if you will.

**DISCLAIMER**

This repository is purely intended as an exercise in creating snap packages. Don't use this wallet to store crypto without a proper audit of both the snap and the upstream Reden repository. In other words: don't trust random code on the interwebs!

# Installing

On any snap enabled Linux system:

```
$ snap install reden
$ reden.reden-qt
```

You can now see all installed applications by running `snap info reden`.

# Building

You normally don't need this part. This part explains building the snap, which you don't need as a user of the software.

The snap is build in a "cleanbuild" LXD container to make sure the build instructions are not polluted by random libraries installed on my system. It's slower (no caching) but makes sure you don't forget to include packages you might have on your system but are not available by default on an Ubuntu 16.04 system.

From the root directory of this repository run:

```bash
$ snapcraft cleanbuild
$ snap install reden_0.1_amd64.snap --dangerous
```

You can use `snapcraft cleanbuild --debug` to be dropped in the container's shell if the build fails.

# Known issues

- URL opening doesn't work on Ubuntu 18.04. This is a confirmed bug and has been fixed in snapd: https://github.com/snapcore/snapd/pull/4495
- The reden-qt application icon is missing since it's not correctly specified in the Reden repository: https://github.com/RedenCore/Reden/blob/master/contrib/debian/reden-qt.desktop.desktop#L8
- Starting reden-qt throws an AppArmor warning related to dbus, needs fixing.