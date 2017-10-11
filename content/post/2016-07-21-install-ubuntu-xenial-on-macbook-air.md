---
title: Install Ubuntu Xenial on Macbook Air
date: 2016-07-21
author: philmikejones
categories:
  - Code
tags:
  - linux
  - mac
  - macbook air
  - os x
  - ubuntu
---

Below are simply my notes on installing Ubuntu 16.04 Xenial on a Macbook Air as I couldn't find one clear or up-to-date source.
My Macbook is a mid-2011 (4,2) so your mileage may vary if you have a different model.

NB: If you try to follow these instructions you do so at your own risk; I make no guarantees that these instructions work or even that they won't brick your Macbook.
Needless to say, make a backup of anything you need before you begin.

1. Download Ubuntu 16.04 from the Ubuntu website. You want the 64-bit version.
1. Download the binary zip version of rEFInd from: http://www.rodsbooks.com/refind/getting.html
1. Install rEFInd on your Mac. There are installation instructions in the unzipped folder, but essentially you need to: 

  a. Unzip the folder.
  a. Reboot, and at the chime hold Command + R.
  a. Open the Terminal from the Utilities menu. Navigate to where you unzipped the folder to (it's probably `/Volumes/Macintosh\ HD/Users/your-user-name/Downloads/refind-folder/`). Replace 'Macintosh HD' if necessary, and the refind folder usually has a version number.

1. Install rEFInd with `./refind-install`. You might get a warning about secure boot, but if you choose to proceed the installation should still work.
1. Restart your Mac and you should be presented with the rEFInd menu, demonstrating it worked. You should now boot back into your Mac.
1. Prepare a USB stick that's bootable for a Mac. The USB stick should be at least 4GB in size. To make it bootable, first format it as 'MS-DOS (FAT)' or ExFAT (not sure if it makes a difference).
1. Make a copy of the downloaded Ubuntu iso in case something goes wrong to save downloading it again. Open a terminal in the folder containing your Ubuntu iso.
1. Convert the .iso into an .img with: `hdiutil convert -format UDRW -o ubuntu-16.04-desktop-amd64.img ubuntu-16.04-desktop-amd64.iso`
1. Now we need to unmount (but not remove) the USB drive to be able to copy the .img onto it. 
  a. Find out your USB drive's drive identifier with `diskutil list`. It might be `/dev/disk2`, for example.
  a. Unmount it with `diskutil unmountDisk /dev/disk2` (replacing `/dev/disk2` with the actual disk identifier from step 7.1.
1. Copy the .img with `sudo dd if=ubuntu-16.04-desktop-amd64.img.dmg of=/dev/rdisk2 bs=1m` (replacing `rdisk2` with the drive identifier obtained in 7.1).
1. Eject with `diskutil eject /dev/disk2` then remove the drive.
1. Shutdown your Mac. Insert the USB drive and turn the computer back on (you don't need to hold option at the chime). The rEFInd menu should have an option to boot from USB. I suggest trying the live environment first to make sure everything boots and works correctly. You can then begin installing Ubuntu from the live environment once you're happy.
1. Begin the installation by clicking on the icon on the desktop.
1. Set up options as you wish. Once you get to the &#8216;Installation Type' option choose 'Something else'. Select the partitions based on how you want your installation (I install just Ubuntu but remove everything else). However, **do not remove** the efi partition, which is at the beginning of the drive and about 200MB. You can work with the rest of the drive, but this is what boots your Mac.

You should now be able to complete the installation and boot into Ubuntu as normal. Almost everything works out of the box, including wi-fi!
