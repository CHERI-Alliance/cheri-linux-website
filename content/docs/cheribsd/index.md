---
title: 'CheriBSD Ports'
date: 2025-03-28
weight: 3
---

Over 10,000 open source packages have already been ported to CheriBSD, and that work can be re-used with Linux on CHERI.

<!--more-->

There are a variety of ways that new contributors to the CHERI software ecosystem can add value. This is a quick list of possible starting points, with some supporting information to help dive in quickly. For now this is focused on CheriBSD, but once we have a Linux image integrated into cheribuild (hopefully no more than a few months away), it should be possible to expand the list to include Linux too. All work to port packages to CheriBSD will also benefit Linux on CHERI, because we can re-use the same patches. The CheriBSD's package building infrastructure consists of multiple components (QEMU user mode, FreeBSD ports, QEMU user mode) that had to be appropriately adapted to enable package building for CheriBSD at scale. In order to reproduce such results on a future Linux distribution for CHERI (e.g., based on Debian), similar infrastructural changes will have to be scheduled and implemented. For the time being, it would be beneficial to both CheriBSD and CHERI-enabled Linux ecosystems to work on third-party software adaptations that target all pure-capability ABIs – from CheriBSD, Morello Linux, and other Linux distributions for CHERI. It's even more beneficial when the patches can be merged into the upstream projects, so later releases of the upstream project will build on both CheriBSD and CHERI-enabled Linux distributions without any changes.

## Package building infrastructure in FreeBSD and CheriBSD

The FreeBSD source code repository, as opposed to Linux itself, consists of both userland and the kernel. The userland is referred to as the base system, and is distributed altogether with the kernel in release images.

For the third-party software, the FreeBSD project maintains a collection of around 34,000 adaptations to FreeBSD that are referred to as FreeBSD ports. Each port consists of a Makefile file that describes, using other helper make files, how to automatically fetch an archive with third-party software's source code, configure its build system (e.g., to enable X11 support), compile it, build a package with the compiled files, and install compiled files in the system. Most of such implementation details are hidden behind components in the FreeBSD ports' build system that are reused across many ports (e.g., commands to use cmake).

An end user of FreeBSD has the choice to either compile third-party software themselves or use a pre-compiled package with it. Historically, many users used ports to compile them themselves and optimise that code specifically for their platform, but today most users just use pre-compiled packages. The only exception is when a user wants to remove an unneeded feature from a package that requires many unnecessary dependencies.

In order to automate the process of building FreeBSD ports into packages, the FreeBSD project implements the build orchestration utility called Poudriere. Poudriere can bootstrap a build environment and run package builds in parallel. The progress of the builds can be observed through a website hosted by Poudriere.

For architectures that do not have CPU implementations with a very large number of cores (e.g., RISC-V, 32-bit ARM), Poudriere can build packages using the QEMU user mode on a larger arm64 or amd64 server. QEMU itself can operate in two modes: system and user. The former emulates a CPU, all devices and runs the whole operating system. The latter only emulates the CPU and translates system call calls and results for an emulated process. FreeBSD provides an in-kernel functionality that can transparently run a binary using the QEMU user mode. When the kernel is configured with the user mode, a user can run a program to be emulated as if it was a program compiled for the host itself. Poudriere can benefit from that and run an emulated build environment in which all processes are run with the QEMU user mode.

FreeBSD ports, packages, Poudriere, and the QEMU user mode have been adapted to CHERI and CheriBSD. They operate similarly in the context of CheriBSD but the infrastructure has additional limitations due to some missing software adaptations (e.g., there is no CheriABI CPython in ports yet). You can read more on the CheriBSD ports and packages in the [FreeBSD Journal](https://freebsdfoundation.org/wp-content/uploads/2023/05/CheriBSD_ports.pdf). Guidelines on how to use packages and their limitations are also described in the [Getting Started in CheriBSD](https://ctsrd-cheri.github.io/cheribsd-getting-started/packages/) guide.

## Understanding what's already been changed

Over 10,000 packages have already been ported to CheriABI (purecap). Some of the changes required to port these packages have already been merged into the upstream open source project, so in the best case a successfully ported package might not need any local changes in CheriBSD. For other ported software, CheriBSD keeps a set of patches that are applied to the upstream source code after it's fetched, or uses a CheriBSD-specific fork of the upstream project repository (usually in the CTSRD-CHERI GitHub organisation). You will also find changes in the CheriBSD repositories that modify the overall build system for ports or the build system for a particular package so it can build on CHERI/CheriBSD (for example, a change in a Makefile that disables optimisations in the form of assembly instructions that haven't been ported to CHERI). Across all of the changes, some are necessary to adapt the code to CHERI C/C++ or CHERI ISAs (and so would be equally necessary on Linux for CHERI), while others are unique to CheriBSD and the way CheriBSD organises packages and files installed in the system (for example, hybrid things live in /usr/local64 and purecap things in /usr/local, and some ports require added support to handle custom local bases).

The CheriBSD base system ([https://github.com/CTSRD-CHERI/cheribsd/](https://github.com/CTSRD-CHERI/cheribsd/)) includes a script `diff-to-upstream.sh`, which outputs a complete text diff of all the changes that CheriBSD has added to FreeBSD. A full text diff is a lot to wade through, but you can update line 7 of the script with the `–stat` (human readable) or `–numstat` (machine readable) flag so it will output a simple list of which files were modified (and how many lines were changed).

Beyond the base system, userlevel software can be found in the CheriBSD ports repository ([https://github.com/CTSRD-CHERI/cheribsd-ports/](https://github.com/CTSRD-CHERI/cheribsd-ports/)), which contains the necessary meta information to build CheriBSD packages from upstream open source projects (for example, Makefiles and patches applied before building). This repository doesn't have a script for comparing CheriBSD ports to the upstream FreeBSD ports, but you can add one yourself:

```
#!/bin/sh  
UPSTREAM_SHA_TO_COMPARE='652d0c1' 
git diff --numstat ${UPSTREAM_SHA_TO_COMPARE} HEAD
```

The "upstream SHA" is the most recent merge from FreeBSD ports into CheriBSD ports, so that will change over time. The merge history is recorded on the CheriBSD ports wiki ([https://github.com/CTSRD-CHERI/cheribsd-ports/wiki/Ports-merges\#merge-history](https://github.com/CTSRD-CHERI/cheribsd-ports/wiki/Ports-merges#merge-history)), so from the section header "merge-230804-652d0c1" the last chunk of hyphenated text (highlighted) is the SHA to compare.

Instead of the `–numstat` flag (for machine readable output), you could run the comparison script with the `–stat` flag (for human readable output), the `–shortstat` flag (for a summary count of files and lines changed), or no flag for the default full text diff output. The machine readable output is useful for passing on to other scripts/tools, for example you can grep the output for "cheribsd.patch" to get a list of all the patch files that CheriBSD applies to upstream open source projects.

### Example: annotations of changes in CheriBSD

In the CheriBSD base system (not CheriBSD ports), files that have been changed to support CHERI include annotated comment blocks (in json format) explaining what's been changed and why. The documentation file "[CHERI change annotations](https://github.com/CTSRD-CHERI/cheribsd/blob/main/tools/tools/cheri-changes/cheri-changes-json.md)" explains the format and meaning of these annotations. In [the same directory](https://github.com/CTSRD-CHERI/cheribsd/tree/main/tools/tools/cheri-changes), you'll find some scripts for working with these annotations, particularly `extract-cheri-changes.awk`.

### Example: changes for Chromium

The work to port the Chromium browser has used a label `project:chromium-cheri` on git pull requests, [so searching for that label in the CheriBSD ports repo](https://github.com/CTSRD-CHERI/cheribsd-ports/pulls?q=is%3Apr+label%3Aproject%3Achromium-cheri+) is a good way to see what changes were made to port Chromium's dependencies to CHERI.

### Example: skipped packages

There are a few hundred packages in the CheriBSD ports repo that were identified as failing to build under Purecap at some point in the past, so they were annotated to be "skipped" by the ports build system. Sometimes the annotation is in the main Makefile for the particular package, and looks like:

```
BROKEN_purecap= some text explanation
```

Other packages have a separate file added named `Makefile.purecap`, containing a single line:

```
BROKEN_purecap_failed=1
```

To identify packages with either annotation, you can grep over the CheriBSD ports repo for the string "BROKEN\_purecap". Or, if you run the script above to get a machine readable diff to upstream for CheriBSD ports, you can grep the output for files named "Makefile.purecap".

Another way to find skipped packages is to check the build logs from the [Poudriere build infrastructure for CheriBSD packages](https://poudriere.cheribsd.org/). For example, this [build log report for Morello CheriABI packages for 24.05](https://poudriere.cheribsd.org/hosts/freebsd-arm64/build.html?mastername=aarch64c-24_05-24_05-cheriabi&build=2024-06-18_07h29m08s) shows a complete list of which packages built successfully, which failed with an error, and which were skipped or ignored.

## Testing packages that have already been ported

The \~10,000 packages that have been successfully ported to CheriABI (purecap) are known to successfully build. The packages have also generally had some verification that they are able to run, but they have not been verified with their own full test suite and there is no CI infrastructure running to continuously test the packages. (You can read more about this in: [Maturity of CheriABI packages](https://ctsrd-cheri.github.io/cheribsd-getting-started/packages/limitations.html#maturity-of-cheriabi-packages).)

So, one valuable area of work is to run the full test suite on packages that have already been ported and report (or fix) any issues you find. The CheriBSD ports repo inherits the infrastructure to run test suites from FreeBSD ports, and many ports (not all) have implemented this feature. For those that do implement it, you can simply run `make test` in the port directory for the project.

Report any issues you find in the [CheriBSD ports issue tracker](https://github.com/CTSRD-CHERI/cheribsd-ports/issues). You will also find issues that others have reported there.

The CheriBSD ports wiki has a short [list of packages that are currently most actively maintained](https://github.com/CTSRD-CHERI/cheribsd-ports/wiki/Ports-merges#cheriabi) (i.e. "stable"), which are a good place to start testing since you'll find the fewest  issues. Some of those packages no longer require any code changes for CHERI, since their changes have already been merged upstream (so there is no CHERI-specific patch in CheriBSD ports to show what changes were applied to allow them to successfully compile). To get a complete list of all packages that have been ported, you can browse the pre-built binary CheriBSD package list at [https://pkg.cheribsd.org/](https://pkg.cheribsd.org/). Currently, CheriBSD 24.05 is the most recent release, so the list of [Morello CheriABI packages for 24.05](https://pkg.cheribsd.org/CheriBSD:20240617:aarch64c.html) is the best list of what successfully builds on Morello (purecap).

NOTE: CheriBSD developers specifically mentioned nginx as a package that's in good shape and would benefit from more extensive testing. The [short list of most "stable" packages](https://github.com/CTSRD-CHERI/cheribsd-ports/wiki/Ports-merges#cheriabi) are also good targets for regular testing.

## Improving packages that have already been ported

Many packages that have already been ported to CheriBSD need maintenance, refinement, and updates. These kinds of improvements are often an easier starter task than porting a new package, and are an important part of the ongoing porting work. Running a package's full test suite is one good way to identify work that needs to be done. These are a few more good ways to identify needed improvements:

* Check the [CheriBSD ports issue tracker](https://github.com/CTSRD-CHERI/cheribsd-ports/issues) for reported problems, some will be easy fixes.  
* Try using the package in "real world" examples. Even relatively simple examples can sometimes quickly find odd runtime behavior that isn't exposed by the test suite.  
* Try running common benchmark suites that use the ported software. (This will be harder at first, since the benchmarks may depend on software that hasn't been ported yet, but it will be more possible in the future.)

NOTE: CheriBSD developers specifically mentioned Postgresql, abseil library, and grpc as packages that have been ported but would benefit from cleaning, updating, and rebasing on upstream.

## Merging patches into upstream open source projects

The patch file that CheriBSD ports applies to an upstream open source project before building is named "cheribsd.patch". If you run the script above to get a machine readable diff to upstream for CheriBSD ports, you can grep the output for files named "cheribsd.patch" to identify all the packages that have patch files (currently, there are only 44 of them). Some of these patches might have already been merged into the upstream open source project, but for the ones that haven't been merged upstream yet, it's worth exploring whether they can be merged. This isn't only a technical question of whether it's possible to merge the changes, it's also partly a question of whether the upstream project will be willing to accept the changes. Any upstreaming efforts should be reviewed within the CHERI ecosystem first to make sure that the upstream project receives a patch that is correctly implemented and can be maintained over time (e.g., that CHERI LLVM will correctly compile in the future).

All changes to CheriBSD ports are captured in the [CheriBSD ports repo](https://github.com/CTSRD-CHERI/cheribsd-ports) (for example, as Makefile changes or as a "cheribsd.patch" file). But, to simplify the development workflow, the same changes may also be captured in a fork of the upstream open source project, so it's worth checking [https://github.com/CTSRD-CHERI/](https://github.com/CTSRD-CHERI/) to see whether there's already a development fork of the upstream project. These development forks are used to rebase the CHERI changes on a new version of the upstream open source project, and generate an updated patch file to add to the CheriBSD ports repo.

## Porting new packages

The most open-ended task in this guide is porting new software to CheriBSD. Since CheriBSD ports currently successfully builds about a third of the total packages in FreeBSD ports, that leaves \~20,000 packages to choose from when you're deciding what to port (and even more options if you're considering other open source software that hasn't been ported to FreeBSD yet).

Many of the packages that have already been ported are for desktop software, because a working desktop was a major goal of the CHERI project. (Again, see the report "[Assessing the Viability of an OpenSource CHERI Desktop Software Ecosystem](https://www.capabilitieslimited.co.uk/_files/ugd/f4d681_e0f23245dace466297f20a0dbd22d371.pdf)".) But, a desktop certainly isn't the only viable target for CHERI, and you might be more interested in a server deployment, embedded IoT, or something else entirely. So, before diving into porting specific packages, it's worth taking a step back to think about the set of open source software that's likely to be most important or frequently used for your domain. Then also consider the dependencies necessary to build and use that software.

Once you've decided what packages you want to port, the work is basically the same as improving packages that have already been ported, just more of the same. Try building the source code, running the test suite, and using the package as intended, then fix the errors or failures that you find. For many packages, this is a relatively straightforward process, but it can get complicated when the source code has done "interesting" things with pointers. The [CHERI C/C++ Programming Guide](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-947.pdf) provides a good overview of the kinds of source code changes needed for porting to CHERI, and an explanation of why they're needed. It can also be helpful to look at the changes that were already made to other packages. There has been substantial work over the years on tools to assist with porting to CHERI, which can be helpful, though there isn't a single comprehensive tool that will handle all cases (for a recent quick overview of several of these tools, see [Static Analysis for Transitioning to CHERI C/C++](https://dl.acm.org/doi/10.1145/3652588.3663323)).
