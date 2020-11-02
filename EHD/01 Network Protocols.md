

01 Network Protocols
===



## Table of Contents

- [01 Network Protocols](#01-network-protocols)
  * [Table of Contents](#table-of-contents)
  * [Tools](#tools)
    + [Kali Linux](#kali-linux)
    + [Wireshark](#wireshark)
    + [Nmap](#nmap)
  * [HTTP](#http)
    + [HTTP Methods](#http-methods)
    + [HTTP & HTTPS](#http---https)
  * [Protocols for Remote Access](#protocols-for-remote-access)
    + [Netstat](#netstat)
    + [Remote Desktops](#remote-desktops)
      - [Remote Desktop Software](#remote-desktop-software)
      - [Remote Desktop Services](#remote-desktop-services)
    + [File Transfer Protocol (FTP)](#file-transfer-protocol--ftp-)
    + [Telnet](#telnet)
    + [Secure Shell (SSH)](#secure-shell--ssh-)
  * [Network Protocols](#network-protocols)
    + [Address Resolution Protocol (ARP)](#address-resolution-protocol--arp-)
      - [ARP Poisoning/Spoofing](#arp-poisoning-spoofing)
    + [Domain Name System (DNS)](#domain-name-system--dns-)
      - [DNS Poisoning/Spoofing](#dns-poisoning-spoofing)
    + [Simple Network Management Protocol (SNMP)](#simple-network-management-protocol--snmp-)
    + [Ping Sweeps](#ping-sweeps)
    + [Banner Grabbing](#banner-grabbing)
  * [Summary](#summary)


Tools
---
### Kali Linux
- linux distro with many useful security software
    - Eg. wireshark, nmap etc.
- can run off LiveCD or USB
- rebuild of backtrack linux

### Wireshark
- open source packet analyser
- network traffic captured & stored for offline analysis
- displays info in packets in human-readable format

![](https://i.imgur.com/pO6K0fC.png)

- with wireshark you can
    - understand how protocols work
    - reassemble captured network traffic

### Nmap
- test if port opened, SYN packet sent to port
- if SYN/ACK packet returned, port opened
- nmap is popular tool to scan for opened ports

![](https://i.imgur.com/rjfvSgw.png)



HTTP
---
- when client requests webpage, request sent as HTTP GET method

![](https://i.imgur.com/3KILeGn.png)

- when client submits data in webform, data sent as HTTP POST method

![](https://i.imgur.com/nqdF3Kv.png)

### HTTP Methods
- GET
    - request data from web server
    - most commonly used
- POST
    - send data to web server from webform
- HEAD
    - similar to GET but returned packet only has HTTP headers with no response body
    - used for testing
- PUT
    - replace resource specified in URL
    - usually not activated 
        - not secure
- DELETE
    - delete res specified in URL
- TRACE
    - perform loopback test to res specified in URL
- OPTIONS
    - describe comm options available
    - not so good devs will usually leave this activated
        - always use this method to find info about web server
            - Eg. using apache or IIS

### HTTP & HTTPS
- HTTP
    - port 80
    - data not encrypted
- HTTPS
    - encrypt HTTP data
    - port 443


Protocols for Remote Access
---
- diff protocols for remote access
    - FTP
    - telnet
    - SSH, SCP, SFTP
    - remote desktop

### Netstat
- is command avail on windows & linux to display opened ports & current conns

### Remote Desktops
- allows comp's desktop env to be viewed/controlled remotely
- used by IT support to troubleshoot comp probs
- can be used by hackers impersonating IT support staff & getting users to allow remote desktop access
- __Remote Access Trojan (RAT)__
    - malware that allows hacker to control comp remotely

#### Remote Desktop Software
- remote desktop services (microsoft)
- teamviewer
- tightVNC
    - based on virtual network computing
- more

#### Remote Desktop Services
- microsoft's remote desktop conn
- allows users to connect remotely to windows
- tcp port 3389
- if remote desktop needed, use network lvl auth for more security

![](https://i.imgur.com/xS060Jr.png)

### File Transfer Protocol (FTP)
- protocol for copying files between systems
- FTP server runs on
    - port 21 for control conns
    - port 20 or other for data conn
- no encryption
    - all data in plaintext
- can use alts like SFTP

### Telnet
- allows user to login remotely to another system
- port 23
- old protocol - data not encrypted
- shld use alts like Secure Shell (SSH)

### Secure Shell (SSH)
- popular app for remote login
- port 22
- data encrypted across network
- SCP (Secure Copy) & SFTP (Secure FTP) work over SSH protocol to allow secured file transfers


Network Protocols
---

### Address Resolution Protocol (ARP)
- for device to send packet to another on same local network need MAC of dest
- ARP used to find MAC
- to find MAC of IP

    - ![](https://i.imgur.com/5vkba2c.png)

![](https://i.imgur.com/GreSnE8.png)

#### ARP Poisoning/Spoofing
- if atker can poison ARP table, can cause devices to send packets to him instead

- normal scenario
    - ![](https://i.imgur.com/cZhsiEz.png)

- attack scenario
    - ![](https://i.imgur.com/czw2Y59.png)

### Domain Name System (DNS)
- when browsing internet, user enters domain name
    - DNS resolves domain names to their IP addr

- DNS server/nameserver contains db that holds section of domain names mapped to IP addr

![](https://i.imgur.com/xTqjmzy.png)

#### DNS Poisoning/Spoofing
- if atker can edit DNS db or DNS cache, he can direct users to own website instead

![](https://i.imgur.com/FOveGtK.png)

- proper config of DNS can reduce risks of such atks


### Simple Network Management Protocol (SNMP)
- for remote monitoring & management of network nodes
- SNMP manager monitors set of SNMP agents installed on network nodes
    - checks perf of monitored nodes
    - makes changes in config of monitored nodes
- SNMP agent can send warning to SNMP manager of unusual situations

### Ping Sweeps
- ping sweep sends ping packets to range of IP to see which system will reply
- used to see which system is alive
- AKA ICMP sweep

### Banner Grabbing
- many services return info like ver num when client connects to it
    - a "banner"
- banner grabbing - method hackers use to find info abt running service
- usually telnet/netcat (nc) used to do banner grabbing

![](https://i.imgur.com/6sKHqx4.png)





Summary
---
![](https://i.imgur.com/nDUddmQ.png)
![](https://i.imgur.com/7NsuyVh.png)





###### tags: `EHD` `DISM` `School` `Notes`