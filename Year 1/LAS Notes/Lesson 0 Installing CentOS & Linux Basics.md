---
title: 'Lesson 0 Installing CentOS & Linux Basics'
disqus: hackmd
---

:::info
ST2412 Linux Admin & Security
:::

Lesson 0 CentOS Config & Basics
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


Basics
---
### View & Config IPv4 Settings
- ```nmcli d``` - view current devices under control by __Network Manager__
    - can be used to config ens33 interface
- ```nmtui``` - config IPv4 settings with GUI
    - can change IPv4 config to static instead of manual
    - __Note__: in etc/shadow, $6 refers to encryption method, following is salt
- to change hostname, use nmtui and go into ```etc/hosts``` and add IP & domain name of client & server to access IP via domain name of ea other

### su to another user
- ```su - root``` to change user to root
- ```ps -t pts/0``` - verify that there's 2 bash sessions running in virtual terminal device pts/0
    - 1 for student acc & other for su command
    - ![](https://i.imgur.com/UdO1A1E.png)

### Virtual Consoles
- use <kbd>CRTL</kbd> + <kbd>ALT</kbd> + <kbd>F1</kbd> to <kbd>F6</kbd> to toggle between virtual consoles & GUI

### Creating users
- use ```useradd newuser``` to add users
- ```passwd newuser``` to change their password
- ```groupadd newuser``` to create new group
- ```usermod -aG groupname newuser``` to add user to group

### File Permissions
- use ```chmod u=rw,g=r,o= /tmp/practice``` to give practice file rw permissions to owner, r to group and none to all
    - (u)ser, (g)roup, (o)ther, (a)ll


Setting Up yum repos on server
---
__Background__
- all software on linux system divided into packages to be installed/uninstalled/upgraded/queried/verified
    - linux system may connect to various online software repos to download & install these pkgs
    - common to use >1 software pkg utility type due to many packaging formats
    - CentOS uses yum utility to access & install RPM software pkg
- we will setup FTP based repos which contains rpm package files at our CentOS server
![](https://i.imgur.com/oCsLAvr.png)


### Copy RPM files from DVD to Server VM
- CentOS installation DVD contains software files (rpms)
    - go to vm > settings and connect the DVD to vm
- locate dvd in ```/run/media/root```
    - copy packages file into ```/var/ftp/ub```
        - is the public ftp dir so other comps can ftp into it
    - can use ```diff``` command to see differences between folders to ensure integrity
- eject dvd using ```umount```

### Setup yum repos
- install createrepo rpm package using rpm command in Packages dir
![](https://i.imgur.com/OgdCUV0.png)
![](https://i.imgur.com/HgU79TB.png)
- install vsftpd rpm file
    - this is to install the FTP server
- create rum repos using ```createrepo``` command
![](https://i.imgur.com/QxJbQRM.png)

### SELinux
- set all rpm files to have default SELinux security context settings
    - [Reference Link](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/selinux_users_and_administrators_guide/chap-security-enhanced_linux-selinux_contexts)
    - list current file context with ```ls -lcontext``` or ```ls -Z```
- use ```restorecon``` to set file to default context value
    - ```restorecon –R  –v  /var/ftp/pub/Packages``` to restore all rpm file in Packages folder to default SELinux context
![](https://i.imgur.com/dnQvIOp.png)
- unconfined user, object, public content - anyone can access

### Start FTP Server
- ```systemctl start vsftpd``` to start and ```systemctl enable vsftpd``` to start it on startup
- go to Firewall and change permenant config for ftp to enabled & runtime config for ftp to be disabled
    - if no work check the runtime ftp option and you should be able to connect to server through ftp ```ftp://<ip>```
![](https://i.imgur.com/MZT4GY6.png)

### Connect to yum repos from client
- view client-side yum repos definition files
    - ```ls /etc/yum.repos.d```
![](https://i.imgur.com/LQhvuei.png)
- use ```yum repolist``` to retrieve corresponding list of 'active' repos
![](https://i.imgur.com/H81q5XQ.png)
- add in packages of server as additional repo for client
    - create new file ```/etc/yum.repos.d/server.repo```
        - can be any name but must end with .repo
    - enter following text with own IP
```
[server]
name=My Yum Server
baseurl=ftp://172.16.10.88/pub/Packages
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```
- view all repos your client configured to using ```yum repolist```
    - ``` yum --disable="*" --enablerepo="server" list``` to only enable server repo
- try to install vsftpd service package from server
    - ``` yum --disablerepo="*"  --enablerepo="server"  install  vsftpd ```
    - ```yum info vsftpd``` to view info on pkg
    - ``` yum remove vsftpd``` to remove installed vsftpd package
- if want yum command to only connect to local repos, add line ```enabled=0``` to other yum repos definition lines in ```/etc/yum.repos.d```

### Which packages installed?
- on server, login as root and display current repo servers using ```yum repolist```
- connect to local yum repos by creating new file ```/etc/yum.repos.d/server.repo```
    - enter following
```
[server]
name=My Yum Server
baseurl=file:///var/ftp/pub/Packages
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```
- rerun ```yum repolist``` to check if additional local repo added correctly
- ```rpm -ga``` - list packages installed on your system
    - use ```grep``` to find specific installed packages
    - ```yum list installed | less``` - list packages installed on system from yum repos

###### tags: `LAS SEM 2` `DISM SEM 2` `School` `Notes`