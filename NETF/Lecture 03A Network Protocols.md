---
title: 'Lecture 03A Network Protocols'
disqus: hackmd
---

:::info
ST1010 Network Fundamentals
:::

Lecture 03A Network Protocols
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


Network Protocols
---
- network protocols - protocol devices follow when comm
    - set out rules on how devices comm with ea other

### OSI Model & TCP Stack
![](https://i.imgur.com/xkeFG8y.png)

#### Network Layer 3
- network layer - controls transmission of packets along router on network
    - controls IP packets
#### Transport Layer 4
- see below


### TCP/IP's Layered Architecture
- example of how layers work tgt
    - start browser & your homepage is `www.cengage.com`
    - browser format request for homepage using app layer protocol HTTP
        - Eg. get the cengage.com home page
        - unit of info the app layer works with called __data__
    - app layer protocol HTTP passes request down to transport-layer protocol (TCP)
    - TCP adds TCP header to request
        - unit of info TCP works with called __segment__
    - TCP passes segment to internetwork layer protocol (IP)
    - IP placed IP header on segment
        - unit of info called __packet__
        - packet passed to network access layer - whr NIC operates
    - frame header & trailer added
    - frame delivered to network medium as bits
        - (on way to www.cengage.com server)
    - web server processes it & returns a webpage

#### Headers of Each Layer
![](https://i.imgur.com/VIxn0Cr.png)


### MAC Address
- media access control
- unique physical address assigned to NICs
    - assigned by vendor of NIC
- represented as 6 grps of 2 hex digits
    - Eg. 01:D6:A7:F0:38:95

### Ethernet Frame
- data link layer - transmits frames between adjacent nodes
- for data travlling on ethernet cables

![](https://i.imgur.com/8qzYGdi.png)

### ICMP
- internet control msg protocol
- assists TCP/IP networks with troubleshooting comm probs
    - can tell if another host is alive through ping signal
- firewall & packet filters might be used to blk ICMP packets

#### ICMP Payload
![](https://i.imgur.com/6nSk17T.png)
- common ICMP type codes
    - 0 - echo reply
    - 3 - dest unreachable
    - 7 - dest host unknown
    - 8 - echo request

#### Ping Signatures
- signature - type of characteristics/pattern used to define type of network activity

![](https://i.imgur.com/VvTPbg9.png)

### Time-to-Live (TTL)
- TTL is field in IP packet
- when packet created, TTL set to initial val
- as packet travels on internet, ea time it passes through router, TTL field is decremented
- when TTL reaches 0 & packet not reached dest yet, router discards it & sends ICMP packet back to sender
    - this prevents packets from staying in internet forever

#### Default TTLs
- diff OSes have diff default TTL vals for their packets
    - can guess OS of source

### Hypertext Transfer Protocol (HTTP)
- protocol used to access data on world wide web

![](https://i.imgur.com/rEjl9cA.png)

#### HTTP Signatures
![](https://i.imgur.com/71lO5Ad.png)
![](https://i.imgur.com/KenELi0.png)


#### HTTPS
- why need HTTPS?
- in norm HTTP, client web requests & server responses (webpages) sent over internet in cleartext
    - anyone can intercept traffic & view data traffic
- HTTPS - to transport HTTP data securely over internet
    - HTTP over SSL (secure socket layer) or HTTP over TLS (transport layer security)
- session key set up to encrypt traffic between user & web server
- anyone who intercepts data cant decrypt it


### File Transfer Protocol (FTP)
- protocol for copying files between systems
- 2 connections used
    - control conn for user auth & other control info
        - usually port 21 on ftp server
    - data conn for transfer of file data
        - may be port 20 or other on ftp server
- old protocol - designed when security not issue
    - no encryption
        - all data including password sent in plaintext
    - use alternatives like SFTP

#### FTP Signatures
![](https://i.imgur.com/r85CfJY.png)
![](https://i.imgur.com/DmJgpPi.png)



IP Addressing
---
### IPv4 & IPv6
- IPv4 uses 32bit (4 byte/octets) addresses
    - limits the address space to abt 4 billion
- IPv6 uses 128bit addresses
    - supports about 300 trillion trillion trillion addreses
    - Eg. `2001:0db8:8fa3:dc94:1a2e:a370:7334:7337`
    - 1 or more consecutive sections of all 0s in IPv6 address can be replaced by double colon
        - Eg. `2001:0f58:0:0:0:0:1986:202` can become `2001:0f58::1986:202`

### IP Classes
![](https://i.imgur.com/Ueo1go7.png)

- packets that begin with 127 in 1st octet used for network testing
- broadcast addresses generally end with 255

### Subnet Mask
- IP address components
    - network address
    - host address
    - subnet mask
- subnet mask determines whcih part of address is for network & host
    - can be used to divide network into subnetworks

#### Classless Interdoamin Routing (CIDR) Notation
- Eg. 192.168.1.0/24
    - means network 192.168.1.0 have netmask of 255.255.255.0

### Loopback Address
- hostname localhost or IP 127.0.0.1 refers to local machine
- packet addresses to loopback nvr leaves the system
- used for testing



Transport Layer 4 - TCP & UDP
---
- transport layer - provides transfer of data between end nodes
    - TCP & UDP
- TCP - transmission control protocol
    - connection-oriented
    - monitoring receipt of frames
        - resend if needed
    - controls data flow
- UDP - user datagram protcol
    - connectionless
    - doesnt guarantee packets received
    - no flow control

#### TCP Packet
![](https://i.imgur.com/vWiVPfJ.png)

#### UDP Packet
![](https://i.imgur.com/RsK0Rev.png)


### TCP Flags
- flags
    - URG - urgent
    - ACK - acknowledge
    - PSH - push func
    - RST - reset connection
    - SYN - synchronise sequence numbers
    - FIN - finished
- request for comments (RFC)
    - document to describe standards for networking protocols
- TCP - RFC 793
    - www.ietf.org/rfc/rfc793.txt

### UDP Headers
- UDP - provides transport service for IP
    - unreliable as connectionless
        - udp packet doesnt contain sequence/ack nums that enable tcp to guarantee delivery
    - faster than tcp - less overhead
    - used for broadcasting msgs/for protocols that dont need same lvl of service as tcp
    - atkers can also scan for open udp services
- common applications that use udp
    - DNS, DHCP, SNMP

### TCP 3-way Handshake
- tcp uses 3way handshake to establish connection between 2 comps

![](https://i.imgur.com/PIyZEfh.png)

- tcp session begins when client sends tcp syn segment to dest device (usually server)
    - dest port num specified & src port num assigned dynamically
- when server receives syn segment, it responds by sending 1 of 2 segments
    - ack-syn segment or rst segment
- if rst segment returned, server refused the request to open a session
    - possibly because dest port is unknown
- if ack-syn segment returned, client completes the 3way handshake by sending ack segment back
    - client then ready to begin sending/requesting data

### TCP SEQ & ACK Numbers
- TCP uses SEQ & ACK fields to check that all packets sent & received correctly
- SEQ num is randomly allocated to SYN packet
    - SEQ is sequence num given to 1st data byte in tcp packet
- ACK contains sequence num of next packet expected to be received
- __IMPT__ - just need to understand below
    - with SEQ & ACK nums, TCP can re-order packets that arrive out of sequence
    - with SEQ & ACK nums, TCP can tell if packet is missing in transit & can resend packet

__Example__
![](https://i.imgur.com/6tWzbtl.png)

__Simplified Website Request__
![](https://i.imgur.com/miAag2q.png)
![](https://i.imgur.com/HcYJJ5a.png)

- help

### TCP & UDP Ports
- virtual channel to apps that are sending & receiving network data
    - AKA sockets
- port nums start from 0 to 65535
- well-known port nums
    - 21, 20 - file transfer protocl (FTP)
    - 25 - simple mail transfer protocol (SMTP)
    - 80 - hypertext transfer protocol (HTTP)
    - 443 - hypertext transfer protocol secure (HTTPS)
    - more

Netstat
---
- used to display opened ports & current network connections

#### Sample Output
![](https://i.imgur.com/tQu7Pjo.png)

### Columns
- local address

![](https://i.imgur.com/IBDS1I6.png)

- foreign address
    - IP address of machine connected to port

### Common States
- LISTENING
    - port ready & listening for new conns
- SYN_SEND
    - syn packet sent
- SYN_RECEIVED
    - syn packet received
- ESTABLISHED
    - conn established with port
- CLOSE_WAIT
    - fin packet received
- LAST_ACK
    - fin packet sent
- TIME_WAIT
    - after sending fin packet, wait awhile to ensure no more data being sent on conn
- CLOSED
    - conn closed


Summary
---
![](https://i.imgur.com/kUl2ROs.png)

        



###### tags: `NETF` `DISM` `School` `Notes`