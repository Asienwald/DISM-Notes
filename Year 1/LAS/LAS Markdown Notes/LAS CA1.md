---
title: 'LAS CA1'
disqus: hackmd
---

:::info
ST2412 Linux Admin & Security
:::

LAS CA1 Applied Research on Root Access Recovery Centos 7
===

<style>
img{
/*     border: 2px solid red; */
    margin-left: auto;
    margin-right: auto;
    width: 90%;
    display: block;
}
</style>


## Table of Contents

[TOC]

Overview
---
![](https://i.imgur.com/ltNRghp.png)
- root pasword of system lost
- grub menu protected by unknown password
- what we know
    - how to recover root access from system
    - BUT not applicable as grub is locked by unknown password

### Resources
- https://www.2daygeek.com/linux-reset-change-forgotten-root-password-in-rhel-7-centos-7/
    - reset root password

### Marking Scheme
![](https://i.imgur.com/Sjs9LBM.png)

Tasks
---
- document steps to resolve problem in a report
    - using pt form/screenshots
    - list assumptions made
- create demo video & upload to youtube
    - duration 5-7 minutes
- indiv reflection
    - hints
        - ![](https://i.imgur.com/PUGcSiI.png)

> Report is here
> https://drive.google.com/open?id=13PorjeFxZ-_4gFwYuKwPNWxAakyR-gd9


### Setting up VM
- root password configured as centos

#### Setting up GRUB password
- type `grub2-mkpasswd-pbkdf2` to generate password hash for "grubcentos" (our grub password)

![](https://i.imgur.com/LKHnmwj.png)
```
grub.pbkdf2.sha512.10000.2B89695729AB307897FA6E21B2E4EFB023E49E2D96519DC615D63FEAA6AF2C81B38C08D70B3295454B3ADA49F07F9773F72564F6DE9426343F74C91BAD1DB35E.B7B3639B68381B5CD48235A0CFF16EFB6716C41E40CF796ACF78464D4C83B2B1D1379B487D97ACA9B2BA8FA6EBD1F6F18E943AE5095737F134BFD3673CE36A0F
```

- edit `/etc/grub.d/40_custom` file and append `set superusers="root"` and `password_pbkdf2 root <hash>` to end of file

![](https://i.imgur.com/dHvvUOn.png)

- type `grub2-mkconfig -o /boot/grub2/grub.cfg` to refresh the grub boot config and enable the new config

![](https://i.imgur.com/xS12HXW.png)

- now the grub menu should be password protected
    - user = `root`, password = `grubcentos`

![](https://i.imgur.com/zBzF6vq.png)


### Resetting GRUB & Root password through bootable media
- since grub is password protected, we can't reset our root password through our grub menu
- reset root password by booting into rescue mode

#### Reset root password through rescue mode
- when seeing the vmware logo, press esc to go into the boot menu

![](https://i.imgur.com/cvCKPe0.png)

- insert your bootable media (centos iso file) and boot from CD-ROM drive in the boot menu

- choose `troubleshooting`

![](https://i.imgur.com/Kw8BiOl.png)

- choose rescue a centos system and press enter to enter the installation process

![](https://i.imgur.com/5fMIvfV.png)

- once greeted by this menu, choose 1 and the rescue environment will attempt to find your centos installation & mount it under `/mnt/sysimage`

![](https://i.imgur.com/MXfvj1v.png)

- press enter to get a shell

![](https://i.imgur.com/h3ump4G.png)

- type `chroot /mnt/sysimage` to get into a chroot jail so that `/mnt/sysimage` is used as the root fo the file system

![](https://i.imgur.com/wl0s7wv.png)

- type `passwd` to reset the password of the root user
    - the new password i used is "newpassword"

![](https://i.imgur.com/Zz7BS0I.png)

- by default CENTOS 7 uses SELinux in enforcing mode
    - by creating the hidden file `.autorelabel`, it will automatically perform a relabel of all files on the next boot and allows us to fix the context of the `/etc/shadow` file

![](https://i.imgur.com/DJOBDDJ.png)

- type `exit` twice to exit the chroot jail environment and reboot the system
- now you can login as root with your new password

#### Reset GRUB password with new root password
- type `grub2-mkpasswd-pbkdf2` to generate a new password hash for "grubcentos" (our new grub password)

![](https://i.imgur.com/LKHnmwj.png)
```
grub.pbkdf2.sha512.10000.2B89695729AB307897FA6E21B2E4EFB023E49E2D96519DC615D63FEAA6AF2C81B38C08D70B3295454B3ADA49F07F9773F72564F6DE9426343F74C91BAD1DB35E.B7B3639B68381B5CD48235A0CFF16EFB6716C41E40CF796ACF78464D4C83B2B1D1379B487D97ACA9B2BA8FA6EBD1F6F18E943AE5095737F134BFD3673CE36A0F
```

- make a backup of your `/etc/grub.d/40_custom` and `/boot/grub2/grub.cfg` files

- edit `/etc/grub.d/40_custom` file and append `set superusers="root"` and `password_pbkdf2 root <your password hash>` to the end of file
    - delete the entries in the 40_custom file from before

![](https://i.imgur.com/dHvvUOn.png)

- type `grub2-mkconfig -o /boot/grub2/grub.cfg` to refresh the grub boot config and enable the new config

![](https://i.imgur.com/xS12HXW.png)

- now the grub menu password should be reset to your new password
    - user = `root`, password = `<your password>`

![](https://i.imgur.com/zBzF6vq.png)


Script
---
Hello everyone I'm Kar Wei/Yuran and this video is a guide on root access recovery on CentOS 7.

So let's say you have a CentOS 7 system who's root password is lost and the GRUB menu is also protected with an unknown password.

In normal circumstances the way to reset your root password is through the GRUB menu but this isn't applicable in our current situation as the menu is locked.

Hence, we will be resetting our root password through a different method - rescue mode.


So firstly, we'll start by preparing our bootable media to boot into rescue mode.

Since we're using a VM in this demo, we can simply add a CD ROM pointing to our CentOS 7 .iso file to act as the bootable media.

__(explain how to add .iso file as CD)__

If your CentOS 7 is acting as your host OS instead of a VM, you'll have to prepare a external USB stick with the .iso file to act as the media and plug it in.

__(pan to image of USB stick)__


Once we have our bootable media, we'll have to open up our boot menu.
In vmware all we have to do is restart our vm and press esc once you see the vmware logo.
In an actual PC, we'll have to restart our pc and press a specific key (usually F12 or F10) to enter our BIOS and access our boot menu from there.

__(enter vmware boot menu)__

Over here we should be able to see a list of devices currently connected to our system. All we have to do is select the one with our bootable media which in this case is the CD-ROM Drive.

__(select CD-ROM Drive)__

choose troubleshooting and then rescue a CentOS system.

__(do above)__

Once we're in our rescue environment, select 1 and press enter to get a shell.

the rescue environment will attempt to find your CentOS installation and mount it under `/mnt/sysimage`.

__(do above)__

Next type `chroot /mnt/sysimage` to get into a chroot jail so that `/mnt/sysimage` is used as the root of the system.

Now with our new shell with root privileges, we can use the `passwd` command to reset and change our root password.

in this tutorial, we'll set our password to "centos"

__(change password)__

By default CentOS 7 uses SELinux in enforcing mode.
We'll have to create a hidden file autorelabel to perform a relabel of all files on the next boot and fix the context of the `/etc/shadow` file

__(type `touch /.autorelabel`)__

Once done, we can proceed to exit the chroot jail environment and sign into our root user with our newly set password.

__(exit and sign in as root)__

With our newly set root password, we can now also reset our GRUB menu's password.

Firstly, we'll have to generate a new password hash for our new grub password using the `grub2-mkpasswd-pbkdf2` command

In this tutorial, we'll use the password "grubcentos"

__(type command and generate password hash)__

Take note that we'll have to use this hash later on so let's save it into a text file.

__(copy & paste hash into text file in host OS)__

Next, we'll be editing our grub config files hence it's best to make backups of them in case something goes wrong.

These files are located in `/etc/grub.d/40_custom` and `/boot/grub2/grub.cfg`.
Let's create a new directory and save the files in it.

__(`mkdir backup` and copy the files into the new dir)__

to set our new password for our grub menu, we open up the `40_custom` file located in `/etc/grub.d/` and delete the previous entries.

we then append `set superusers="root"` and `password_pbkdf2 root ` followed by our password hash earlier into the file

Like this.
__(do above)__


Once that's out of the way, we'll have to refresh our grub boot configuration to use our new configuration with our new password with this command.

__(type `grub2-mkconfig -o /boot/grub2/grub.cfg` on screen)__


Now, our grub menu's password should be reset and we can access it with our new password and root as the user.

__(restart and enter grub menu with new password)__


This concludes our tutorial on resetting our root password using rescue mode and resetting our grub password.

I hope you learnt something from this because we did while making this video.

remember to like, comment and subscribe! bye!




###### tags: `LAS SEM 2` `DISM SEM 2` `School` `Notes`