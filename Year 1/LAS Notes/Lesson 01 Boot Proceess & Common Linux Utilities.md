---
title: 'Lesson 01 Boot Proceess & Common Linux Utilities'
disqus: hackmd
---

:::info
ST2412 Linux Admin & Security
:::

Lesson 01 CentOS Boot Process & Common Linux Utilities
===

<style>
img{
/*     border: 2px solid red; */
    margin-left: auto;
    margin-right: auto;
    width: 80%;
    display: block;
}
</style>


## Table of Contents

[TOC]

Root Password Recovery
---
- demo how to reset root password on CentOS system
- when on grub menu, press "e"
    - this interrupts the boot process at grub menu
- search for line that starts with `linux16`
    - append `rd.break`
        - rd = ram disk
    - this instructs bootloader to break during boot process
![](https://i.imgur.com/H0d4cZm.png)
- press `CRTL-x` to resume boot process
    - boot process will break & enter emergency mode
    - cmd provided (with root)
    - in emergency mode actually boot from ramdisk with bare minimum system files & tools
    - real root file system mounted under `/system/root`
        - can type `mount` command to verify
- to reset root passwd which is stored in 'real' root file system, 
    - remount `/sysroot` to read/write mode
    - change our root from `/` to `/sysroot`
    - commands
        - `umount /sysroot`
        - `mount /dev/mapper/centos-root /sysroot`
        - `chroot /sysroot`
    - now can use `passwd` command to reset root passwd
- to follow CentOS/Redhat convention, need to ensure `.autorelabel` file created at `/` folder
    - `touch .autorelabel`
    - to create/update timestamp of file (if alrdy existed)
- type `exit` to exit emergency mode shell
- type `init 6` to reboot system


Securing GRUB & Linux Boot Process
---
### 6 Stages of Linux Boot Process
![](https://i.imgur.com/TOZtzqm.png)
- [More Info](https://www.thegeekstuff.com/2011/02/linux-boot-process)




###### tags: `LAS SEM 2` `DISM SEM 2` `School` `Notes`