---
layout: page
title:  "Systemd... Why? Why not? Runit ????"
author: spandan
categories: [ Jekyll, tutorial ]
tags: [red, yellow]
description: "All that bloat ain't evil -> All that minimal aint tough!"
featured: true
hidden: false
layout: post
image: assets/images/sys.png
comments: false
---
The Linux world has changed rapidly in the past few years. It has become beginner friendly with proper hardware support requiring little or no technical knowledge to get up and running. There are several Linux (more accurately GNU/Linux) distributions out there Debian, Fedora , Arch Linux, Solus, Clear OS, Gentoo and many more. One thing that most of these distros have in common is *Systemd* (Gentoo primarily supports and encourages OpenRC but has systemd profiles as well). My 11 years of linux usage has taught me to both respect and hate systemd and today hopefully I can convince you of the same. While I myself am not a big fan of systemd I will try to (If I can) be as objective as possible so as to not enforce an opinion on you. 

To love or hate something we must understand what it is. Systemd is an **init** system. And now coming to the basic question whose answer shall shape the approach we take to come to the controversy that systemd is.

**What is an init system? What is is supposed to do?**

Let us walk through how our machine would boot. The boot process starts with the BIOS (Basic Input / Output System) which looks at the bootable disks and attempts to open up a bootable hard disk. This is usually a bootloader which gives us a menu of chices regarding what to boot. A popular bootloader is **grub**, The booloader would then look for the Linux kernel selected (happy to see I am not considering a Windows boot as an option XD). Right after the kernel loads and the driver loading scripts are executed, the init system is started. As the name suggests it initiates and runs a bunch of services as requested by the user. Eg: It may run a service that enables ssh access to the system. The handling of these services is the task of the init system.

Usually this init system is run as the first process and is hence PID 1 of the system. In the older days, Linux used to use SysVInit as the init system before systemd came along. It made service management extremely simple. I am not going to list the commands here. Fire up your terminal emulator of choice and run the following to just begin to know how much you use systemd without actually knowing (In case you still use a distro that sets a lot of things up for you)
```
$ man systemctl
$ man journalctl
```

![Systemd Components](_posts/linux/systemd/Systemd-components.png)

Systemd is on many modern hardware considerably faster than SysVinit and does a lot more. It has its own power management scripts, an excellent binary logging system and many more features. It does all that an **init** system must do and more. It is basically the paradise for someone who does not want to worry about much and get going with his/her workflow. There are also scripts to anlalyze your boot time and do in something called a critical-chain, all of which you will find in the man pages.

While we are in the *heaven* that systemd is, we have maybe gone a bit astray as to what we, the Linux community represent. We represent respect for opinions of the people and have always encouraged the ability of people to choose.

With all these features (jargon), Systemd is no longer just an init system. It does a lot of things for you and if you are a minimalist like me, it does way too much than it should. For a hardcore minimalist, **Systemd is bloat**. I would just like to clarify here that I like what systemd does for someone who does not care what the init does and just wants everything to work while focussing on one's respective project or other (lesser crazy) aspects of life.

![Systemd Logs](_posts/linux/systemd/logs.png)

There are two very popular alternatives : Gentoo's OpenRC and Void's runit. Void's runit is my personal favourite and I'll go on and talk about it. By definition, unit is a suite of tools which provides an init (PID 1) as well as daemontools-compatible process supervision framework, along with utilites which streamline creation and maintenance of services. In other words, its just an init system. It maintains two folders for services. In one folder all the services are stored and in the other the enabled services should have a symlink to the respective services in the first folder. The location of these folders may vary from distro to distro however, I'll stick to the mainstream here and go on to describe it the way Void linux has made it.

To get a list of all the services installed one may check the contents of the folder in which they are stored (here: **/etc/sv**).
In case of another distro like artix linux, its there in **/etc/runit/sv**

```
$ ls /etc/sv
```

![Screenshot](_posts/linux/systemd/Screenshot_2019-08-13_22-57-29.png)

The enabled services are stored as symlinks in **/var/service (/run/runit/service for atrix linux)**.
Eg: To enable a service,

```
$ ln -s /etc/runit/sv/service_name /run/runit/service/
```

To disable a service in the current runlevel, remove the symlink to its service directory from the directory containing the symlinks:

```
$ rm /var/service/service_name
```

The service is then enabled as well as started. Otherwise starting and stopping services are quite easy.
To start, stop or restart a service, run:

```
$ sv up service_name
$ sv down service_name
$ sv restart service_name
```

To get the current status of a service, run:

```
$ sv status service_name
```

To get the current status of all enabled services, run:

```
$ sv status /var/service/*
```

To learn more about the runit commands like runsvdir, runsvschdir etc, please refer to the official documentation of runit : http://smarden.org/runit/

To wrap it up, Systemd does a great job at what it aims to achieve but if you,like me do not want an init system that also takes care of date-time stuff XD (timedatectl), it is imperative that we try something like runit. runit is also known for its extremely fast boot times. This difference is more notable on a HDD harddisk where I even got 10s faster boots on a 2GB RAM machine.
