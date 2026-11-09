---
supertitle: 'Monthly News Update: October 2026'
title: 'Draft Specification Update and CHERI QEMU Improvements'
author: 'Paul Metzger'
date: 2026-11-09
draft: false 
categories: ['featured']
---
The [RISC-V draft specification for CHERI extensions](https://riscv.github.io/riscv-cheri/) has recently been updated to version 0.9.10, introducing changes to ISA mnemonics and semantics. Tariq Kurd of Codasip presented an overview of these changes to the working group.

Support for the new version is currently being merged from the LLVM fork maintained by the group at the University of Cambridge into the CHERI Alliance's LLVM fork. Codasip's Linux kernel fork does not yet support the latest draft version.

Christian Ehrhardt worked on performance improvements for CHERI QEMU, substantially reducing execution time in some cases.
