---
supertitle: 'Monthly News Update: July 2026'
title: 'CVA6 support, a test suite for POSIX-based OSes and work on glibc'
author: 'Paul Metzger'
date: 2026-08-07
draft: false 
categories: ['featured']
---
Hesham Almatary's work at Capabilities Ltd has reached a significant milestone in the platform bring-up of [CHERI-CVA6](https://github.com/Capabilities-Limited/cheri-cva6/). As a reminder, CHERI-CVA6 is a 64-bit CHERI-RISC-V CPU that's being developed by Capabilities Ltd as part of the [COSMIC project](https://cosmic-project.lowrisc.org/cosmic/index.html). With Hesham's work, a configuration comprising a purecap kernel and purecap user space based on BusyBox and musl libc is running on the platform. The corresponding cheribuild targets can be found in the [cva6-cheri branch](https://github.com/CTSRD-CHERI/cheribuild/tree/cva6-cheri). In addition, [RVY](https://riscv.github.io/riscv-cheri/) CHERI-RISC-V QEMU targets are available for this musl libc-based configuration and a Debian-based configuration with a non-CHERI user space that can run purecap binaries.

Paul Metzger of the University of Cambridge released a preview version of the [cheriostest](https://github.com/CTSRD-CHERI/cheri-os-test) test suite, targeting POSIX-based OSes that were ported to CHERI, such as CheriBSD and the Linux ports. The test suite includes over 300 tests covering a wide range of low-level interfaces and functionality. Cheribuild targets for Linux are available in cheribuild's main branch. It is heavily based on CheriBSD's cheribsdtest test suite, which it will eventually replace.

Christian Ehrhardt of Codasip continued to work on a CHERI port of glibc and reported that most tests are now passing. As glibc is used by many Linux distributions, porting it to CHERI will be an important step towards a purecap Linux desktop environment.

The working group discussed how to handle security mitigations that are likely unnecessary with a purecap kernel, such as ASLR and pointer hashing.

Pawel Zalewski of the Capable Hub contributed to Uwe Kleine-König's cleanup work, which will benefit future CHERI upstreaming efforts. The Capable Hub's other CHERI-related activities are still temporarily paused.
