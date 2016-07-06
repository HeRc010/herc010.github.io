---
layout: post
category: Day-to-Day Linux
title: "Installing Debian with an LVM using Encrypted Root and Swap Partitions"
tagline: ""
tags : [Debian, Installation, Encryption, LVM, Multi Boot]
---
{% include JB/setup %}

## Overview

Installing Debian with an encrypted LVM wherein both the root and swap partitions are encrypted can be slightly challenging when not using the default option provided in the installer, and instead using manual partitioning.

## Disclaimer

I'm not responsible for any unintended/intended damage experienced as a result of this guide, nor am I responsible for any inadequacy on the behalf of this approach to appropriately secure the contents of the resulting Debian installation; ultimately it is the responsibility of you, the reader, to ensure that your computer system (s) are appropriately secured.

## Process

Once booted into the debian installer, and after arriving at the partitioning step (guides such as [] may be used as references when performing the installation steps prior to this one), two partitions must be created:

1. A '/boot' partition
2. A 'physical partition for encryption'

Firstly, select the free space available for your installation [should probably mention, or comment on, the steps associated with allocating space beforehand, whether through windows or the installer itself --> mention the care required when doing this], provide a name for the partition if desirable and choose 100 MB (0.1 GB) for the partition size (which according to [] is a recommended size for the boot partition).
  -> If you're dual booting with Windows I strongly recommend performing the partitioning within Windows using [the name of that one tool], since I've noticed that it appears there are undisclosed restrictions on the permitted space allocated to the Windows drive (shrinking the primary Windows partition beyond a certain point is not permitted by the tool). I'm uncertain whether shrinking the partition beyond the minmum size as implicitly dictated by this tool will have severe consequences. Given that it is well known that Windows tends to play rough with neighbor OS's in multi boot systems however, I wouldn't risk it personally.

- Name the partition appropriately if desirable
- Select 'Ext4 journaling file system'
- Select mount point '/boot'

... list other requirements

[Show final image]

Secondly, select the remaining free space available for installation, name the partition appropriately if desirable and for the size of the partition provide the <b>sum</b> of the desired space required of both the swap and root partitions (for example, if a 9 GB swap partition with a 20 GB root partition is desired, enter 29 GB for the partition size).

- Name the partition appropriately if desirable
- Select 'Ext4 journaling file system'

Sticking with the recommended encryption options is recommended, although you should do the research to confirm this these options are what you want/need.

The final partition scheme should moderately resemble that shown below:

[Image]

Once the partitions have been created, select 'Configure Encrypted Volumes' in the partition manager, choose 'yes' when notified that changes to the partition table will be made.

[Show image]

When prompted with two options, to '[Something]' and 'Finish' choose finish. When prompted with... blah blah blah subsequent screens, choose things, do stuff.

Once returned to the partition manager, the configuration should resemble the following, with the newly encrypted volume displayed under '[Heading]' accordingly:

[Image]

Select 'Configure LVM', blah blah blah, 'Create Volume Group', choose the encrypted volume, create two logical volumes, one the size of the swap partition, one the size of the root partition. Upon the conclusion of the creation of the two volumes, selecting the top option to 'View LVM Summary' should render an illustration similar to the following:

[Image]

Select 'Finish'. Once returned to the partition management screen, the partition configuration should resemble the following illustration:

[Image]

Select the logical volume with space allocated for the root partition and choose the following options:

- Name the partition appropriately if desirable
- Select 'Ext4 journaling file system'
- Select mount point '/'

... list other requirements

Select 'Ok'. Once returned to the partition management screen select the logical volume with space allocated for the root partition and choose the following options:

- Name the partition appropriately if desirable
- Select 'swap area'

... list other requirements

Once returned to the partition management screen, select 'Finish'. When prompted to choose whether to commit changes to the partition table by a screen similar to the following, choose 'Commit':

[Image]

The remainder of the Debian installation process is covered in great detail by well-written guides such as [][][].

Once the installation is finished and the system is rebooted, before the login screen is shown, you will be prompted to enter the passphrase required to decrypted the encrypted volume.
  -> Earlier in the guide, comment on the criticality of the retention of this password; it cannot be recovered.

## Sources

[1] [http://karuppuswamy.com/wordpress/2011/09/09/how-to-fix-grub-rescue-prompt-without-live-cd-for-grub2/, "How to Fix GRUB Rescue Prompt Without Live CD (For GRUB2)", 2016.](http://karuppuswamy.com/wordpress/2011/09/09/how-to-fix-grub-rescue-prompt-without-live-cd-for-grub2/) [Accessed: 30-Apr-2016].
