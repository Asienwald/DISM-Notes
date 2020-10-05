

Lecture 03B Network Protocols
===




## Table of Contents

- [Lecture 03B Network Protocols](#lecture-03b-network-protocols)
  * [Telnet](#telnet)
  * [Secure Shell (SSH)](#secure-shell--ssh-)
  * [Email Protocols](#email-protocols)
    + [Simple Mail Transport Protocol (SMTP)](#simple-mail-transport-protocol--smtp-)
    + [Post Office Protocol (POP3)](#post-office-protocol--pop3-)
    + [Internet Message Access Protocol (IMAP4)](#internet-message-access-protocol--imap4-)
  * [Address Resolution Protocol (ARP)](#address-resolution-protocol--arp-)
      - [To Find MAC Addr of IP Addr](#to-find-mac-addr-of-ip-addr)
      - [Find MAC Addr on Different Network](#find-mac-addr-on-different-network)
    + [ARP Poisoning/Spoofing](#arp-poisoning-spoofing)
      - [Normal Scenario](#normal-scenario)
      - [Attack Scenario](#attack-scenario)
  * [Domain Name System (DNS)](#domain-name-system--dns-)
      - [How it Works](#how-it-works)
    + [DNS Poisoning/Spoofing](#dns-poisoning-spoofing)
      - [Example](#example)
  * [Simple Network Management Protocol (SNMP)](#simple-network-management-protocol--snmp-)
    + [Ping Sweeps](#ping-sweeps)
    + [Basic Port Scan](#basic-port-scan)
  * [Banner Grabbing](#banner-grabbing)
  * [Summary](#summary)


Telnet
---
- allow user to login remotely to another system
- port 23
- old protocol - data not encrypted
    - use SSH (secure shell)

Secure Shell (SSH)
---
- popular for remote login
- port 22
- data encrypted

Email Protocols
---
### Simple Mail Transport Protocol (SMTP)
- to transmit emails between computers
    - server to server or client to server

### Post Office Protocol (POP3)
- emails stored in mail server
    - users use own client comps to retrieve emails from server
- POP3 used to retrieve these emails
- POP3S - secured

![](https://i.imgur.com/63oz4Gh.png)

### Internet Message Access Protocol (IMAP4)
- alt to POP3
- IMAPS - secured


Address Resolution Protocol (ARP)
---
- when device has packet to send, will look at dest ip
    - determines if dest ip on same local network
        - look at net part of ip addr
    - if dest not local, packet sent to gateway
    - if dest local, send packet to dest
- MAC needed to send packet to dest on local network

#### To Find MAC Addr of IP Addr
- sender look at ARP table
- if ip not in arp table, sender send arp broadcast to all devices in local network to ask who has that ip addr
- device with ip addr send arp reply to sender with its mac
- sender send packet to the mac addr
- sender update arp table with the mac in case need to send more packets again

#### Find MAC Addr on Different Network
- src comp uses arp to retrieve mac addr of router configed as default gateway
- packet delivered to router
    - router determine whr packet shld go next
- when packet gets to dest network, router on dest network use arp to get dest comp's mac
- packet delivered to dest comp

### ARP Poisoning/Spoofing
- atker poison arp table
    - cause devices to send packets to him

#### Normal Scenario
![](https://i.imgur.com/Z0Wrqfc.png)

#### Attack Scenario
![](https://i.imgur.com/8lvlhtl.png)


Domain Name System (DNS)
---
- dns server translate fully qualified domain names (Eg. www.yahoo.com) to IP addr (Eg. 72.30.38.140)
- dns is distributed db system running on internet
- ea domain have 1 or more dns servers
- dns server (AKA nameserver) contain db holding section of domain names mapped to IP addr

![](https://i.imgur.com/OAFUhr4.png)

#### How it Works
![](https://i.imgur.com/Dnt5G8M.png)

### DNS Poisoning/Spoofing
- atker edit dns db/cache
    - direct users to his own website
- proper config of dns can reduce risks of this atk

#### Example
![](https://i.imgur.com/BAGvN5G.png)


Simple Network Management Protocol (SNMP)
---
- for remote monitoring & management of network nodes
- snmp manager monitors set of snmp agents installed on network nodes
    - check perf of monitored nodes
    - make changes in config of monitored nodes
- snmp agent can send warning to snmp manager of unusual situations

### Ping Sweeps
- ping sweep sends ping packets to range of IP addr to see which system will reply
- used to see which system is alive
- AKA ICMP sweep

### Basic Port Scan
- when send SYN packet to web server on port 80, it send back SYN/ACK packet as 3 way handshake

![](https://i.imgur.com/yGRpmAm.png)

- if port 80 not opened, no packet sent back

![](https://i.imgur.com/13YGYjF.png)

- firewalls can be configed to blk such port scans

![](https://i.imgur.com/Rdq1E0R.png)


Banner Grabbing
---
- many services return info like ver num when client connects to it
    - AKA banner
- banner grabbing - method to find more info abt running service
    - usually telnet/netcat used for banner grabbing

Summary
---
![](https://i.imgur.com/X41FXoy.png)



###### tags: `NETF` `DISM` `School` `Notes`