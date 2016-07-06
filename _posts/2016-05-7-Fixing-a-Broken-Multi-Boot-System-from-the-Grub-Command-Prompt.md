---
layout: post
category: Day-to-Day Linux
title: "Fixing a Broken Multi-Boot System from the Grub Command Prompt"
tagline: ""
tags : [Grub2, Debian, Ubuntu, Windows 10, Multi Boot]
---
{% include JB/setup %}

## Overview

I use an ASUS laptop with a UEFI motherboard for the majority of my computing tasks, which until recently utilized a dual boot system hosting both Windows 10 and Ubuntu 15.04, though I almost exclusively used Ubuntu.

I recently made the decision to try Debian. After preparing a bootable ISO, I made the naive assumption that the GRUB installation performed during the installation of Ubuntu was performed in an independent manner from the Ubuntu installation, and as such that I was free to delete and reformat the existing Ubuntu partition with no consequences to the integrity of the bootloader; I assumed that after rebooting, GRUB would simply display the remaining, valid boot entries.

After deleting the existing Ubuntu partition within Windows in order to make space for the new Debian installation, I rebooted the computer, further assuming that the mistake of having not entered the UEFI manager via Shift+Restart in Windows (in order to boot from the USB) would be of little consequence, since I would likely be able to reboot into Windows should the EFI manager fail to boot from the bootable USB by default.

## Boot Failure

Follwing such discourse I witnessed the following, indicative of a boot failure:

![](http://i.imgur.com/Z28h3m5.jpg)

After selecting ok, and a few lines of text being printed to the screen in sucession so quickly that I couldn't read them, a GRUB command prompt was displayed. After using 'ls' to examine what was accessible from the prompt I observed that two disks were available: hd0; the bootable USB, and hd1; the hard disk of the laptop.

## Booting the Debian Installer from the Bootable USB

After further examination of the contents of the accessible disks, and after doing some research online, I noticed a pair of adjacent files on the bootable USB looked familiar, indeed similar to the files shown in a particular blog post [1]. I applied the follwing sequence of commands, similar to those used in the blog post:

>set root=(hd0,1)  
>linux (hd0,1)/install.amd/vmlinuz root=/dev/sd00 ro  
>initrd (hd0,1)/install.amd/initrd.gz  
>boot  

In doing so, I managed to launch the Debian installer in non-graphical mode. My assumption was that I would be able to install Debian within the space for which the installation was previously allocated, and that during the installation GRUB would be installed in a manner which would repair the apparently broken previous GRUB installation.

## Loading the GRUB Configuration File

However after installing Debian and rebooting, the issue persisted. After further examination of the disk contents, and a significant amount of time invested in reading material online, at one point after reading the contents of the grub.cfg file residing in the hard disk of the computer at the path: '(hd1,1)/EFI/ubuntu/', I realized that GRUB was simply loading another grub.cfg file from the '/boot/grub/' directory within a particular partition, which I assumed previously held the Ubuntu installation.

After making this observation I hypothesized that the Debian installation likely contained a grub.cfg file in the same location, and as such I could use the following commands, similar to those used within the previously utilized grub configuration file:

>set root=(hd1,gpt9)  
>set prefix=($root)'/boot/grub'  
>configfile $prefix/grub.cfg  

Not knowing which partition within which Debian was installed however, I applied the command sequence to numerous partitions until I was able to locate the partition within which Debian was installed, and in doing so load the configuration file produced during the Debian installation process. Once I sucessfully loaded the configuation file I was able to successfully boot into Debian and Windows.

## Sources

[1] [http://karuppuswamy.com/wordpress/2011/09/09/how-to-fix-grub-rescue-prompt-without-live-cd-for-grub2/, "How to Fix GRUB Rescue Prompt Without Live CD (For GRUB2)", 2016.](http://karuppuswamy.com/wordpress/2011/09/09/how-to-fix-grub-rescue-prompt-without-live-cd-for-grub2/) [Accessed: 30-Apr-2016].
