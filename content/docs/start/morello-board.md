---
title: 'Getting Started with Morello Linux on Morello hardware'
date: 2026-08-19
---

This page contains some simple instructions to setup a Morello development board with everything you need to build and boot into a Morello Linux environment.

**Note:** This approach requires Morello hardware.

### Update the firmware

Remove the microSD card from the Morello board. (Press the card into the slot until it clicks, and it will spring out of the slot.) Plug the microSD card into a Linux desktop using an SD card reader (something like https://www.amazon.com/dp/B01EFPX9XA). Find the right drive by running  `lsblk` on your desktop before and after plugging in the SD card reader. Mount the microSD card, and delete any old firmware.

```
 $ sudo mount /dev/sdX1 /mnt
 $ sudo rm -rf /mnt/*
```

Get the latest version of the `board-firmware` repo on the Morello Project GitLab, and copy all files from the git repo onto the microSD card:

```
 $ git clone https://git.morello-project.org/morello/board-firmware.git
 $ cp -r board-firmware/* /mnt/

```

When the copy is done, unmount the microSD card: 

```
 $ sudo umount /mnt
```

Then unplug the SD card reader from your desktop, and re-install the microSD card in the Morello board.

## Install Morello Linux on the internal drive

Download the [latest image](https://git.morello-project.org/morello/morello-rootfs-images/-/jobs/artifacts/morello/mainline/raw/morello-soc.tar.xz?job=build-morello-rootfs-images) for the Morello SoC from the [list of images](https://git.morello-project.org/morello/morello-rootfs-images). Unpack the compressed image:

```
 $ tar -xJf morello-soc.tar.xz
```

While the Morello board is powered down, remove the internal SATA drive from the board (the default drive on a desktop Morello box is a 240GB SDD). Plug the drive into a Linux desktop computer using an external SATA to USB adapter cable (something like https://www.amazon.com/dp/B00MYU0EAU/). Find the right drive by running `lsblk` on your desktop before and after plugging in the drive.

Write the Morello Linux disk image to the drive:

```
 $ sudo cp morello-soc/morello-soc.img /dev/sdX
 $ sync
```

Reinstall the internal SATA drive in the Morello board.

## Boot the Morello board

Attach a power cable, keyboard, and monitor to the Morello board, and turn on the power. If the board doesn't choose the correct internal drive the first time you boot it (or tries to network boot or PXE boot), hold down `ESCAPE` when the boot splash screen comes up on the monitor to enter the "Boot Manager" and choose the internal drive as the boot target.

When the boot process is fininished, you'll see a login prompt. Login with user `root` and password `morello`.


## Access the Morello board over SSH

You can SSH into the Morello board as soon as it boots, since the Morello Linux image sets this up for you automatically. Look up the IP address of the Morello board on the local network by running `ifconfig` in the terminal on the monitor. Use same username `root` and password `morello`:

```
ssh root@<ip address>
```

