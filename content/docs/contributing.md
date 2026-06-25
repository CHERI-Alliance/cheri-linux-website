---
title: 'Contributing'
date: 2026-06-03
weight: 2
categories: ['sidebar']
---

The focus of the CHERI Linux Project is cross-architecture development work to adapt the Linux kernel and userspace software to benefit from CHERI's memory protection and software compartmentalization features. This work is still in an early stage, but builds on decades of collaborative open source development work, most notably:

* **CheriBSD:** A capability enabled Unix-like operating system that extends FreeBSD to run on hardware with CHERI memory protection and software compartmentalization features, such as the Arm Morello board and CHERI RISC-V.
* **Morello Linux:** An Arm-led research project started in 2022, which explores memory safety in OS environments based on the Linux kernel, targeting the Arm Morello board. This used a hybrid mode approach where most kernel pointers remained regular integers, with capabilities mainly at the syscall boundary.
* **Codasip RISC-V:** Codasip currently has a team working on Linux for CHERI on RISC-V that started with the hybrid Morello kernel and evolved it into a purecap implementation for their RISC-V embedded boards.
* **Linux/Unix Ecosystem:** Tens of thousands of open source projects integrated into Linux-based and Unix-based operating systems.

With this background, it is unsurprising that we consider healthy collaboration to be crucial to the success of Linux on CHERI, for a variety of reasons including:

* **Shared knowledge.** Open source projects often last longer than any individual contributor. Working together spreads knowledge about design choices and problems, so this information doesn't just stay with one person. This helps make projects resilient.
* **Diverse perspectives.** People use software in wildly different environments, for different purposes, and with different constraints. Contributors working on embedded, desktop, server, or security targets may encounter edge cases that the original authors never imagined. That diversity of perspective, when channeled well, can help create software that works for a wider range of users and use cases.
* **Trust and transparency.** When development is open and collaborative, users can see how decisions are made and who made them. This openness is a big part of why people, businesses, and organizations trust open source software with critical infrastructure.
* **Shared ownership and longevity.** Projects that are genuinely collaborative tend to attract more contributors, which creates a virtuous cycle — more contributors means more maintenance capacity, which means the project stays healthy longer. Projects that feel like a single person's fiefdom, even if technically "open," often struggle to build that kind of community.

## Repository Structure

The repositories managed by the CHERI Linux Project include:

* [busybox](https://github.com/CHERI-Alliance/busybox): A port of Busybox to CHERI, to support minimal Linux userspace builds
* [cheri-linux-website](https://github.com/CHERI-Alliance/cheri-linux-website): Source code for the [cheri-linux.org](https://cheri-linux.org/) website
* [linux](https://github.com/CHERI-Alliance/linux): A port of the Linux Kernel to CHERI, based on earlier work in Morello Linux
* [linux-roadmap](https://github.com/CHERI-Alliance/linux-roadmap): Source code for the CHERI Linux Project's [Roadmap](https://cheri-alliance.github.io/linux-roadmap/)
* [ltp](https://github.com/CHERI-Alliance/ltp): A port of the Linux Test Project to CHERI
* [meta-cheri](https://github.com/CHERI-Alliance/meta-cheri): A CHERI architecture layer for Yocto
* [musl](https://github.com/CHERI-Alliance/musl): A port of the musl to CHERI, to provide an implementation of the C standard library for Linux-based systems
* [opensbi](https://github.com/CHERI-Alliance/opensbi): A port of the OpenSBI project to CHERI-RISCV, an open-source implementation of the RISC-V Supervisor Binary Interface (SBI) specifications.
* [u-boot](https://github.com/CHERI-Alliance/u-boot): A port of the U-Boot project to CHERI, an open source boot loader for embedded boards.
* [yocto-manifest](https://github.com/CHERI-Alliance/yocto-manifest): A Yocto manifest file to build a CHERI-enabled Linux purecap userspace

Within these repos, we have two kinds of branches:

* Branches maintained and tested by a collaborative team across multiple projects and companies. In general, these branches are named `main` or starting with `cheri-`, while for repos with many branches, these may be named starting with `integration-` for clarity. Collaborative branches actively welcome pull requests, aim to serve as an integration point for different work streams, and balance the priorities of many contributors.
* Branches maintained by a smaller group. These branches may be focused more narrowly on the needs of a particular team, or may be a work-in-progress. For clarity, these branches are generally named with a project or company name at the start, like `morello-`, or `codasip-`.

## How to Contribute

We welcome contributions in many forms:

* Bug reports and fixes for software that has already been ported to CHERI
* Porting new software packages to Linux on CHERI
* Tests, including porting existing test suites from Linux or CheriBSD to Linux on CHERI
* Tools to help simplify the process of porting software to CHERI, or to help verify that a port was successful
* Documentation edits to improve exising docs and new guides for topics that aren't well documented are always appreciated


## Contributor Teams and Permissions

The CHERI Linux Project has 2 teams of contributors:

* CHERI Linux Project Contributors (GitHub Team) - have Triage permissions on all repos managed by the project, so they can help with managing issues and pull requests and edit the wiki, but can't merge pull requests or commit to the repo.
* CHERI Linux Project Maintainers - have Write or Maintain permissions on specific repos managed by the project, so they can merge pull requests, manage GitHub Actions, and create branches.

| contributor | permissions |
|:---|:---|
| Alfredo Mazzinghi | Write: linux |
| Allison Randal | Contributors Team; Admin: busybox, cheri-linux-website, linux, linux-roadmap, ltp, meta-cheri, musl, opensbi, u-boot, yocto-manifest |
| Carl Shaw | Contributors Team; Admin: busybox, cheri-linux-website, linux, linux-roadmap, ltp, meta-cheri, musl, opensbi, u-boot, yocto-manifest |
| Christian Ehrhardt | Maintain: linux; Write: busybox, musl |
| Florian Schmaus | Write: musl |
| Hesham Almatary | Write: busybox, linux, linux-roadmap, musl, u-boot; Future: meta-cheri |
| Jessica Clarke | Request: Contributors Team |
| Ka Leung Ho | Contributors Team; Write: opensbi, u-boot |
| Kevin Brodsky | Contributors Team; Write: linux |
| Paul Metzger | Contributors Team; Maintain: cheri-linux-website |
| Pawel Zalewski | Request: meta-cheri |
| Robert Watson | Contributors Team; Write: linux-roadmap, linux, musl |
| Stephen Smalley | Write: linux |
| Stuart Menefy | Maintain: yocto-manifest, meta-cheri |


Anyone can request to join a team. The CHERI Linux Strategy Working Group will decide whether to approve the request.

Contributor and Maintainer Team members are expected to:

* Review PRs and issues in a reasonable timeframe (aim for within 7 days)
* Participate in roadmap discussions
* Uphold and enforce the Code of Conduct
* Mentor contributors and help newcomers find their footing
* Communicate openly when they are unavailable for extended periods

To be considered, a contributor should generally have demonstrated:

* Sustained, quality contribution
* Good judgment in reviews
* Alignment with the project's values and direction
* Responsiveness and reliability

## Community & Support

* **Chat** — Use [the cheri-linux Slack channel](https://cheri-cpu.slack.com/messages/cheri-linux) for questions, ideas, and general conversation
* **Mailing list** — [linux-kernel@cheri-alliance.org](https://lists.cheri-alliance.org/mailman3/postorius/lists/linux-kernel.cheri-alliance.org/) for announcements

## Code of Conduct

The CHERI Linux Project and CHERI Linux Strategy Working Group follow the CHERI Alliance [Code of Conduct](https://cheri-alliance.org/code-of-conduct/). If you have questions or believe that someone is violating the code of conduct, please get in touch with the CHERI Alliance Code of Conduct team thorough the [contact page](https://cheri-alliance.org/contact/).

