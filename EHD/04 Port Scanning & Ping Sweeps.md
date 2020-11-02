
Lecture 04 Port Scanning & Ping Sweeps
===




## Table of Contents

- [Lecture 04 Port Scanning & Ping Sweeps](#lecture-04-port-scanning---ping-sweeps)
  * [Table of Contents](#table-of-contents)
  * [Introduction to Port Scanning](#introduction-to-port-scanning)
    + [Port Scanning Tools](#port-scanning-tools)
  * [Types of Port Scans](#types-of-port-scans)
    + [TCP Connect Scan (-sT)](#tcp-connect-scan---st-)
    + [SYN Scan (-sS)](#syn-scan---ss-)
    + [FIN (-sF), XMAS (-sX), NULL (-sN) scans](#fin---sf---xmas---sx---null---sn--scans)
    + [ACK Scan (-sA)](#ack-scan---sa-)
    + [Range of Ports Scanned](#range-of-ports-scanned)
  * [NMAP](#nmap)
    + [Summary NMAP](#summary-nmap)
      - [Review Questions](#review-questions)
    + [Avoiding Detection](#avoiding-detection)
    + [Common Nmap Options for Timing](#common-nmap-options-for-timing)
    + [Host Discovery](#host-discovery)
  * [Unicornscan](#unicornscan)
  * [Ping Sweeps for Host Discovery](#ping-sweeps-for-host-discovery)
    + [Fping](#fping)
    + [Other Methods](#other-methods)
    + [Hping](#hping)
  * [Resources](#resources)
  * [Summary](#summary)

Introduction to Port Scanning
---
- 2nd stage of pentestring - network discovery
- port scanning
    - find whichs ervices offered by host
    - identify vuln
    - can report
        - open ports
        - closed ports
            - not blked by firewall but no service running on port
        - filtered ports
            - possibly behind firewall
        - best-guess assessment of which OS running
- open services can be used in attacks
    - identify vuln port
    - launch exploit
- scan all ports when testing
    - not just well-known ports
    - 0 to 65536 (both TCP/UDP)

### Port Scanning Tools
- nmap (network mapper)
    - popular
        - open source
        - standard tool for pros
    - CMD/GUI ver
        - Eg. Zenmap

![](https://i.imgur.com/ct2EmWn.png)

Types of Port Scans
---
- SYN scan
- TCP connect scan
    - complete 3 way handshake
- NULL scan
    - packet flags turned off
- XMAS scan
    - FIN, PSH & URG flags set

### TCP Connect Scan (-sT)
- if port opened, tcp 3 way handshake established

![](https://i.imgur.com/6HbGfsk.png)

- if port closed, RST returned

![](https://i.imgur.com/AE7UxCY.png)

### SYN Scan (-sS)
- if port opened

![](https://i.imgur.com/uSJWidY.png)

- if port closed

![](https://i.imgur.com/8tvLd39.png)

- since tcp 3 way handshake not completed, app wont log connection
    - hence quieter/stealthy compared to TCP connect scan

### FIN (-sF), XMAS (-sX), NULL (-sN) scans
- FIN scan
    - send only packets with FIN flag
- XMAS scan
    - send packets with FIN, PSH & URG flags
- NULL scan
    - send packets with no flags
        - theoretically null packets dont exist

- if port open

![](https://i.imgur.com/E7Sfa58.png)

- if port closed

![](https://i.imgur.com/263OCdP.png)


- AKA stealth scans as only 1 packet sent & 1 reply packet expected
- problems
    - 1st prob
        - if firewall blks port, no reply received
        - hence "open|filtered" received
    - 2nd prob
        - diff os respond diff
        - Eg. windows reply RST regardless of open/closed ports
- need use other scans to cfm observations

### ACK Scan (-sA)
- only reply filtered/unfiltered
- use for traversing through firewall
- if no resp, firewall may be present
    - Eg. filtered

![](https://i.imgur.com/CLnzdf5.png)

- if RST received, no firewall or firewall allowed ACK packet through

![](https://i.imgur.com/B0FSDej.png)

### Range of Ports Scanned
- nmap by default only scans common 1000 ports for ea protocol (TCP/UDP)
- nmap determines most common 1000 ports from `/usr/share/nmap/nmap-services` file based of freq indicated in file
- can specify which ports u want nmap to scan using -p


NMAP
---

### Summary NMAP
![](https://i.imgur.com/p4ilbLY.png)

#### Review Questions
![](https://i.imgur.com/QYUqIZt.png)


### Avoiding Detection
- port scans noisy
    - generate lots of traffic & slow down network
- atkers may try to avoid sending large num of packets in short burst of time
    - scan throttling - delay progression of scan over hours, days or even weeks
    - Eg. 1 SYN packet sent to 1 port every 30 mins. difficult to detect

### Common Nmap Options for Timing
![](https://i.imgur.com/hWQGboy.png)

### Host Discovery
- by default nmap will try to discover if host alive before scanning ports
    - if target on same network, nmap will send ARP broadcast to discover if host is up
    - if target on diff network, nmap will send following to discover is host up
        - ICMP echo request
        - SYN packet to port 443 & ACK packet to port 80
        - ICMP timestamp request

![](https://i.imgur.com/e7I5LbW.png)


Unicornscan
---
- developed for 2004
    - ideal for large networks
- scans 65535 ports in 3-7 seconds
    - handles port scanning using
        - TCP
        - ICMP
        - IP
    - optimises UDP scanning
- unix based


Ping Sweeps for Host Discovery
---
- ping sweeps
    - identify which ip belong to active hosts
    - ping range of ip addrs
- problems
    - comps that shut down cannot respond
    - networks can be configed to blk ICMP echo requests
    - firewalls may filter out icmp traffic

### Fping
- fping.sourceforge.net
- ping multiple ip simultaneously
- cmd tool
- input: multiple ip addr
    - entered at shell
        - -g option
    - input file with addr
        - -f option
    - nmap equivalent for ping sweep
        - `nmap -sP ip_addr`

![](https://i.imgur.com/XBsqIPb.png)


### Other Methods
- ARP broadcasts
    - send arp broadcast requests for range of ip to see which host will reply
    - can only discover hosts in same network
    - can use netdiscover tool/nmap with -sn

### Hping
- used to bypass filtering devices
    - allows user to fragment & manipulate IP packets
- www.hping.org
    - powerful tool
        - all security testers must be familiar with tool
        - support many parameters (command options)



Resources
---
- https://securitytrails.com/blog/nmap-vulnerability-scan


Summary
---
![](https://i.imgur.com/rz1yIX5.png)



###### tags: `EHD` `DISM` `School` `Notes`