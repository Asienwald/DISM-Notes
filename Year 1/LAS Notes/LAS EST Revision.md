---
title: 'EST Revision'
disqus: hackmd
---

:::info
ST2412 Linux Admin & Security
:::

LAS EST Revision
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


General
---
- set date and time
    - `timedatectl set-time [YYYY-MM-DD]`
    - https://www.thegeekdiary.com/centos-rhel-7-how-to-set-datetime-ntp-and-timezone-using-timedatectl/
- set hostname
    - ` hostnamectl set-hostname your-new-hostname`
    - or `/etc/hosts`
- create user passwd
    - `passwd`
    - prac 08?
- create dir, grp set perms
    - `mkdir`, `chgrp`, `chmod`



Samba
---
- config samba server
    - config file `/etc/samba/smb.conf`
```
 [myshare]  
comment = My Samba Share for peter , paul and mary
path = /samba_share
guest ok = yes
browsable = yes
write list = peter mary
```
- auto start samba
- create sam share dir
- set up operational samba share
- config `/etc/samba/smb.conf`
- access control
    - auth browsable, allow read/write perm or certain users



DNS
---
- prepare set template files for


###  DNS config file `/etc/named.conf` 

![](https://i.imgur.com/nvheZXA.png)
![](https://i.imgur.com/FES9JGp.png)

#### Add forward lookup zone
- append to named.conf
```
zone "las.org" IN {
    type master;
    file "las.org.zone";
};
```

#### Add reverse lookup zone
```
zone "108.16.172.in-addr.arpa" IN {
 type master;
 file "172.16.108.zone";
};
```
#### Allow zone transfer
- add to named.conf `allow-transfer { 172.16.108.199; }`


### Forward lookup zone `/var/named/xxx.zone`
#### For zone `las.org`
```
$TTL 86400
las.org.    IN SOA server root (
                42    ; serial
                3H    ; refresh
                15M   ; retry
                1W    ; expiry
                1D )  ; minimum
las.org.    IN NS server

server    IN A 172.16.108.88
client    IN A 172.16.108.128
testpc    IN A 172.16.108.99
```
### Reverse lookup zone `/var/named/yyy.zone`
```
$TTL	86400
@	IN SOA server.las.org. root.server.las.org. (
			42	; serial
			28800	; refresh
			14400	; retry
			3600000	; expiry
			86400)	; minimum
	IN NS	server.las.org.

128	IN PTR	client.las.org.
88	IN PTR	server.las.org.
99	IN PTR	testpc.las.org.
```

- dns query
    - forward - use URL & resolve it to IP
    - reverse - use IP & resolve to hostname (rmb fullstop)
- understand `/etc/resolv.conf` (nameserver) & `/etc/NetworkManager/NetworkManager.conf` (dns) if local dns required
    - change nameserver in resolv to server
    - change `dns=none` under `[main]` in networkmanager.conf
- if cannot start service, chances are config file has prob



System Monitoring/Log analysis
---
- config `/etc/rsyslog.conf`
    - config what lvl of logs and go where

- understand logger cmd
    - by default logger writes to `/var/log/message`
- capture required info on log
    - for diff services, know which log files to use & what info to retrieve
- search required info on system
    - Eg. files/folders
- perform remote logging
    - need understand how to config rsyslogd to send logs & accept incoming logs
- understand how to use AIDE (Advanced Intrusion Detection Environment)
    - understanding settings in `/etc/aide.conf` & how to config

### Security Levels

![](https://i.imgur.com/xSJH2Oq.png)

### Addtional things that prac 07 has
- finding files based on conditions
- get usage stats
- set process limits




Remote access control
---
- `/lib64/security/pam_*.so` 
    - * = security modules
- config of pam_permit (security module) for passwd access
    - how to config pam_permit for `/etc/pam.d/login`
    - `/etc/pam.d/gdm-password` for host GUI config files
- config pam_time (security module) for `/etc/pam.d/vsftpd` for ftp in `/etc/security/time.conf`
- Eg. SSH config for user auth `/etc/pam.d/sshd` & `/etc/security/time.conf`

### Additional things that might be utterly useless
- /etc/nsswitch.conf - control whr stuff like passwords and groups are read from
- allocating admin tasks to norm users with sudo



Firewall
---
- config firewall & firewalld
- firewall rules



Web Server
---
- general config
- SSL for web servers


<hr>


Apache Web Server
---
- lecture 02
- root at `/var/www/html/`
- main config file `/etc/httpd/conf/httpd.conf`
- log files
    - `/var/log/httpd/access_log`
    - `/var/log/httpd/error_log`

### Enable server status
- in config file
```
<Location /server-status>
  SetHandler server-status
  Order allow,deny
  Allow from all
</Location>
```
- enables everyone to access & view server status at `http://localhost/server-status`

### Containers
- edit config file and add Directory for books
- OR create new file `/etc/httpd/conf.d/books.conf`
    - all conf files in conf.d will be processed when server started

```
<Directory /var/www/html/books>
    Options -Indexes
</Directory>
```
- this only prevents dir listing

### Access Control
```
<Directory /var/www/html/books>
    Options -Indexes
    Require all denied
    Require ip 172.16.108.128 172.16.108.88
</Directory>
```
- only client can access

### Securing using SSL
- `yum install mod_ssl`
    - ssl module will gen default pair of priv key & cert
        - priv key `/etc/pki/tls/private/localhost.key`
        - cert `/etc/pki/tls/certs/localhost.crt`
- edit `/etc/httpd/conf.d/ssl.conf` and make sure `SSLCertificateFile` and `SSLCertificateKeyFile` pointing to right locations

### Named based Virtual Host
- in `/etc/hosts` resolve hostnames to your IP
- create dir `/var/www/flowers` and `/var/www/fruits` and make index.html for both
- in `/etc/httpd/conf.d/flowers.conf` or fruits wtv

```
<VirtualHost your_server_ip:80>
    ServerName www.flowers.com
    DocumentRoot /var/www/flowers
    ErrorLog /var/log/httpd/flowers-error_log
    CustomLog /var/log/httpd/flowers-access_log combined
</VirtualHost>
```

### User Authentication
- acc system diff from linux users
- use `htpassword` to maintain user accs

![](https://i.imgur.com/FwImG0v.png)

- create file `/var/www/flowers/.htaccess` and add

```
AuthType basic
AuthName "Flowers Website"
AuthUserFile /etc/httpd/conf/flowers-users
require user bob alice
```
- only Bob and Alice can login

- append to `flowers.conf`

```
<Directory /var/www/flowers>
    AllowOverride AuthConfig
</Directory>
```

### Squid Proxy Server
- yum install squid
- edit config file `/etc/squid/squid.conf`
- create access control list for my subnet
    - look for lines with acl
    - add line `acl LAS_net src 172.16.108.0/24`
- create http_access for LAS_net
    - look for # INSERT YOUR OWN RULE part
    - add line `http_access allow LAS_net`
    - comment out the http_access for localnet
- set visible_hostname to my hostname
    - `visible_hostname server.example.com`
- start squid service and allow on firewall
- check error msgs at `/var/log/messages`
- config firefox to use squid proxy
    - go preferences > network proxy > settings
    - connections > settings > manual proxy config
    - enter server IP and port 3128 (squid port)
        - set for all protocols

![](https://i.imgur.com/0lNkf6v.png)

- see lecture 2 on how to block domains etc


Firewall - Lecture 04
---
- zone files in `/etc/firewalld/zones/public.xml`
- logging info in `/var/log/messages`

### Reverse Proxy
- ip masquerading - outgoing packets modified to have same src ip as client/target NIC
- proxy port forward to target server

### Control outgoing traffic
- need to use direct interface in firewalld





###### tags: `LAS SEM 2` `DISM SEM 2` `School` `Notes`