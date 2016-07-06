---
layout: post
category: Day-to-Day Linux
title: "Running Debian with Secure Boot Enabled"
tagline: ""
tags : [Debian, Secure Boot, EFI]
---
{% include JB/setup %}

So! This process is highly straightforward as it turns out, provided the UEFI interface of the computer being used is sufficiently usable.

This pages lists a series of approaches available when dealing with secure boot: [1].

And this one describes the process associated with installing custom keys. A thourough read is STRONGLY encouraged, and indeed this post is meant to be supplemental material to lend an air of simplicity to the process.

As, described in [2], there are X steps associated with this process:

1.
2.
...

## Header 1

...

## Header 2

...

The gist of this one is:

- Installing efitools on a neighbor Ubuntu installation
  -> Need to see if this can be done with an Ubuntu live CD
- Perform a series of commands to generate custom keys
- Create a signed copy of the Debian .efi executable
- Add the keys to EFI records using the EFI manager

## Sources

[1] http://www.rodsbooks.com/efi-bootloaders/secureboot.html
[2] http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html
[1] [http://karuppuswamy.com/wordpress/2011/09/09/how-to-fix-grub-rescue-prompt-without-live-cd-for-grub2/, "How to Fix GRUB Rescue Prompt Without Live CD (For GRUB2)", 2016.](http://karuppuswamy.com/wordpress/2011/09/09/how-to-fix-grub-rescue-prompt-without-live-cd-for-grub2/) [Accessed: 30-Apr-2016].
