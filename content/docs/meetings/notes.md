# Linux Strategy Meeting Notes

### 21 May 2025

* Q: Is there at 6.14 branch of the Codasip Linux Kernel? A: Still cleaning up the 6.10 branch first, then will do the update to 6.14.  
* CHERI C Examples repository: [https://github.com/CTSRD-CHERI/cheri-c-examples](https://github.com/CTSRD-CHERI/cheri-c-examples) with discussion in the [\#cheri-c-examples](https://cheri-cpu.slack.com/archives/C08NKQB7D4K) channel in the public CHERI-CPU Slack.  
* Q: How to publish updates to the website? A: Commit the update, and Carl will launch the changes (not handed over to CHERI Alliance sysadmin yet).  
* Future topics: temporal safety on RISC-V CheriBSD ports (Alfredo, end of June or early July), MIT Lincoln Lab (Derrick, 2+ months), Yocto (Codasip after released, see if Good Penguin will do a deep dive on theirs), bpf, aio (Christian Ehrhardt), graphics, ioctl, compat, testing, ltp, plan to increase coverage, principles, performance improvements (benchmarking/optimization).  
* Ongoing action items:  
  * Release CHERI Linux strategy doc  
  * Publish collaboration guidelines on website  
  * Publish a page with meeting schedule/information on website  
  * Publish these meeting notes on website

### 7 May 2025

* Christian presented a deep dive on the [Codasip Linux Kernel work](deepdive/2025-05-07_Christian_Ehrhardt_CHERI_Linux_Kernel_work.pdf).

### 23 Apr 2025

* The [CHERI Alliance Linux Kernel repo](https://github.com/CHERI-Alliance/linux/tree/codasip-cheri-riscv) is now public on GitHub. This is Codasip’s work combining the Morello Linux patches with their own patches, on Linux Kernel version 6.10 as a base.  
* Next step will be to update to Linux Kernel version 6.14, with a cleanly rebased history.  
* Discussion of setting up CI for the CHERI Alliance repos related to Linux. Currently, Codasip uses GitLab internally and Cambridge uses Jenkins. Explore using GitHub’s built-in CI. Initially target QEMU, but eventually also target Codasip’s cores, Tooba, and CVA6.

### 9 Apr 2025

* Carl presented Linux status update talk on [Porting Linux to CHERI](deepdive/2025-04-09_Carl_Shaw_Porting_Linux_to_CHERI.pdf) (repeat from [CHERI Blossoms](https://cheri-alliance.org/events/cheri-blossoms-conference-apr-2025/) conference).

### 26 Mar 2025

* musl \- doesn't seem to be one in CHERI Alliance, would be good to get it released  
* When Morello tried to get some graphics working in purecap, Morello in purecap means you cannot use TLS in any purecap libraries. For any real porting needs to be addressed first. Has Codasip already done this?  
* Reasonable expectations for malloc and free, could go in the CHERI C/C++ Programming Guide.  
* Still hoping to get a walkthrough of the Codasip Kernel patches, choices they made, and things we know are still missing.  
* Portfolio of different potential targets:  
  * Desktop workstation (requires a very large software stack, but a lot of that is not FreeBSD-specific, so established work is useful there)  
  * Server stack (nginx, haven't done mysql)  
  * Most of the gaps are currently in the Linux kernel, the low level bits that enable memory safety and temporal safety  
  * Would be good to try out the things that are already ported to FreeBSD on Linux, including private patches that can't be upstreamed.  
* Move toward a KDE demo, a complete development stack that people can target. That's what people experimenting with CHERIbsd frequently asked "when can we get a real idea". A list of targets in cheribuild, but cross-compiling kde will likely be faster than native compiling in a VM. KDE cross-compile targets exist, but haven't been tested in a while. But, at least the cross-compile infrastructure is there.  
* QEMU userlevel support for CHERI.  
* Can debian image building do cross-compile using QEMU?  
* What are the interventions we can make as early as possible, to enable others to do work?  
* Codasip in 18 months may have chips, but in order, single pipeline, etc.  
* Draw out a roadmap for CHERI Linux as a distro.  
* Release the CHERI Linux Roadmap. Either a wiki or mdbook. Check with cheri alliance for a repo. Get permission from existing contributors.

### 12 Mar 2025  
### 26 Feb 2025

* Historically CTSRD QEMU, and CheriBSD, have been making merge commits when they update to a new upstream version. Here's the work in progress update merge for QEMU 6.2: [https://github.com/CTSRD-CHERI/qemu/pull/264](https://github.com/CTSRD-CHERI/qemu/pull/264)  
  * Pros: This preserves the upstream history and the CHERI development history without rebasing (so the SHAs are all the same, and you avoid all the problems of multiple collaborators working on a mainline that's constantly rebased).  
  * Cons: The merge commit approach works best when you're updating regularly from upstream, otherwise you can end up with a large and complex merge commit.  
* Morello was rebasing all their patches on each new upstream version, but was only updating every third release of the upstream Linux Kernel.  
* Codasip also rebased all the Morello patches on   
* Generally agreed on one of two paths:  
  * Option A: Start with clean Linux kernel v6.10 with full history, apply Morello patches on top, and then a cleaned up set of Codasip patches on top of that  
  * Option B: Start with clean Linux kernel v6.14 with full history, apply Morello patches on top, and then a cleaned up set of Codasip patches on top of that  
* Carl is going to do an assessment of the changes between v6.10 and v6.14, to help decide which of the two options will be the most reasonable.  
* Compat accelerated development, because you can run entire existing applications, and also check that you didn't break anything.)  
* Morello merged 5 patches to support netfilter on hybrid kernel (fixes problem when kernel and userspace pointers aren't the same size)  
* Carl will make Allison an admin on the CHERI Alliance Linux Kernel mailing list.  
* Ongoing work on the CHERI C/C++ Programming Guide: https://github.com/CTSRD-CHERI/cheri-c-programming  
* Future topics: yocto, bpf, aio (Christian Ehrhardt), graphics, ioctl, compat, testing, ltp, plan to increase coverage

### 12 Feb 2025

* Discussion of Morello and Codasip versions of the Linux Kernel, and paths toward convergence.

### 29 Jan 2025

* Codasip has a binary userspace image they can release.  
* Yocto build system still coming.  
* Codasip is working on aligning with the latest RISC-V profiles.  
* Future topics: collaboration guidelines, deep dive on Yocto.


### 15 Jan 2025

* Yocto build system is coming.  
* Have some Codasip boards to try out the new Linux branch. Should be able to give a bitstream for Codasip boards next week.  
* Have run benchmarks, but limited by lacking things like strcopy/memcopy.  
* Request to record the deep dive sessions.  
* Would be helpful to have a deep dive session on CHERI design principles and user expectations.

### 18 Dec 2024

* Vincenzo and Kevin gave deep dive presentations on the [Morello Linux project](deepdive/2024-12-18_Vincenzo_Frascino_Morello_Technical_Intro.pdf), and the [Morello Linux Kernel](deepdive/2024-12-18_Kevin_Brodsky_Morello_Linux_kernel_overview.pdf) – the choices they made, what they accomplished, lessons learned, and thoughts on future development for Linux on CHERI.

### 4 Dec 2024

* Website has been launched: [https://cheri-linux.org/](https://cheri-linux.org/)  
  * Ask Carl about making the website repo public.  
* Carl is working on setting up mailing lists.  
* Question: Could CheriBSD tests be abstracted to other OS and systems \[after the call, Robert suggests that cheribsdtest could become something like cheriabitest or cheriposixtest, hosted under CHERI Alliance\]  
  * What tests has Morello been running on Linux?  
  * Seemed that Codasip wanted to do some work, but anyone could work on that.  
  * Within CheriBSD, a set of binaries you can build  
  * Morello, main test were LTP, not the full syscall suite, there were exceptions, have some separate tests too, specific to purecap (self-contained, no libc)  
  * [https://git.morello-project.org/morello/morello-linux-ltp](https://git.morello-project.org/morello/morello-linux-ltp)   
  * [https://git.morello-project.org/morello/kernel/linux/-/tree/morello/master/tools/testing/selftests/arm64/morello](https://git.morello-project.org/morello/kernel/linux/-/tree/morello/master/tools/testing/selftests/arm64/morello)  
* Allison proposes starting deep-dive sessions and intro calls on topics for Linux on CHERI:  
  * Alfredo volunteers to do a session on CHERI QEMU, and another on CheriBSD purecap kernel.  
  * Carl can do one on Codasip’s Linux repo.  
  * Kevin and Vincenzo can do one on Morello Linux (What obstacles did they encounter? Plan was to finish the CHERI ABI first, and then do a purecap kernel. CHERI ABI isn't finished yet.)  
* Pull initial draft of contribution guidelines from Morello slides: [https://git.morello-project.org/morello/kernel/linux/-/wikis/res/Linux\_on\_Morello\_Contribution\_Process.pdf](https://git.morello-project.org/morello/kernel/linux/-/wikis/res/Linux_on_Morello_Contribution_Process.pdf)   
* Do we want to add a linux-roadmap repo, for the roadmap document and tracking issues/epics for who's working on what?  
* Action items  
  * Merge website cleanup branch  
  * Add a page to the website with meeting/schedule information

### 20 Nov 2024

* Carl set up a new repo cheri-linux-website on CHERI Alliance for the cheri-linux.org website, initially based on the Morello website.  
* Alfredo has continued working on CHERI QEMU (Cambridge/Codasip).  
* Continuing work on Codasip’s Linux Kernel, not yet up on CHERI Alliance GitHub.

### 6 Nov 2024

* Set the cadence of meetings to every other week, at the same time.  
* Codasip is nearly ready to push their Linux Kernel repo to the CHERI Alliance org on GitHub.  
  * Codasip kernel is purecap, cherry-picked patches from Morello kernel to a new baseline.  
* Alfredo is looking into Morello support in Codasip’s QEMU.  
* Carl is working on setting up a CHERI Alliance mailing list for Linux work.  
* Discussion of contribution workflows: Morello used mailing list for patch reviews (like the upstream linux and glibc). Most existing CHERI-related software projects are using git pull requests. General consensus is to accept both.  
* Decision to use Hugo for cheri-linux.org website, model it on linux.morello-project.org.  
* Do we want to use CHERI Alliance wiki (BookStack) or Next Cloud?

### 30 Oct 2024

* Add more participants from other organizations.  
* Analyze the differences between Morello Linux and Codasip’s work on Linux, and the scope of merging.  
  * Codasip includes most of Morello’s Linux patches.  
  * Codasip LLVM (version 17\) is derived from Cambridge LLVM (version 16). End goal is to merge forks of LLVM into one CHERI Alliance repo.  
  * Codasip QEMU has Morello hardware emulation in it, but not tested.  
  * Codasip doesn’t have virtualization yet, but have some work on it.  
  * Codasip hasn’t looked at subobject bounds yet, but may be easier on Linux than it was on BSD.  
* Action items:  
  * Collect GitHub usernames for (currently private) access to Linux Kernel repo at CHERI Alliance.  
  * Setup \#cheri-linux channel on public CHERI-CPU Slack.  
  * Publish CHERI Linux Roadmap.  
  * Setup cheri-linux.org website.

### 16 Oct 2024

* Discussions on roadmap and the scope of merging multiple CHERI-related Linux forks into one unified set of repos.

### 9 Oct 2024

* Discussions on roadmap and the scope of merging multiple CHERI-related Linux forks into one unified set of repos.

### 2 Oct 2024

* Second meeting on CHERI Linux Strategy.  
* Check-in on status of ARM Morello port of Linux.  
* Decision to repeat strategy calls weekly for the first few weeks.

### 30 Sept 2024

* First meeting on CHERI Linux Strategy.  
* Check-in on status of Codasip port of Linux.

### 21 Apr 2024

* First draft of CHERI Linux Roadmap document shared for collaborative editing.

### 22 Feb 2024

* Strategy meeting, plan to draft CHERI Linux Roadmap document
