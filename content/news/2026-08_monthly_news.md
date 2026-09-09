---
supertitle: 'Monthly News Update: August 2026'
title: 'POSIX man page extensions, setup guides, Debian userspace and test suite work'
author: 'Paul Metzger'
date: 2026-09-09
draft: false 
categories: ['featured']
---
During the development of CheriBSD and CHERI support for Linux, POSIX interfaces had to be extended for CHERI. The two efforts made differing design decisions, hurting portability and motivating a review of these extensions. Since November last year, Paul Metzger of the University of Cambridge has been driving efforts to realign CHERI-related operating system interfaces. Over the last months, he has catalogued the divergences between CheriBSD and Linux variants that support CHERI; this document is available on request. He has also published a preview version of [cheri-os-test](https://github.com/CTSRD-CHERI/cheri-os-test), a CHERI-specific OS test suite, which is heavily based on [cheribsdtest](https://github.com/CTSRD-CHERI/cheribsd/tree/main/bin/cheribsdtest).  
For the next stage of this work, he recently received permission to augment the POSIX man pages with CHERI-specific documentation and to publish the modified versions. He and the group at Cambridge plan to expand this permission to cover the entire POSIX specification. The annotated documents will support ongoing realignment efforts and guide future work on CHERI support for other POSIX-based operating systems. As part of this work, he also resumed discussions on the [mailing list](https://lists.cheri-alliance.org/mailman3/hyperkitty/list/wg-support-portability@cheri-alliance.org/) of the OS Support & Portability Working Group.

Allison Randal of Capabilities Ltd added guides to cheri-linux.org, improving the documentation for Linux on CHERI. These are available [here](https://cheri-linux.org/docs/start/).

Hesham Almatary of Capabilities Ltd and the University Cambridge is working on running Linux with CHERI support and a legacy Debian user space on CVA6-CHERI. While the stock Debian user space consists of non-CHERI binaries, this setup is capable of running purecap binaries. He also integrated cheri-os-test (see above) into Cambridge's CI system.

Alexander Richardson created a CMake-based build system for cheri-os-test. Paul merged it into the development branch and is involved with final refinements of the build scripts.
