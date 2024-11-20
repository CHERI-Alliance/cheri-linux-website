---
title: 'Introduction'
date: 2023-04-25T15:14:39+10:00
weight: 2
---

This page describes what CHERI Linux is and on what virtual platform or real hardware that you can run it on.

<!--more-->

CHERI Linux is a project to add memory-safety to the Linux kernel and to user-space applications by enhancing software to take full advantage of CHERI, a hardware memory access technology.

To find out more about CHERI and what it can do, visit the [CHERI Alliance website](https://cheri-alliance.org/).

# Supported architectures

We currently support CHERI Linux on Arm and RISC-V. In future, we may also support it on other ISAs and implementations that have been extended with CHERI, such as x86.

To date, CHERI Linux has been implemented on the following ISAs which are suitable for running Linux :

1. [Arm Morello v8-A](https://developer.arm.com/documentation/ddi0606/latest/) : an extension of Armv8-A
2. [CHERI-RISC-V RV64](https://github.com/riscv/riscv-cheri) : an extension of the RISC-V ISA (64 bit only)

## CHERI Linux on a virtual platform

CHERI Linux is currently supported on two virtual platforms:

1. Arm Morello using an Arm [Fixed Virtual Platform (FVP)](https://www.arm.com/products/development-tools/simulation/fixed-virtual-platforms)
2. CHERI-RISC-V using [QEMU-CHERI](https://github.com/CHERI-Alliance/qemu)

## CHERI Linux on real hardware

CHERI Linux can boot on the following hardware:

1. The [Morello Board](https://www.arm.com/architecture/cpu/morello)
2. The Codasip X730 FPGA platform

The documents on this web site provide further information on how to build and run CHERI Linux, how to develop applications and what our plans are for the future.

