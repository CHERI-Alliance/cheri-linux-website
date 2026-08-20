---
title: 'Getting Started with Debian on QEMU'
date: 2026-08-19
---

This page contains some simple instructions to build and boot into a plain vanilla Debian environment running on a RISC-V or ARM-based CHERI virtual machine in QEMU.

## Setup

We will use the `cheribuild.py` script from the University of Cambridge to simplify the process of building and running QEMU with support for CHERI. These instructions are for a Debian/Ubuntu host machine, but [cheribuild's README](https://github.com/CTSRD-CHERI/cheribuild/) has instructions for setting up your development environment on MacOS, RHEL/Fedora, FreeBSD, and Arch Linux hosts.



### Install dependencies

On a Debian/Ubuntu host machine, you can install the packages required for the most commonly used cheribuild targets with:

```
apt install autoconf automake libtool pkg-config clang bison cmake mercurial ninja-build samba flex texinfo time libglib2.0-dev libpixman-1-dev libarchive-dev libarchive-tools libbz2-dev libattr1-dev libcap-ng-dev libexpat1-dev libgmp-dev bc tzdata
```

A few additional dependencies are needed for running Debian on QEMU:

```
apt install device-tree-compiler python3-setuptools libssl-dev
```

### Build and run the QEMU VM

Clone the cheribuild source repo:

```
git clone git@github.com:CTSRD-CHERI/cheribuild.git
```

From the `cheribuild/` source directory run the cheribuild script:

```
./cheribuild.py run-debian-on-cheri-linux-riscv64-purecap --linux-kernel/git-revision cambridge-morello-7.0 -d
```

This command specifies that cheribuild should:

 * Build and run Debian on a RISC-V purecap target `run-debian-on-cheri-linux-riscv64-purecap` (for Debian on a Morello purecap target use `run-debian-on-cheri-linux-morello-purecap`)
 * Use the Linux Kernel version `cambridge-morello-7.0`
 * Build all dependencies necessary to build and run the QEMU VM (that's the `-d` at the end)

The build will take a while, and near the end it will pause to ask you to set your timezone and root password. After completing that configuration, it will drop you into a login prompt for the Debian image running in a QEMU VM. Login with user `root` and the password you set.

## Access the VM over SSH

You can SSH into the VM from the host machine as soon as it launches, since cheribuild sets this up for you automatically. The port number is variable, because cheribuild was designed for a shared build system. Near the end of the build process, cheribuild will show a message that tells you which port to use for SSH from the host machine:

```
Listening for SSH connections on localhost:<port>
```

Then ssh into the guest from the host with the same username and password you used on the login prompt:

```
ssh -p <port> root@localhost
```

If you want SSH to listen on a specific port on the host machine, you can add the command-line option `--run/ssh-forwarding-port <port>` when you call `cheribuild.py`.
