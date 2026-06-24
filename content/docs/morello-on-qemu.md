---
title: 'Getting Started with Morello Linux on QEMU'
date: 2026-06-24
---

This page contains some simple instructions to setup a QEMU VM with everything you need to build and boot into a Morello Linux environment.

**Note:** This approach does not require Morello hardware.

## Setup

We will use the `cheribuild.py` script from the University of Cambridge to simplify the process of building and running QEMU with support for the Morello platform. These instructions are for a Debian/Ubuntu host machine, but [cheribuild's README](https://github.com/CTSRD-CHERI/cheribuild/) has instructions for setting up your development environment on MacOS, RHEL/Fedora, FreeBSD, and Arch Linux hosts.



### Install dependencies

On a Debian/Ubuntu host machine, you can install the packages required for the most commonly used cheribuild targets with:

```
apt install autoconf automake libtool pkg-config clang bison cmake mercurial ninja-build samba flex texinfo time libglib2.0-dev libpixman-1-dev libarchive-dev libarchive-tools libbz2-dev libattr1-dev libcap-ng-dev libexpat1-dev libgmp-dev bc tzdata
```

For Morello Linux specifically, a few additional dependencies are needed:

```
apt install device-tree-compiler python3-setuptools libssl-dev
```

### Get cheribuild

Clone the cheribuild source repo:

```
git clone git@github.com:CTSRD-CHERI/cheribuild.git
```

At the moment, using a Morello Linux image in cheribuild requires some patches that haven't been merged into the main branch yet, so you'll need to checkout the `linux_debian` branch:

```
cd cheribuild
git fetch
git checkout --track origin/linux_debian

```

### Build and run the QEMU VM

From the `cheribuild/` source directory run the cheribuild script:


```
./cheribuild.py run-morello-debian-on-cheri-linux-morello-purecap --linux-kernel/git-revision cambridge-morello-7.0 -d
```

This command specifies that cheribuild should:

 * Build and run the target `run-morello-debian-on-cheri-linux-morello-purecap`
 * Use the Linux Kernel version `cambridge-morello-7.0`
 * Build all dependencies necessary to build and run the QEMU VM (that's the `-d` at the end)

The build will take a while, but at the end it will drop you into a login prompt for the Morello Linux image running in a QEMU VM. Login with Morello's default user `root` and  password `morello`.

## Access the VM over SSH

You can SSH into the VM from the host machine as soon as it launches, since cheribuild sets this up for you automatically. The port number is variable, because cheribuild was designed for a shared build system. Near the end of the build process, cheribuild will show a message that tells you which port to use for SSH from the host machine:

```
Listening for SSH connections on localhost:12345
```

If you want SSH to listen on a specific port on the host machine, you can add the command-line option `--run/ssh-forwarding-port <port number>` when you call `cheribuild.py`.
