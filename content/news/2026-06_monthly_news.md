---
supertitle: 'Monthly News Update: June 2026'
title: 'Linux on CHERI with Debian user space, CVA6 support, CHERI-Enabled Linux v7.1'
author: 'Paul Metzger'
date: 2026-07-06
draft: false 
categories: ['featured']
---
As usual, Codasip kept pace with recent Linux kernel releases and published v7.1 of Linux on CHERI. The company also contributed its RVY adaptation of the Linux Test Project (LTP) to the CHERI community.

Hesham Almatary combined Linux on CHERI with the Debian userspace, using the compatibility layer for non-CHERI legacy software. He also created cheribuild targets for generating Debian-based images. With his Morello pull requests now merged, this works on both Morello and RVY. Because this significantly simplifies porting software to Linux on CHERI, the working group discussed options for providing CHERI LLVM for this setup.

Uwe Kleine-König anticipates that his patches will be included in the next upstream Linux v7.2 release. These patches are expected to ease future upstreaming efforts, and with currently around 130 submitted by him, he will likely be one of the top contributors to this release.

Benjamin Braddock and Hesham have been working on CVA6 support and successfully booted the Linux on CHERI fork. Yocto meta-cheri support and cheribuild targets for this are currently work in progress.

Allison Randal worked on guides available on cheri-linux.org and participated in discussions about hosting the website on a CHERI system. She also tested externally developed CHERI porting tools. 

Unfortunately, UKRI funding for the Capable Hub has stopped and most employees have ceased working on CHERI. It is anticipated that this is only temporary.
