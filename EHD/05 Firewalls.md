

Lecture 05 Firewalls
===




## Table of Contents

- [Lecture 05 Firewalls](#lecture-05-firewalls)
  * [Table of Contents](#table-of-contents)
  * [Network Address Translation](#network-address-translation)
    + [Why?](#why-)
    + [How does it Work?](#how-does-it-work-)
  * [Proxy Server](#proxy-server)
    + [How it Works](#how-it-works)
    + [Connecting to Proxies](#connecting-to-proxies)
    + [Advantages & Disadvantages](#advantages---disadvantages)
    + [Choosing Proxy](#choosing-proxy)
    + [Reverse Proxy](#reverse-proxy)
  * [Demilitarised Zone (DMZ)](#demilitarised-zone--dmz-)
  * [Bastion Host](#bastion-host)
  * [Honeypot](#honeypot)
  * [Firewalls](#firewalls)
    + [Firewall Rules](#firewall-rules)
    + [What it Can't Do](#what-it-can-t-do)
    + [Types of Firewalls](#types-of-firewalls)
      - [Personal Firewalls](#personal-firewalls)
      - [Enterprise Firewalls](#enterprise-firewalls)
    + [Application Layer Firewall](#application-layer-firewall)
  * [Packet Filtering](#packet-filtering)
    + [Stateless Packet Filtering](#stateless-packet-filtering)
    + [Stateful Packet Filtering](#stateful-packet-filtering)
    + [Typical Locations of Packet Filters](#typical-locations-of-packet-filters)
  * [Configuring Firewall Rules](#configuring-firewall-rules)
      - [Base Rules on Policy](#base-rules-on-policy)
      - [Keeps Rule Base Simple](#keeps-rule-base-simple)
    + [Restrict Subnets, Ports & Protocols](#restrict-subnets--ports---protocols)
    + [General Practices](#general-practices)
    + [Anti-Spoofing Rule](#anti-spoofing-rule)
    + [Firewall Rule Matching](#firewall-rule-matching)
    + [Firewall Logs](#firewall-logs)
  * [Designing Firewall Configurations](#designing-firewall-configurations)
    + [Screening Router](#screening-router)
    + [Dual-Homed Host](#dual-homed-host)
    + [Screened Host](#screened-host)
    + [Screened Subnet DMZ](#screened-subnet-dmz)
    + [Multiple DMZ](#multiple-dmz)
    + [Multiple Firewalls](#multiple-firewalls)
    + [Advantages & Disadvantages](#advantages---disadvantages-1)
  * [Comparing Firewalls](#comparing-firewalls)
    + [Software-based Firewalls](#software-based-firewalls)
    + [Hardware Firewalls](#hardware-firewalls)
    + [Hybrid Firewalls](#hybrid-firewalls)
    + [Advantages & Disadvanatages](#advantages---disadvanatages)
  * [Summary](#summary)

Network Address Translation
---
- network device (usually firewall/proxy) hides internal IP from outside
    - public IP presented instead

![](https://i.imgur.com/TkMphWe.png)

### Why?
- reduce num of public IP required by org
    - hundred/thousands of internal comps behind single IP
- internal IP hidden from attackers

### How does it Work?
- when internal comp requests data from web server in internet, packet goes through NAT device

![](https://i.imgur.com/lGFx3tG.png)

- NAT device replaces source IP with public IP & sends packet to web server in internet

- web server only sees public IP
    - send packet to NAT device

![](https://i.imgur.com/T5RUkgr.png)

- NAT device rmbs which internal comp requested for data & send accordingly

![](https://i.imgur.com/dXKTeDr.png)


Proxy Server
---
- proxy intercepts internal user requests & processes request on behalf of user

![](https://i.imgur.com/oSAnhHx.png)

- keeps cache of retrieved webpages
    - other users requesting same page can retrieve from proxy cache
    - faster retrieval time
- can filter webcontent
    - blk access to undesirable websites
    - keeps log of websites accessed
- hide IP address

![](https://i.imgur.com/xg9dIFI.png)

### How it Works
- prevent direct conn between external & internal comps
- work at application layer
    - examines data in packet
    - decides which app/system to forward packet to
    - reconstructs packet & forwards it
        - replace orig header with new header containing proxy's own IP

![](https://i.imgur.com/pedq93g.png)
![](https://i.imgur.com/XTNqK6g.png)

### Connecting to Proxies
- client programs (Eg. web browsers) can be configured to connect to proxy instead of internet
- transparent proxy servers/intercepting proxies dont need client to be specially configured

### Advantages & Disadvantages
![](https://i.imgur.com/cwiq2Gm.png)

### Choosing Proxy
- freeware proxy
    - AKA content filters
    - might not have advanced features
    - Eg. Squid
- commercial proxy
    - offers
        - webpage caching
        - srs & dest IP addr translation
        - content filtering
        - NAT
    - Eg. many hardware firewalls come with this

### Reverse Proxy
- reverse proxy used to help web server
    - offload some load off server by caching static web content
    - perform load balancing among multiple web servers
    - handle SSL encryption
        - free web servers from doing encryption/decryption of data

![](https://i.imgur.com/66gCRIZ.png)


Demilitarised Zone (DMZ)
---
- normally all internal comps kept inaccessible from internet
    - but public users still need to access some res like web servers
    - DMZ is section of network visible to outside world
    - public users can access DMZ but cannot enter internal secured network
    - AKA service network/perimeter network

![](https://i.imgur.com/pyHr5VR.png)


Bastion Host
---
- normally refers to comp specially protected through OS patches, auth, encryption etc.
    - specially secured comps normally at network perimeter
        - may be in DMZ
- usually provides web, ftp, email, other services running on specially secured server

![](https://i.imgur.com/7hVXHUm.png)


Honeypot
---
- comp placed on network perimeter
- attracts atkers away from real & critical servers
- logging
    - logs used to learn abt atker's techniques
- legal issues
    - Eg. atker use purposely unsecured honeypot to harm other networks

![](https://i.imgur.com/tEBb41x.png)


Firewalls
---
- firewall
    - hardware/software
    - blk unauth network access
    - earliest were packet filters
- not standalone solution
    - cannot protect from internal threats
    - need strong security policy & employee education
    - must be combined with other security solutions
        - antivirus
        - intrusion detection systems

### Firewall Rules
- can be configed by setting rules
- rules for blking traffic can be done case-by-case
- actions
    - allow traffic
    - blk traffic
    - customise access
        - Eg. forward packet to another set of rules for further processing

### What it Can't Do
- firewalls cannot protect conns that dont go through it

![](https://i.imgur.com/iCk0S8C.png)

### Types of Firewalls

#### Personal Firewalls
- some firewalls designed for personal use
    - norton internet security
    - zonealarm

#### Enterprise Firewalls
- designed for company/enterprise
- for monitoring & protecting large-scale networks
- manage security policies throughout org


### Application Layer Firewall
- inspect both header & data portions of packets
- AKA content filtering
- can check for malicious code in data
- combination of packet filters & app layer firewalls can be used in network



Packet Filtering
---
- only info in headers checked
    - data not checked
- types
    - stateless packet filtering
    - staeful packet filtering

### Stateless Packet Filtering
- decide whether to allow/blk based only on info on protocol headers
- filtering based on common IP header features
    - IP addr & ports
    - protocols
    - flags & options
- advantage
    - inexpensive & fast
- disadvantage
    - atks more complicated

![](https://i.imgur.com/Qsml5p3.png)

### Stateful Packet Filtering
- besides looking at info in protocol header, also keeps record of conns host comp made with other comps
    - maintain file called __state table__ containing record of all current conns
    - allows incoming packets to pass only from external hosts alrdy connected

![](https://i.imgur.com/Qf1Ecrc.png)

### Typical Locations of Packet Filters
- packet filter placement
    - between internet & host/network
    - between proxy & internet
    - either end of DMZ

![](https://i.imgur.com/5Y5WMlt.png)
![](https://i.imgur.com/46tc7PB.png)


Configuring Firewall Rules
---
- rule base
    - tells firewalls what to do when certain kind of traffic attempts to pass
- pts to consider
    - based on org's security policy
    - determine what can be access from external network
    - logging & auditing requirements
    - NAT if used
    - simple & short as possible
        - firewall shld not cause too much delay in network speed
        - shld be easy to maintain

#### Base Rules on Policy
![](https://i.imgur.com/JmCaQfg.png)

#### Keeps Rule Base Simple
- keep list of rules as short as possible
    - so firewall perform faster
- firewalls process rules in particular order
    - if rules numbered, firewall matches packets with 1st rule then 2nd rule, so on
    - most impt & frequently accessed shdl be at top of list
    - make last rule a cleanup rule
        - catch-all type of rule

![](https://i.imgur.com/Rsow3pU.png)
![](https://i.imgur.com/1Uo34sb.png)

### Restrict Subnets, Ports & Protocols
- can filter by
    - IP addr
    - ports
- some firewalls can filter by name of service
    - dont  need rmb port num
- some firewalls can also filter by 6 TCP control flags/IP options

### General Practices
- most freq matches rules shld be near top of rule base for faster processing
- nobody can connect to firewall except admin
- blk direct access from internet to any comp behind firewall
- permit access to public services in DMZ

![](https://i.imgur.com/OWJ8hig.png)

### Anti-Spoofing Rule
- many firewall configs, 1st rule is anti-spoofing rule
- anti-spoofing rule blks packets coming from outside network pretending to be internal system

![](https://i.imgur.com/yCVNxKo.png)

### Firewall Rule Matching
- firewalls match packets to rules in particular order
    - once rule matches, packet processed according to action (allow/blk) specified in rule
- for firewalls with numbered rules, packets matches to rules according to rule numbers
![](https://i.imgur.com/bl00DOf.png)

- other firewalls will match deny rules then allow rules
- packets that dont match any rules will follow firewall's default policy action
    - normally deny any packet not explicitly allowed

### Firewall Logs
- decide what to log
    - some firewalls log only packets associated with deny rule
        - Eg. blked IP addresses
- configuring log file format
    - many firewalls generate log files in plaintxt
    - sophisticared firewalls save log files in other formats
- review log files regularly
    - log files can indicate signatures of atk attempts
- prepare log file summaries & generating reports
    - log summary
        - show major events over period of time
        - contain raw data that can be used to create reports
    - some firewalls contain log file analysis tools
        - viewing raw data tedious & error-prone
    - reports
        - display data in easy-to-read format



Designing Firewall Configurations
---
- firewalls deployed in many ways
    - part of screening router
    - dual-homed host
    - screen host
    - screened subnet DMZ
    - multiple DMZs
    - multiple firewalls
    - reverse firewall
- can be other methods of deploying firewalls
    - depends on company's network & needs


### Screening Router
- screening router
    - determines whether to allow/deny packets based on src/dest IP addrs
        - or other info in headers
    - dont stop many atks
        - especially those that use spoofed/manipulated IP info
    - shld be combined with firewall/proxy
        - for extra protection

![](https://i.imgur.com/zk158VV.png)


### Dual-Homed Host
- comp configured with >1 network interface
- firewall software forwards packets from 1 NIC to another
- limited security
- host servers as single pt of entry to org

![](https://i.imgur.com/xeUYgVM.png)

### Screened Host
- similar to dual-homed host
- can add router between host & internet
    - for packet filtering
- combines dual-homed host & screening router
- can func as gateway/proxy

![](https://i.imgur.com/K2irkhB.png)


### Screened Subnet DMZ
- dmz
    - subnet of publicly accessible servers placed outside internal LAN
    - AKA __service network__ or __perimeter network__
- firewall that protects DMZ connected to internet & LAN
    - AKA __three-pronged firewall__

![](https://i.imgur.com/O2WDpgl.png)

### Multiple DMZ
- server farm
    - grp of servers connected in own subnet
    - work tgt to receive reqiests with help of load-balancing software
- load-balancing software
    - prioritises & schedules requests & distributes to servers
- clusters of servers in DMZ helps protecting network from being overloaded
    - ea server farm/DMZ can be protected with own firewall/packet filter

![](https://i.imgur.com/4g9iTov.png)

### Multiple Firewalls
- protecting DMZ with 2/more firewalls
    - 1 control traffic between dmz & internet
    - other control traffic between protected LAN & dmz
        - can server as failover firewall
    - advantage
        - can control whr traffic goes in 3 networks you have
    - extra firewall inside internal network to protect network management systems
        - extra lvl of protection
        - intruders that gain control of network management system can potentially gain access to all network

![](https://i.imgur.com/UZ4cWEq.png)

- protect branch offices with many firewall
    - multiple firewalls can be implemented in single security policy
    - central office has centralised firewall
        - directs traffic for branch offices & their firewalls
        - deploys security policy through this firewall using security workstation

![](https://i.imgur.com/NgjQMrF.png)

### Advantages & Disadvantages
![](https://i.imgur.com/bXoXKtG.png)


Comparing Firewalls
---
- software-based
- hardware-based
- hybrid

### Software-based Firewalls
- free firewall programs
- commercial programs for personal use
- commercial for enterprise use
    - capable of managing multile instances from centralised location

### Hardware Firewalls
- AKA firewall appliances
- advantages
    - dont depend on conventional OS
    - generally more scalable than software firewalls
- disadvantages
    - depend on nonconventional OS
    - more expensive than software products

### Hybrid Firewalls
- combines aspects of hardware & software firewalls
- benefits from strengths of both solutions

### Advantages & Disadvanatages
![](https://i.imgur.com/qQplapY.png)


Summary
---
![](https://i.imgur.com/TVrNW5q.png)



###### tags: `EHD` `DISM` `School` `Notes`