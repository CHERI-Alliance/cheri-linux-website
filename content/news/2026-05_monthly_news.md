---
supertitle: 'Monthly News Update: May 2026'
title: 'CHERI-Enabled Linux 7.0 Released, Platform Support and Toolchain Improvements'
author: 'Paul Metzger'
date: 2026-06-05
draft: false
categories: ['featured']
---
As in the previous month, working group members have been busy with a range of Linux kernel and user space-related endeavours. Notably, Codasip has released a CHERI-enabled Linux v7.0 kernel, making a very recent kernel available to the working group and the general public.

Following Codasip's release, Hesham Almatary of the University of Cambridge created multiple pull requests for Morello support. His fixes are also available in a temporary branch while the pull requests are under review. In addition, he advanced Morello user-space support. He is achieving near feature parity with Morello Linux, with only three additional tests failing (out of over 200 test cases). [Morello](https://www.morello-project.org/) is a hardware prototype featuring CHERI-enabled ARM® Neoverse N1 server-class cores, and Morello Linux is a corresponding CHERI-enabled Linux variant. 

Hesham also made significant progress with CVA6-CHERI support, a RISC-V CPU design developed as part of the [COSMIC](https://cosmic-project.lowrisc.org/) project. With his patches, the CHERI-enabled Linux fork is now operational on CVA6-CHERI, supported by his improved U-Boot implementation for the platform. The [cheribuild](https://github.com/CTSRD-CHERI/cheribuild) scripts have also been extended to support creating disk images for CVA6-CHERI and booting them in QEMU with CHERI support. 

Pawel Zalewski of The Good Penguin/The Capable Hub has done initial work to enable the use of the Syzkaller kernel fuzzer on Linux on CHERI. BayLibre continued to submit patches to the Linux kernel mailing list that will indirectly help with future CHERI upstreaming efforts, leading to useful discussions. Markus Schneider-Pargmann of BayLibre created a pull request to add `PROT_CAP` and `PROT_NO_CAP` to Linux on CHERI. These flags are available in CheriBSD and provide control over whether capabilities can be stored in memory mappings, for example when passed to mmap(). Adding these flags was motivated by Paul Metzger's (University of Cambridge) efforts to align CHERI-related interfaces between Linux on CHERI and CheriBSD. Paul refined his portable adaptation of the CheriBSD test suite, cheribsdtest, with the goal of publishing it in the near future. In the course of this, he also contributed improvements to Morello LLVM. 

Allison Randal of Capabilities Ltd and Carl Shaw of Codasip began improving permission management for the Linux-related CHERI Alliance repositories, with the aim of enabling members of the wider CHERI community to help review pull requests. 
