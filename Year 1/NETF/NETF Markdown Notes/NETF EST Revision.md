---
title: 'NETF EST Revision'
disqus: hackmd
---

:::info
ST1010 Network Fundamentals
:::

NETF EST Revision
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

Overview
---
- section A 10 qns
    - 20%
- section B 6 qns 80%
    - topic 3a & 3b (2q)
    - topic 4 (2q)
    - topic 5 (2q)

03A/B Network Protocols
---
- network protocols - protocol devices follow when comm
    - set out rules on how devices comm with ea other

### OSI Model & TCP Stack
![](https://i.imgur.com/xkeFG8y.png)

- datalink layer - transmit frames between adj nodes
- network layer - controls transmission of packets along router on network
    - controls IP packets
- transport layer - provide transfer of data between end nodes


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
    - __frame__ delivered to network medium as bits
        - (on way to www.cengage.com server)
    - web server processes it & returns a webpage

#### Headers of Each Layer
![](https://i.imgur.com/VIxn0Cr.png)

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

### Time-to-Live (TTL)
- field in IP packet
- when packet created, TTL set to initial val
- as packet travels on internet, ea time it passes through router, TTL field is decremented
- when TTL reaches 0 & packet not reached dest yet, router discards it & sends ICMP packet back to sender
    - this prevents packets from staying in internet forever

#### Default TTLs
- diff OSes have diff default TTL vals for their packets
    - can guess OS of source

### HTTP & HTTPS
- http - protocol used to access data on www
    - web requests & server responses sent in cleartext
    - anyone can intercept & read
- https - transport http data securely over internet
    - http over SSL (secure socket layer) or TLS (transport layer security)
    - session key to en/decrypt traffic


### TCP (Transmission Control Protocol)
- connection-oriented
- monitoring receipt of frames
    - resend if needed
- controls data flow

#### TCP Packet
![](https://i.imgur.com/vWiVPfJ.png)

#### TCP Flags
- flags
    - URG - urgent
    - ACK - acknowledge
    - PSH - push func
    - RST - reset connection
    - SYN - synchronise sequence numbers
    - FIN - finished
- request for comments (RFC)
    - document to describe standards for networking protocols

#### TCP SEQ & ACK Numbers
- with SEQ & ACK nums, TCP can
    - reorder packets arrived out of sequence
    - tell if packets missing in transit & resend

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

### UDP (User Datagram Protocol)
- connectionless
    - unreliable
    - no SEQ/ACK nums to enable tcp to guranatee delivery
- doesnt guarantee packets received
- no flow control
- faster than tcp
    - no overhead

#### UDP Packet
![](https://i.imgur.com/RsK0Rev.png)


### Netstat
- used to display opened ports & current network connections

#### Columns
- protocol - tcp/udp
- local address

![](https://i.imgur.com/IBDS1I6.png)

- foreign address
    - IP address of machine connected to port`

- state
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


### Address Resolution Protocol (ARP)
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

#### ARP Poisoning
- atker poison arp table
    - cause devices to send packets to him


04 Network Hardware in Depth
---
### Switches
- datalink layer 2 - work w frames
- switches send broadcast frames out all ports
- ea switch port considered a collision domain
    - dont forward collision info to other ports
- can operate in full-duplex

#### Creating Switch Table
- switching table holds MAC address/port pairs that tell switch whr to forward a frame based on dest MAC
- switching table empty when switch powered on
    - add frame's src addr mapped to port received on when receiving frames
- if frame's dest not found in table, the switch forwards the frame to all ports

![](https://i.imgur.com/5P0svpZ.png)

- most swithes include a num that indicates num of MAC addresses the switch can hold
    - Eg. 8k MAC supported
- __stale entries__
    - prevent stale entries by including timestamp when entry created
        - when switch gets frame from device alrdy in table, it updates the entry with new timestamp
    - period of time a table keeps a MAC is called __aging time__
        - if timestamp not updated within aging time, the entry expires & removed from table

#### Frame Forwarding Methods
- cut-through switching - only read frame's src & dest
    - fastest
    - disadvantage - no error checking
- store-and-forward switching - reads entire frame into buffers before forwarding
    - examines the FCS field to ensure no errors before forwarding
        - __frame check sequence (FCS)__ - error-detecting code added to a frame
    - all errors except frame fragments forwarded
    - medium
- fragment-free switching - switch reads enough of frame to guarantee that its at least the min size for network type
    - slowest
    - no error forwarded

![](https://i.imgur.com/fX8RIw7.png)


### Advanced Switch Features
- high-end switches (AKA smart switches/manages switches) can help make network more efficient & reliable
- common features in smart switches
    - multicast processing
    - spanning tree protocol
    - virtual lan
    - port security

#### Multicast Processing
- switches process multicast frames in 1 of 2 ways
    - as broadcast & send to all port
        - used by low-end switches or those not configured for it
    - by forwarding frames only to ports with the registered multicast addr
        - used by switches that support internet grp management protocol (IGMP)
        - multicast MAC addr always begin with `01:00:5E`
            - rest of addr identifies particular multicast app

#### Spanning Tree Protocol (STP)
- enables switches to detect when there's potential for switching loop
    - occurs when frame is forwarded from 1 switch to another in infinite loop
- when possible loop detected,
    - 1 of switch ports goes into blking mode
        - prevents it from forwarding frames that creates loops
    - if loop config broken, switch that was in blking mode resumes forwarding frames

![](https://i.imgur.com/kRItQC8.png)

- Side Effects of STP
    - device takes longer to create link with switch that runs the protocol

- Rapid Spanning Tree Protocol (RSTP)
    - enhancement to STP that provides faster convergence when topology changes


#### Virtual Local Area Networks (VLANs)
- enable you to config 1 or more switch ports into separate broadcast domains
    - like separating switch into 2 or more switches that aint connected
- router needed to comm between VLANs
- improves management & security of network & gives more control of broadcast frames
- allows admins to grp users & resources logically instead of by phy location

![](https://i.imgur.com/JpTSywh.png)
![](https://i.imgur.com/mPHS2Xj.png)

- VLAN Trunks
    - __trunk port__ - switch port configed to carry traffic from all VLANs to another switch/router
        - switch/router port must also be configed as trunk port
    - involves switch adding tag to ea frame that must traverse the trunk port
        - VLAN tag identifies which vlan traffic originated from

- Consideration Factors
    - overuse of vlans will cost more than it benefits you
    - more vlan = more logical networks
        - network more complicated
    - every vlan you create needs corr router interface
        - routers are slow so perf decrease with more vlan
    - more router interfaces mean more IP networks
        - need subnetting your existing network


#### Switch Port Security
- network jacks with connections to switches often avail to public users - can plug in laptop with viruses, hacker tools or malware
    - switch with port security can help prevent these types of conn
- enables admin to limit how many & which MAC can connect to a port
    - if unauth comp attempts to connect, port can be disabled & msg sent to admin to alert them of intrusion

### Routers
- network layer 3 - work with packets
- connect separate logical networks to form internetwork
- broadcast frames not forwarded to other outer ports/networks
- can use complex internetworks with multiple paths
    - creates fault tolerance & load sharing

#### Routing Tables
- composed of network addr & interface pairs that tell router which interface packet shld be forwarded to
- most tables contain following for ea entry
    - dest network - in CIDR notation
    - next hop - indicates interface name/addr of next router in path to dest
        - total num of routers a packet must travel through called __hop count__
    - metric - numeric val that tells router how far away dest network is
        - AKA cost or distance
    - how route derived - tells you how route got into routing table (1 of 3 ways)
        - network connected directly
        - admin enters route info manually
            - AKA __static route__
        - route info entered dynamically via __routing protocol__
    - timestamp - tells router how long since the routing protocol updated the dynamic route

![](https://i.imgur.com/EFoUJjA.png)

#### Routing Protocols
- set of rules that routers use to exchange info so all routers have accurate info abt internetwork to populate their routing tables
- 2 main types of protocols
    - dist-vector protocols
    - link-state protocols

- dist-vector protocol
    - share info abt internetwork's status by copying router's routing table to other routers
        - routers sharing network are called __neighbour__
        - routing info protocol (RIP) & RIPv2 are most common

- link-state protocol
    - share info with other routers by sending status of all interface links to other routers
        - open shortest path first (OSPF) most common


![](https://i.imgur.com/hQNm1KI.png)

- __speed of convergence__ - how fast routing tables of all routers in internetwork updated when change in network occurs

- __interior gateway protocols (IGP)__ used in __autonomous system (AS)__
    - AS - internetwork managed by single org
    - routing protocols discussed so far are IGPs
- __exterior gateway protocols (EGP)__ used between AS
    - Eg. broder gateway protocol (BGP)
        - path vector routing protocol - analyses characeristics of all ASs to form nonlooping routing topology
- static routes entered in manually

#### Access Control Lists
- rules configed on router's interface to specify which addr & protocols can pass through interface & to which dests
- when ACL blks packet, called __packet filtering__
- blk traffic based on
    - inbound/outbound traffic
    - src/dest addr
    - protocol



### Wireless Access Points (WAP)
- 3 devices in 1
    - wireless AP
    - router
    - switch

#### Wireless Security Options
- encryption - all private networks shld use
    - common protocols
        - wired equivalent privacy (WEP)
        - wifi protected access (WPA)
        - WPA2
    - use highest lvl of security your systems support
        - all device must use same protocol
- auth - users enter user & password to access wireless network
    - APs that support auth usually support remote dial-in user service (RADIUS) protocol
- MAC filtering - enables you to restrict which devices can connect to AP based on mac addr
- AP Isolation - creates seperate virtual network for ea client conn
    - clients can access internet but cant comm with ea other


05 Troubleshooting & Support
---
### Documenting Your Network
- why?
    - make eq moves/adds/changes easier
    - provide info for troublshooting
    - justification for extra staff/eq
    - determine compliance with standards
    - supply proof that installations meet hardware/software requirements
    - reduce training requirements
    - facilitate security management
    - improve compliance with software licensing agreements

#### Documentation & Troubleshooting
- accurate doc of workstation MAC can help quickly find issues
    - Eg. IP addr conflicts, src of invalid/excessive frames
- what shld be documented
    - phy & logical addressing
    - devices connectivity
    - cabling data

#### Documentation & IT Staffing
- document type & freq of support calls can provide justification for additions to staff/tools to make support more efficient
- stats on network resp time & bandwidth load > justify upgrading servers/adding new eq
- train new employees on how to properly document additions & changes

#### Documentation & Standards Compliance
- document which standards in use
    - Eg. whether 568A or 568B wiring standard used for patch panels & jacks
- other reasons
    - when disputes occur between you & eq vendor abt persistent network error

#### Documentation & Technical Support
- some manufacturers of devices will want to know abt your cabling's test results when solving network device prob
- when calling tech support for software prob, manufacturer would want to know hardware details + OS ver & patch installations

#### Documentation & Security
- doc security patches & virus protection updates helps you adhere to security policies & cfm your resistance to current threats

### Problem Solving Process
- steps 
    - determine prob definition & scope
    - gather info
    - consider possible causes
    - device solution
    - implment solution
    - test solution
    - document solution
    - device preventative measures

#### Step 1 - Determine Prob Definition & Scope
- prob def shld describe what works & what doesnt
    - know who & what affected by prob
- qns to ask
    - anyone else having same prob?
    - how abt other areas?
    - prob in 1 app or more?
    - does prob occur on diff comp?
- assign priority to prob once defined

#### Step 2 - Gather Info
- qns to ask
    - did it ever work?
        - overlooked but helpful
    - when did it stop working?
        - prob occur everytime or intermittently?
        - particular times of day when prob occurs?
        - other apps running when prob occur?
    - anything changed?
        - any network changes made?
- dont ignore obvious
    - check for unplugged cabled
- define how it's supposed to work
    - good doc & clear baseline of network
        - baseline of network shld include network utilisation stats; utilitsation stats on server CPUs, memory, hard drives & other res; normal traffic patterns
        - why? > if utilisation increase by 2-3% per month, can prepare for perf upgrade

#### Step 3 - Consider Possible Causes
- create checklist of possible things that could have gone wrong

![](https://i.imgur.com/I1IzM96.png)

#### Step 4 - Devise Solution
- consider
    - is identified cause truly the cause or just another symptom?
    - is thr way to test proposed solution?
    - what results shld solution produce?
    - ramifications of proposed solution on rest of network?
    - do you need extra help to answer any of these qns?
- might need to
    - save all network device config files
    - doc & backup workstation configs
    - doc wiring closet configs
    - conduct final baseline to compare new & old results

#### Step 5 - Implement Solution
- create intermediate testing opportunities
    - testing small steps in limited num of things can go wrong easier than testing complex solution with lots of prob areas
- inform users of possible disruption to network services
- put plan into action
    - take note of every change you make

#### Step 6 - Test Solution
- testing shld emulate real-world situation
- if testing workstation prob
    - attempt to logon to network as user with similar privileges as main user
    - attempt to access apps that would run on workstation
- if testing network upgrade
    - start some workstations on upgraded part of network & run network-intensive apps
    - gather info abt how network behaves & compare with prev results (before upgrade)

#### Step 7 - Document Solution
- include everything pertinent to prob
    - prob def
    - solution
    - implementation
    - testing
- if prob & solution have implications for entire network, include this info

#### Step 8 - Devise Preventive Measures
- after solving prob, do everything you can to prevent this prob/similar probs from recurring

![](https://i.imgur.com/gTaUfsY.png)

- devise preventive measures is proactive rather than reactive network management


### Approaches to Troubleshooting
- diff methods
    - trail & error
    - solve by example
    - replacement method
    - step by step with OSI model

#### Trial & Error
- require assessment of prob, educated guess to solution & test of results
- used under following conditions
    - system newly configed, no data can be lost
    - system not attached to live network
    - can undo changes easily
    - other approaches take more time than few trail & error attempts
    - few possible causes to prob
    - doc & other res available to draw on to arrive at a solution more scientifically
- not advisable under these conditions
    - server/internwtroking device live on network
    - prob discussed over phone & you're instructing an untrained user
    - you're nt consequence of solutions your propose
    - you cannot undo changes 
    - other approcahes take same amt of time
- follow these guidelines
    - make only 1 change at a time before testing results
    - avoid making changes that affect operation of live network
    - document original settings of hardware & software before making changes
    - avoid making change that can destroy user data
    - if possible, avoid making change that you can't undo

#### Solve by Example
- process of comparing sth that doesnt work with sth that does
    - easiest/fastest ways to solve prob
- general rules
    - use approach only when working sample has similar env as prob machine
    - dont make config changes that will cause conflicts
        - dont change TCP/IP addr of nonworking machine to same addr as working machine
    - dont make changes that can destroy data that cant be restored

#### Replacement Method
- need narrowing down possible srcs of prob & having known working replacement parts on hand so they can be swapped out
- follow these 3 rules
    - narrow list of potentially defective parts down to few possibilities
    - make sure have correct replacement parts on hand
    - replace only 1 part at a time
    - if 1st replacement dont fix prob, reinstall orig part before replacing another part

#### Step by Step with OSI Model
- test prob starting with app layer & keep testing ea layer until have successful test/reach phy layer
    - can also start at phy layer & work way up
- must understand how networks work & shld use troubleshooting tools


### Problem-Solving Resources
- res avail
    - experience
    - internet
    - network doc

#### Experience
- make most out of it
    - take notes abt what you see & learn
- if happened once, will happen again
    - dont think prob so obscure that wont happen again - take time to make not of it
- colleague's experience
    - use people as res
- experience from manufacturer's tech support
    - best time to call when you have specific err num or msg that can report to manufacturer
    - have software ver nums or hardware serial num avail when calling

#### Internet
- most manufacturers create db of probs & solutions so customers can research prob themselves
    - AKA knowledge base/FAQ
- use knowledge base/search engine
    - as specific as possible
    - with error msgs, enclose in quotation marks
- finding drivers & updates
    - when installing new device/OS, check bus fixes, driver updates or new firmware revisions avail
- consulting online support services & newsgroups
    - many online support services dedicated to technical subjects
    - useful subscription pay service is Experts Exchange
- researching online periodicals
    - some of most popular networking journals
        - network computing
        - info week
        - network world
        - windows IT pro mag
        - linux journal

#### Network Documentation
- doc shld read like user's manual for network admins
- network diagrams
    - include network diagrams showing logical pic of network & another diagram showing network phy aspects
        - Eg. rooms, devices, connections


- internetworking devices
    - need diff lvls of doc
        - simple, unmanaged switches need least info
    - shld include model & serial nums, locations, IP, MAC & num of ports (total & num of free ports)

![](https://i.imgur.com/NjLptAe.png)



### Network Troubleshooting Tools
- common tools
    - ping & trace route
    - network monitors
    - protocol analysers
    - time domain relfectometer (TDR)
    - cable testers
    - additonal tools

#### Ping & Tracert
- `ping` cmd tells you whether your comp can comm with another comp using ip
    - with successful reply, know that target machine running & there's path between you comp & target
    - also tell amt of time elapsed before reply received
- with connectivity prob, 1st verify that there are link lights on switch or NIC
    - then use `ping` to verify network layer connectivity
- follow steps
    - run `ipconfig /all` - display ip config
    - ping loopback addr
        - if ping 127.0.0.1 & receive resp, verified ip protocol working
    - ping local ip
        - verify comp can receive icmp packets
    - ping default gateway
        - default gateway is addr of router comp sends packets to when dest on another network
    - ping ip addr of host
        - verifies if can comm using icmp of target comp
    - ping hostname
        - verify you can resolve hostname
    - ping dns server
        - resp from dns server indicate comp can comm with server that can resolve names to IP addr
    - use nslookup
        - verify that dns server can resolve name of host
- using `tracert`
    - `tracert` does reverse dns lookup on ip addr of ea router & displays name of router
    - resp times can help determine if thr is bottleneck between src & dest
    - can also also be used to cfm network design

![](https://i.imgur.com/AG77Q0u.png)

#### Network Monitors
- software packages that can track all/part of network traffic
    - can track packet type, errors & traffic to/from ea comp
    - can generate reports & graphs
    - some programs can email admins when prob detected

#### Protocol Analysers
- protocol analysers allows you to capture packets & analyse network traffic generated by diff protocols
    - can be used to troubleshoot probs related to dns, auth, dhcp, ip addressing, remote access etc
    - also used to create baselines for network perf
- most advanced analysers combine hardware & software in self-contained unit
    - Eg. savvius (wildpackets), omnipeek, fluke network optiview network analyser, wireshark

#### Time-Domain Reflectometer (TDR)
- used to determine whether there's break/short in cable & measure cable length
- TDR sends electrical pulse down cable that reflects back when encounter break or short
    - measures time takes for signal to return & can estimates how far down cable the fault located
- shld use TDR to document actual lengths of all cables


#### Additional Tools
- optical power meter (OPM) - used to measure amt of light on fiber-optic circuit
    - often used to determine amt of signal loss on fiber-optic cable between transmitter (emitter) & receiver
    - amt of signal loss can determine whether the fiber-optic termination was done correctly & whether receiver can interpret signals correctly


### Common Troubleshooting Situations
- cabling & related components
    - 1st step to determine whether prob is with cable/comp
        - check by connecting another comp to cable
    - verify its right type of cable for conn & terminated correctly
    - check back of NIC card to see if have indicator lights
    - if NIC no lights, can try swap NIC
- power fluctuations
    - verify servers up & running
    - use UPSs with batt power to they can be shut down w/o data loss in event of power loss
- upgrades - when you perform network upgrades
    - keep current & do 1 upgrade at a time to make life easier
    - test upgrade before deploying on production network
    - tell users abt upgrades
        - will be more understanding if they're notified beforehand
- poor network perf
    - what changed since last time network functioned normally?
    - new eq added?
    - new apps added to comps on network?
    - someone playing games across network?
    - are thr new users on networks? how many?
    - could any other new eq (Eg. generator) cause interference near network?
- if new users/added eq/newly introduced apps degrade network perf, time to expand network


### Disaster Recovery
- disaster can be anything from server disk crash to fire/flood
- section focus on
    - backup procedures
    - recovery from system failure

#### Backing Up Network Data
- determine what data shld be backed up & how often
- develop schedule for backing up data
- identify people responsible for performing backups
- test backup system regularly
- maintain backup log listing what data backed up, when backed up, who performed backup & what media used
- develop plan for storing data after has been backed up

#### Backup Types
- full backup
    - copies all selected file to selected media & marks file as backed up
- incremental backup
    - copies all files changed since last full/incremental backup & marks files as backed up
- differential backup
    - copies all files since last file backup
    - doesnt mark files as backed up
- copy backup
    - copies selected files to selected media w/o marking files as backed up 
- daily backup
    - copies all files changed the day backup made
    - doesnt mark files as backed up
- bare metal restore backup
    - designed to allow restoring system disk directly from backup media w/o having to install OS & backup software
- of these backup types
    - full, incremental & differential backups most useful as part of regular backup schedule
- system state backup
    - for windows only
    - copy boot files, registry, active dirs on domain controllers and other critical information


#### Backup Schedule
- good model for creating backup schedule combines weekly full backup with daily differential backups
- when creating schedule, post schedule & assign 1 person to perform backups & sign off on them
- windows systems have extra backup type called __system state backup__
    - copies boot files, registry, active dir on domain controllers & other critical info

#### Business Continuity
- consist of policies, procedures & res required to ensure business can func after major catatrophe
- if bulk of IT infrastructure maintained in house, company shld consider 1 of following
    - __cold site__ - phy location that house hardware needed to get IT functioning again
        - only infrastructure, no technology
        - Eg. have place, no pcs and shit
    - __warm site__ - location containing all infrastructure needed for operations to continue
        - Eg. have place with pc and shit
        - have power, phones and networks
        - may have servers & other res
    - __hot site__ - can be running at moment's notice


Focus Areas
---
![](https://i.imgur.com/CDD5p64.jpg)
(creds to Eric for sending this pic)

### Topic 05 Troubleshooting
- diff methods of troubleshooting
    - when to use which method
    - step by step must have more understanding compared to rest
- 3 resources
- all 5 types of backup
    - know how to explain/compare
- troubleshooting tools
    - know them
    - slide 57, OPM, TDR, protocol analyzer, ping etc.
    - cable tester dont need

### Topic 04 Network Hardware
- what device is what lvl
- switching table/routing table
    - what is inside
- frame forwarding methods
- advanced switch features
    - asked to explain
- routing protocols - 2 types
    - distance vector
    - link stage
- slide 47 onwards dont need study

### Topic 3a and 3b
- 3 way handshake and ARP
- know layers


###### tags: `NETF SEM 2` `DISM SEM 2` `School` `Notes`