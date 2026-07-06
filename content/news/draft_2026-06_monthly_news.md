---
supertitle: 'Monthly News Update: June 2026'
title: 'Linux on CHERI with legacy Debian userspace, CVA6 support, CHERI-Enabled Linux 7.1 released'
author: 'Paul Metzger'
date: 2026-07-06
draft: true
categories: ['featured']
---
As usual, Codasip continued to stay on top of recent Linux kernel releases and published v7.1 of Linux on CHERI. Codasip have also contributed their RVY adaptation of the Linux Test Project (LTP) to the CHERI community.

Hesham Almatary combined Linux on CHERI with the Debian userspace, using the compatibility layer to support non-CHERI legacy software. He also created cheribuild targets for generating Debian images running Linux on CHERI. With his Morello pull requests now being merged, this works on Morello and on RVY. As this simplifies porting software to Linux on CHERI, the working group discussed approaches for providing CHERI LLVM for these images.

Uwe Kleine-König anticipates that his patches, which are expected to ease future upstreaming efforts, will likely be included in the next upstream Linux v7.2 release. He is currently maintaining around 130 patches, which will likely make him one of the top contributors to the v7.2 release.

Benjamin Braddock and Hesham have been working on CVA6 support and were able to boot the Linux on CHERI fork. Yocto meta-cheri support and cheribuild targets for running Linux on CVA6 are currently work in progress.

Allison has tested externally developed CHERI-porting tools. Additionally, she worked on guides on cheri-linux.org and led discussions around hosting the website on CHERI system.

Unfortunately, UKRI funding for the Capable Hub has stopped and most employees have ceased working on CHERI. It is anticipated that this only temporary.
