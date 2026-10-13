---
supertitle: 'Monthly News Update: September 2026'
title: 'Temporal Safety Development, Purecap glibc Progress and CHERI-RISC-V Renaming'
author: 'Paul Metzger'
date: 2026-10-13
draft: false 
categories: ['featured']
---
One of the major differences between the Linux fork for CHERI and CheriBSD is that the fork lacks a temporal safety subsystem. To address this, Codasip have started developing a revoker, which is currently a work in progress and not yet publicly available. Additionally, Codasip have started work on hardening the kernel's [eBPF](https://ebpf.io/what-is-ebpf/) subsystem with CHERI. 

While a purecap port of musl libc is available for use with the Linux fork, musl is more commonly used for containers and embedded systems than desktops or servers. The majority of Linux distributions use glibc instead. Codasip have been working on a purecap port of glibc and reported that most of its tests are now passing. This would be an important building block for a possible future Linux distribution for CHERI systems.

Other working group members have also made progress in various areas. Hesham Almatary has continued to work on CHERI-CVA6 support. Paul Metzger merged a CMake-based build system, authored by Alexander Richardson, for the [cheri-os-test](https://github.com/CTSRD-CHERI/cheri-os-test) test suite. Christian Ehrhardt has also been investigating potential performance improvements for CHERI QEMU.

In the wider CHERI ecosystem, work on adding support for the latest CHERI-RISC-V draft standard has commenced and has led to naming changes: `zcheri093` now refers to the older v0.9.3 draft standard, `rvy` refers to v0.9.9 and `xcheri` to [CHERIv9](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-987.pdf). These changes also affect cheribuild targets for the Linux fork, and work to update them is ongoing.

Kevin Brodsky of ARM has been in touch with engineers who worked on the Morello bring-up. Anyone who has encountered firmware bugs should contact him, as these engineers may be available to investigate and fix them.
