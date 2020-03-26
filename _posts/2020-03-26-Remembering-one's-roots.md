---
layout: page
title:  "The apparent 'fallacy' of the root Root password"
author: spandan
categories: [ Linux, tutorial ]
tags: [linux, grub]
description: "Some things are just now worth remembering. But forgetting some others cost us!"
featured: false
hidden: false
layout: post
image: assets/images/grb.png
comments: false
---

In all our installed Linux systems we always have a root user. A user that can acces any file, edit anything, execute anything (ie. has rwx access to anything) on your system. There have been several times when this user has saved us. Forgot the user password? Login as root and change it. Need to access /root , switch to the root user and get it done! Some people, typically pen-testers (beginners and intermediates) just have that one root user or mostly use that one root user. 

My point? A lot revolves around being able to access the root user : from troubleshooting for some people to day to day work for few. There are several cases though where we might not be able to login as root. All complications aside, let's take the most basic catastrophe, 

### YOU FORGOT THE ROOT PASSWORD!
Sad!! Typically you would saya that it this is one reason why one bust keep backups.

However, there are ways to overcome this and gain passwordless root access to your Linux System. The first one is quite simple.

#### Boot the LiveCD open up the terminal and mount the root partition of your main system.
``` 
# mkdir mnt
# mount /dev/sdX mnt
```
1.  Use the command
```passwd --root MOUNT_POINT USER_NAME ``` command to set the new password (you won't be prompted for an old one). Replace USER_NAME with root for altering the root password.
2.  Unmount the root partition.
3.  Reboot, and enter your new password. If you can't remember it, go to step 1.


That said, you may not have a live linux usb with you or you may not have access to the internet or another machine to go and get the iso and flash the usb.

So, in most of the cases you are using the GRUB bootloader which shows up at boot time. 

1.  Select the appropriate boot entry in the GRUB menu and press e to edit the line.
2.  Select the kernel line and press e again to edit it.(the line show in the first figure)
3.  Append **init=/bin/bash** at the end of line.
4.  Press **Ctrl-X** to boot (this change is only temporary and will not be saved to your menu.lst). After booting you will be at the bash prompt.
5.  Your root file system is mounted as readonly now, so remount it as read/write 
**```# mount -n -o remount,rw /```** .
6.  Use the passwd command to create a new root password.
7.  Reboot by typing ```# reboot -f``` and do not lose your password again!

Why does this work? To understand this you must understand init systems in general. Go over and read <a href="https://spandanji.github.io/the-systemd-controversy/">this</a>! Now you probably understand. **init=** mentions the init system. Now, that is the first process to launch. **init=/bin/bash** fires up the terminal just after the partitions have been mounted and no process has been initiated yet and you have root access. 

While this is intended as a feature, it makes some of us paranoid of the odd friend who wants to mess up our system for fun.
So, you can set a password on GRUB, but even then they can use the bios to load a live usb and follow method 1. The fullproof method would be to set a bios password and mind you, **DO NOT FORGET IT!!!**
