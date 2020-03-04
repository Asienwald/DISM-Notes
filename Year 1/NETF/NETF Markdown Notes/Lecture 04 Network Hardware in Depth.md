---
title: 'Lecture 04 Network Hardware in Depth'
disqus: hackmd
---

:::info
ST1010 Network Fundamentals
:::

Lecture 04 Network Hardware in Depth
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

Network Switches in Depth
---
- work at datalink layer 2
    - receive frames on 1 port & forward to port whr dest device found
- switches send broadcast frames out all ports
- ea switch port considered a collision domain
    - dont forward collision info to other ports
- can operate in full-duplex
    - allows connected devices to transmit & receive simultaneously - eliminates possibility of collision

### Port Modes of Operation
- ports on typical 10/100 mbps switch can usually operate in these modes
    - 10mbps half duplex
    - 100mbps half duplex
    - 10 mbps full duplex
    - 100mbps full duplex
- most inexpensive switches run in auto-nego mode
    - switch sets mode to highest perf setting the device supports
- __auto-MDIX__ mode - switch port detects type of device & cable it's connected to
    - straight-through or crossover cable can be used

### Creating Switch Table
- switching table holds MAC address/port pairs that tell switch whr to forward a frame based on dest MAC
- when switch powered on, its table is empty
    - as network devices send frames, switch reads ea frame's src address & adds to table with port its received from
- if frame's dest not found in table, the switch forwards the frame to all ports

![](https://i.imgur.com/5P0svpZ.png)

- most swithes include a num that indicates num of MAC addresses the switch can hold
    - Eg. 8k MAC supported
- switching tables prevent stale entries by including timestamp when entry created
    - when switch gets frame from device alrdy in table, it updates the entry with new timestamp
- period of time a table keeps a MAC is called __aging time__
    - if timestamp not updated within aging time, the entry expires & removed from table

### Frame Forwarding Methods
- cut-through switching - switch reads only enoguh of incoming frame to determine frame's src & dest
    - fastest
    - disadvantage - no error checking
- store-and-forward switching - switch reads entire frame into buffers before forwarding
    - examines the FCS field to enure it contains no errors before forwarding
    - a frame check sequence (FCS) refers to an error-detecting code added to a frame in a communications protocol
- fragment-free switching - switch reads enough of frame to guarantee that its at least the min size for network type

![](https://i.imgur.com/fX8RIw7.png)

### Multilayer Switches
- have funcs of switch (layer 2) but add layers 3 capabilities
    - typically used in interior of networks to route between vlans instead of being placed on network perimeter
- perf advantage over traditional routers
    - packet routing between vlans done within switch than having to exit switch to router

![](https://i.imgur.com/inAuCsA.png)



Advanced Switch Features
---
- high-end switches (AKA smart switches/manages switches) can help make network more efficient & reliable
- common features in smart switches
    - multicast processing
    - spanning tree protocol
    - virtual lan
    - port security

### Multicast Processing
- switches process multicast frames in 1 of 2 ways
    - as broadcast & send to all port
        - used by low-end switches or those not configured for it
    - by forwarding frames only to ports with the registered multicast addr
        - used by switches that support internet grp management protocol (IGMP)
        - multicast MAC addr always begin with `01:00:5E`
            - rest of addr identifies particular multicast app

### Spanning Tree Protocol (STP)
- enables switches to detect when there's potential for switching loop
    - occurs when frame is forwarded from 1 switch to another in infinite loop
- when possible loop detected,
    - 1 of switch ports goes into blking mode
        - prevents it from forwarding frames that creates loops
    - if loop config broken, switch that was in blking mode resumes forwarding frames

![](https://i.imgur.com/kRItQC8.png)

#### Side Effects of STP
- device takes longer to create link with switch that runs the protocol

#### Rapid Spanning Tree Protocol (RSTP)
- enhancement to STP that provides faster convergence when topology changes


### Virtual Local Area Networks (VLANs)
- enable you to config 1 or more switch ports into separate broadcast domains
    - like separating switch into 2 or more switches that aint connected
- router needed to comm between VLANs
- improves management & security of network & gives more control of broadcast frames
- allows admins to grp users & resources logically instead of by phy location

![](https://i.imgur.com/JpTSywh.png)
![](https://i.imgur.com/mPHS2Xj.png)

#### VLAN Trunks
- __trunk port__ - switch port configed to carry traffic from all VLANs to another switch/router
    - switch/router port must also be configed as trunk port
- involves switch adding tag to ea frame that must traverse the trunk port
    - VLAN tag identifies which vlan traffic originated from

#### Consideration Factors
- overuse of vlans will cost more than it benefits you
- more vlan = more logical networks
    - network more complicated
- every vlan you create needs corr router interface
    - routers are slow so perf decrease with more vlan
- more router interfaces mean more IP networks
    - need subnetting your existing network


### Switch Port Security
- network jacks with connections to switches often avail to public users - can plug in laptop with viruses, hacker tools or malware
    - switch with port security can help prevent these types of conn
    - enables admin to limit how many & which MAC can connect to a port
    - if unauth comp attempts to connect, port can be disabled & msg sent to admin to alert them of intrusion


Routers in Depth
---
- operate at network layer 3 & work with packets
    - connect separate logical networks to form internetwork
    - broadcast frames not forwarded to other outer ports/networks
    - can use complex internetworks with multiple paths
        - creates fault tolerance & load sharing
- all processing depends on following features
    - router interfaces
    - routing tables
    - routing protocols
    - access control lists

![](https://i.imgur.com/KWr70jC.png)

### Router Interfaces
- must have 2 or more interfaces (ports) to forard packets to other networks
- when router interface receives frame, it compares the dest MAC with interface's MAC
    - if match, router strips frame header & trailer & reads packet's dest IP
    - if IP maches, it proceeds the packet
        - if not, router consults with routing table to determine how to get packet to dest
    - process of moving packet from incoming interfce to outgoing interface called __packet forwarding__

![](https://i.imgur.com/7lXfYik.png)
![](https://i.imgur.com/jmoOedh.png)

### Routing Tables
- composed of network addr & interface pairs that telll router which interface packet shld be forwarded to
- most tables contain following for ea entry
    - dest network - usually in CIDR notation
    - next hop - indicates interface name/addr of next router in path to dest
        - total num of routers a packet must travel through called __hop count__
    - metric - numeric val that tells router how far away dest network is
        - AKA cost or distance
    - how route derived - tells you how route gets into routing table (1 of 3 ways)
        - network connected directly
        - admin enters route info manually
            - AKA __static route__
        - route info entered dynamically via __routing protocol__
    - timestamp - tells router how long since the routing protocol updated the dynamic route

![](https://i.imgur.com/EFoUJjA.png)

### Routing Protocols
- set of rules that routers use to exchange info so all routers have accurate info abt internetwork to populate their routing tables
- 2 main types of protocols
    - dist-vector protocols
    - link-state protocols

![](https://i.imgur.com/hQNm1KI.png)

- __speed of convergence__ - how fast routing tables of all routers in internetwork updated when change in network occurs

- __interior gateway protocols (IGP)__ used in __autonomous system (AS)__
    - AS - internetwork managed by single org
    - routing protocols discussed so far are IGPs
- __exterior gateway protocols (EGP)__ used between AS
    - Eg. broder gateway protocol (BGP)
        - path vector routing protocol - analyses characeristics of all ASs to form nonlooping routing topology
- static routes entered in manually


#### Distance-Vector Protocols
- share info abt internetwork's status by copying router's routing table to other routers
    - routers sharing network are called __neighbour__
    - routing info protocol (RIP) & RIPv2 are most common

#### Link-State Protocols
- share info with other routers by sending status of all interface links to other routers
    - open shortest path first (OSPF) most common

#### Routing Protocols Considerations
- does network change often?
    - routing protocol good
- are there several alt paths to many of the networks in the internetwork?
    - routing protocol can reroute arnd down links or congested routes automatically
- is internetwork large?
    - routing protocol builds & maintains routing protocols automatically


### Access Control Lists
- set of rules configed on router's interface for specifying which addr & protocols can pass through interface & to whcih dests
- when ACL blks packet, its called __packet filtering__
- usually configd to blk traffic based on
    - inbound/outbound traffic
    - src addr
    - dest addr
    - protocol
- addr can be specific IP addr or network nums & filtering can be done on either src/dest addr or both


Wireless Access Points (WAP) in Depth
---
- 3 devices in 1
    - wireless AP
    - router
    - switch

### Basic Wireless Settings
- wireless network mode
    - allows you to choose which 802.11 standard AP shld operate under
- wireless network name (SSID)
    - when AP is shipped SSID is set to default
        - pls change it
- wireless channel
    - recommended set channels 5 chann apart
        - Eg. 1, 6 & 11
- SSID broadcast status
    - by default, APs configed to transmit the SSID so any wireless device in range can see network

### Wireless Security Options
- encryption - all private networks shld use
    - common protocols
        - wired equivalent privacy (WEP)
        - wifi protected access (WPA)
        - WPA2
    - use highest lvl of security your systems support
        - all device must use same protocol
- auth - users enter user & password to access wireless network
    - APs that support auth usually support remote dial-in user service (RADIUS) protocol
- MAC filtering - enables you to restrict which devices can connect to AP
    - & MAC of wireless devices allowed to access network to a list on AP
- AP Isolation - creates seperate virtual network for ea client conn
    - clients can access internet but cant comm with ea other

### Advanced Wireless Settings
- adjustable transmit power
    - control power & range of wireless signal
- multiple SSIDs
    - 2 or more wireless networks can be created with diff security settings
- vlan support
    - assign wireless networks to wired vlan
- traffic priority
    - if AP configed for multiple networks, can assign priority to packets coming from ea network
- wifi multimedia
    - provides quality of service (QoS) settings for multimedia traffic
    - gives priority to streaming audio/video
- AP modes
    - AP can set to operate as traditional AP, repeater or wireless bridge


NIC in Depth
---
- NIC makes conn between comp & network medium
    - perf & reliability of NIC crucial to comp's network perf

### Advanced Features
- if NIC slow, can limit network perf
- when selecting network adapter, 1st identify phy characteristics card must match
    - type of bus/tech/connector needed
- norm desktop comps with basic features usually adequate
    - servers sometimes warrant these high-end features
    - virtualised envs benefit from NICs with multiple ports

#### Hardware Enhancement Options
- shared adapter memory
    - adapter's buffers map directly to RAM on comp
- shared system memory
    - NIC's onboard processor selects region of RAM on comp & writes to it as though it were buffer space on adapter
- bus mastering
    - permit network adapter to take control of comp's bus to init & manage data transfers to/from comp's memory
- RAM buffering
    - NIC includes extra memory to provide temp storage for incoming/outgoing network data that arrives at NIC faster than it can be sent out
- onboard co-processors
    - enable card to process incoming & outgoing network data w/o requiring service from CPU
- QOS allow pripritising time-sensitive data
- auto link aggregation
    - enable you to install multiple NICs in 1 comp & aggregate bandwidth
- improved fault tolerance
    - by installing 2nd NIC
    - failure of primary NIC shifts network traffic to 2nd NIC
- advanced config power management interface (ACPI)
    - offers wake-up LAN
    - allow admin to power on PC remotely by accessing NIC through network
- preboot execution environment (PXE) adapter
    - allow comp to download OS instead of booting from local hard drive
    - used on diskless workstations (thin clients) that dont store OS locally


Firewall
---
- security device that puts up barrier between local network & internet
- acts as filter, allowing/restricting data traffic between network/other networks
- flexible
    - allows you to modify the blking rules by
        - IP
        - protocol (TCP, UDP, ICMP)
        - port
        - or for software apps & services

### Router VS Firewall
![](https://i.imgur.com/jRJqeTH.png)

### Hardware VS Software Firewall
- both protect from malicious traffic
- hardware firewall can be stand-alone device or part of router
    - such router is simple & effective protection solution for network
        - reviews headers of data packets & decides if can be trusted
        - if think packet safe, forward
        - else, drop
- software firewall - program that you install on comp
    - can be part of antivirus suit or separate
    - protect from uncontrolled access to comp
    - depending on software can keep safe from trojans & worms too
    - differences
        - it will only protect the device with the firewall installed
            - have to install on all devices to be protected
        - will run in background - use up system resources
            - lead to slowdowns

Summary
---
![](https://i.imgur.com/USFh1Em.png)
![](https://i.imgur.com/1niSRv8.png)
![](https://i.imgur.com/VeulV6T.png)



###### tags: `NETF SEM 2` `DISM SEM 2` `School` `Notes`