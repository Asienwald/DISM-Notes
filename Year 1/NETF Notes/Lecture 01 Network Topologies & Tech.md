---
title: 'Lecture 01 Network Topologies & Tech'
disqus: hackmd
---

:::info
ST1010 Network Fundamentals
:::

Topic 01 Network Topologies & Technologies
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

Physical Topologies
---
- topology - describes lay of land
- net topology describes how network physically laid out & how signals travel from 1 device to another
- physical layout of devices & cables doesn't describe how signals travel from 1 device to another
    - hence net topo categorised into physical & logical
- __physical topology__
    - arrangement of cabling & how cables connect 1 device to another in network considered network's physical topology
- the path data travels between computers on network considered network's __logical topology__
- all network designs today based on these basic phy topologies
    - bus
    - star
    - ring
    - meshed
    - point-t-point

### Physical Bus Topology
- continuous length of cable connecting 1 pc to another in daisy-chain fashion
    - simplest & at 1 time most common method for connecting pc
- weaknesses
    - limit of 30 pc per cable segment
    - max total length of cabling is 185m
    - both ends must be terminated
        - if not will over circuit & __signal bounce__
    - any break in bus brings down entire network
    - adding/removing machine brings down entire network temporarily
    - limited to 10mbps half-duplex comm since they use coaxial cabling
- due to limitations no longer used
    - is obselete

__How data travels in physical bus__
- electrical pulses (signals) travel cable's length in all dir
- __signal propagation__ - signal travels across medium & from device to device
- singal continues until weakened/absorbed by __terminator__
    - terminator is electrical component called resistor that absorbs signal instead of allowing it to bounce back up wire
- if not terminated, signal __bounces/reflected__ at end of medium
    - signal bounce is when electricity bounces off end of cable & back in other dir (causes echo)
![](https://i.imgur.com/wWDcoXn.png)

__Physical Bus Limitations__
- only 30 pc can be daisy-chained tgt
    - before signal becomes too weak
    - some of its strength absorbed by both cabling & connectors until signal too weak for NIC to interpret
- for same reason, total length of cabling is 185m

### Physical Star Topology
![](https://i.imgur.com/p0zMtS4.png)
- uses central device for monitoring & managing network
    - hubs & switches can include software that collects stats about net traffic patterns & detect errors
    - as long as cabling & NICs support it, star network can be easily updated by replacing central device
        - for higher speed if needed Eg. 100mbps to 1gbps
- advantages
    - faster than bus
    - centralised monitoring & management of network traffic possible
    - easier network upgrades
- when num of workstations you need exceed num of ports on central device you simply add another central device

__Extended Star__
- several hubs/switches connected, usually 1 device used as central connecting point, forming __extended star topology__
- most widely used in networks with a lot of pc
- central device (switch) sits in middle, connected to other switches/hubs to central switch's ports
    - pc & peripherals attached to these switchs/hubs forming additional stars
- AKA Hierarchical Star
![](https://i.imgur.com/8Xx73hN.png)

__How data travels in physical star__
- depends on type of central device
- central device determines logical topology
    - hub = logical bus
    - switch = logical switching
    - MAU = logical ring

__Physical Star Disadvantages__
- central device represents single point of failure
    - if hub/switch fails, entire network down
    - please have a spare on hand


### Physical Ring Topology
- is like bus
    - devices daisy-chained
    - instead of terminating ea end, cabling brought around from last device back to 1st to form ring
- most widely used to connect LANs with tech called __Fiber Distributed Data Interface (FDDI)__
    - FDDI most often used as __network backbone__, which is cabling used to comm between LANs/between hubs & switches
- data travels in 1 dir
- if any station in ring fails, network fails

__FDDI Dual Ring__
![](https://i.imgur.com/5nhsUN7.png)
- FDDI used as high speed backbone to connect servers, switches (which connects LANs) & terminal concentrators (which connects terminals)
- uses dual ring
    - data travels in both dir
    - 1 ring failure doesn't break network
    - operates using fiber-optic cable at 100mbps
    - extended star topo with Giabit Ethernet has largely replaced FDDI
![](https://i.imgur.com/KcMkkZb.png)

### Point-to-Point Topology
- direct link between 2 devices
    - used to connect 2 pc
- mostly used in WANs
- wireless bridge
    - connect 2 LANs separated by highway, river or railway tracks
- __Advantages__
    - data travels on dedicated link

__Point to Multipoint Topology__
- PMP topology - central device communicates with 2 or more other devices
    - all comm goes through central device
- often used in WANs where main office has connections to several branch offices via router
    - single connection made from router to switching device that directs traffic to correct branch office
- also used in wireless network arrangements
![](https://i.imgur.com/OaLXfqG.png)

### Mesh Topology
- connects ea device to every other device in network
    - multiple pt to pt connections for purposes of redundancy & fault tolerance
- purpose is to ensure if 1 or more connections fail, there's still path for reaching all devices on network
- expensive due to multiple interfaces & cabling
- found in large WANs & internetworks
![](https://i.imgur.com/2u55qmO.png)


Logical Topologies
---
![](https://i.imgur.com/0mRzuct.png)

- describes how data travels from pc to pc
- sometimes same as physical topology
    - in physical bus & ring, logical topology mimics phy arrangement of cables
    - Eg. physical bus vs logical bus
        - for physical star, electronics in central device determine logical topology
- logical ring using physical star implements ring inside the central device's electronics, which is a MAU in the token ring tech
![](https://i.imgur.com/HB4YhNS.png)

- in a __switched topology__, there is always an electrical connection between the computer & switch
    - but when no data being transferred, there is no logical connection/circuit between devices
![](https://i.imgur.com/lCGB8Ap.png)

- More
![](https://i.imgur.com/2KZDrD1.png)


Network Technologies
---
- network technology is the method an NIC uses to access the medium & send data frames
- other terms
    - network interface layer technologies
    - network architectures
    - data link layer technologies
- its whether your network uses Ethernet, 802.11 wireless, token ring or some combination of these to move data from device to device in your network
- Examples
    - LAN
        - ethernet
        - 802.11 wireless
        - token ring
    - WAN
        - frame relay
        - FDDI
        - ATM
- network technology often defines frame format & media

### Cables
- Unshielded Twisted Pair (UTP)
    - most common media type in LANs
    - consists of 4 pairs of copper wires twisted tgt
    - comes in numbered categories
- Fiber-Optic Cabling - uses twin strands of glass to carry pulses of light long distances & at high data rates
- Coaxial Cable - obsolete as LAN medium but used as network medium for Internet access via cable modem

__Categories of UTP Cables__
![](https://i.imgur.com/IwbhKcT.png)

### Baseband & Broadband Signaling
- network technologies can use media to transmit signals in 2 main ways
- __Baseband__ sends digital signals in ea bit of data represented by a pulse of electricity/light
    - sent at single fixed frequency & no other frames can be sent along with it
    - no more than 1 frame can be sent at same time
- __Broadband__ uses analog techniques to encode binary 1s & 0s across a continuous range of values
    - signals flow at partiuclar frequency & each frequency represents a channel of data
    - can have several transmissions occurring at same time

Ethernet Networks
---
- most popular LAN tech
    - easy to install & support with low cost factor
    - baseband
- supports broad range of speeds: 10mbps to 10gbps
- can operate in physical bus/star & logical bus/switched logical topology
- most NICs/hubs/switches can operate at multiple speeds: 10/100/1000
    - underlying tech is same

### Ethernet Addressing
- every station has physical MAC address
- ea MAC address has 48 bits expressed as 12 hex digits
- incoming frames must match NIC's address/broadcast address (FF-FF-FF-FF-FF-FF)
- once processed by NIC, incoming frames sent to network protocol for further processing

### Ethernet Frames
- 4 diff formats/__frame types__ depending on network protocol used to send frame
- ethernet II frame type used by TCP/IP
    - TCP/IP became dominant network protocol in LAN so supporting multiple frame types became unnecessary
- frames must be between 64 & 1518 bytes
    - dest MAC
    - source MAC
    - type
        - network protocol
    - data
    - FCS
        - error-handling/redundancy check
    - 1518 or 1.5kb so can have pause in between transfers and receive other packets too
![](https://i.imgur.com/NlhEuCK.png)
- in header, MAC address will change as you travel, pointing to your next destination
    - IP doesn't change

### Ethernet Media Access
- __Media access method__ - rules governing how & when medium can be accessed for transmission
- ethernet uses __Carrier Sense Multiple Access with Collision Detection (CSMA/CD)__
    - only used in a hub
        - switches have switching tables
    - Carrier Sense: listen before send
        - must hear silence
    - Multiple Access: if 2 or more stations hear silence, multiple stations ma transmit at same time
    - Collision Detection: if 2 or more stations transmit, a collision occurs & is detected by NIC
        - all stations & servers wait for a random amount of time before retransmitting
        - all stations must retransmit

Collisions & Collision Domains
---
- all devices interconnected by 1 or more hubs hear all signals generated by other devices
    - __usually happens in half-duplex__
    - full-duplex (switches) will not have collisions
- extent to which signals in Ethernet bus topology network propagated called __collision domain__
    - all devices in collision domain subject to possibility that whenever a device sends a frame, a collision might occur
- more collisions > need retransmit > slower network traffic
    - collisions do not occur in switches (they have switching tables)
![](https://i.imgur.com/rzqrpvW.png)

### Ethernet Error Handling
- ethernet is best-effort delivery system
    - no acknowledge whether data gets to dest
    - network protocols & apps ensure delivery
    - only collisions auto retransmitted
- ethernet detects damaged frames
    - error-checking code in frame's trailer called __Cyclic Redundancy Check (CRC)__
    - uses CRC to determine that data unchanged
    - if frame detected as damaged, its discarded with no notification

### Half-Duplex VS Full-Duplex Communication
- half-duplex - can talk & listen but not both
    - ethernet on hubs work in half-duplex
- full-duplex means NIC/switch can transmit/receive simultaneously 
    - CSMA/CD turned off
    - most switches operate in full-duplex


Ethernet Standards
---
__NO NEED MEMORISE OBSELETE ONES__
__USUALLY IN FORM OF MCQ__
- expressed as XBaseY
    - X: speed
    - Y: type of media
        - T = twisted pair
        - FX = fiber optic
    - Base = signal (Baseband)
        - is digital
- 10BaseT
    - use 2 of 4 wire pairs
    - runs over cat 3/higher UTP cabling
    - highly susceptible to collisions
    - obselete
- 100BaseTX
    - most common ethernet
    - cat 5/higher UTP
    - use 2 of 4 wire pairs
    - 2 types of 100BaseTX hubs
        - class I - can have >1 hub between devices
        - class II - can have max 2 hubs
    - switches can be used to connect many hubs
- 100BaseFX
    - runs over 2 strands of fiber optic
    - usually used as backbone cabling between hubs/switches
        - also used when immunity to noise & eavesdroppng required
- 100BaseT Ethernet
    - AKA Gigabit Ethernet
    - Cat 5/higher UTP
    - use all 4 wire pairs
- 100GBaseT Ethernet
    - over 4 pairs of cat 6A or 7 UTP
    - only full-duplex
        - no hubs, only switches support
    - expensive
    - good for servers so can keep up with systems that operate at 1gbps
- 100BaseT4
    - all 4 pairs
    - UTP cat 3
    - obselete
- 1000BaseLX
    - use fiber-optic media
    - "L" stands for "long wavelength" laser
    - supports max cable length of 5000m
- 1000BaseSX
    - use fiber-optic
    - "S" stands for "short wavelength" laser
    - not as long as long-wavelength lasers but less expensive
- 1000BaseCX
    - uses specially shielded, balanced, copper jumper cables
    - AKA "twinax"/"short-haul" copper cables
- 10 Gigabit Ethernet IEEE 802.3ae
    - similar to others in frame formats & media access
    - run only on fiber-optic
    - max 40km
    - primarily used for network backbones
    - varieties
        - 10GBaseSR, 10GBaseLR, 10GBaseER, 10GBaseSW, 10GBaseLW, and 10GBaseEW
- 40 Gigabit & 100 Gigabit Ethernet
    - high cost
    - prohibitive
    - adoption slow
    - fiber optic primary medium
        - though have provisions to use special copper assemblies over short dist
- Additional Ethernet standards
![](https://i.imgur.com/Nqbj8ot.png)

Wi-Fi
---
- 802.11 Wi-Fi
    - AKA __Wireless Fidelity (Wifi)__
    - __hotspot__ - public wifi network
    - is extension to ethernet
        - use airwaves instead of cabling as medium

### Modes of Operation
- 2 modes
    - infrastructure - use central access point (AP)
    - ad hoc - no central device
        - data travels from device to device like bus
        - AKA peer to peer mode
        - ![](https://i.imgur.com/MSxWKIf.png)
    - mostly focus on infrastructure mode
![](https://i.imgur.com/1srpkP1.png)

### Wifi Channels & Frequencies
- operate at 2.4ghz or 5ghz (not fixed)
- 2.4ghz actually 2.412 thru 2.484 divided into 14 channels spaced 5mhz apart
    - work like tv channel - must tune to channel to connect
    - needs 25mhz to operate spanning 5 channels
    - choose channels 5 apart from other known APs
- 5.0ghz actually 4.912 thru 5.825 ghz divided into 42 channels of 10, 20 or 40 mhz each
![](https://i.imgur.com/M1KGQZ5.png)

### Wifi Antennas
- antenna is both transmitter & receiver
    - characteristics & placement determine how well device transmits/receives wifi signals
- categorised by radiation pattern
    - omnidirectional antennas
        - signal radiate out in equal strengths in all dir
    - unidirectional antenna
        - signals focused in single dir
        - ideal for long, narrow spaces
![](https://i.imgur.com/xI95pES.png)

### Access Methods & Operation
- wifi access method
    - sending station can't hear if another station begins transmitting so cannot use CSMA/CD access method that ethernet uses
    - wifi device use carrier sense multiple access with __collision avoidance (CSMA/CA)__
    - use request-to-send/clear-to-send (RTS/CTS) packets and ack
        - extra handshake avoids collisions
    - with this extra "chatter" actual throughput cut in half

### Signal Characteristics
- common types of signal interference
    - absorption
        - solid objs absorb radio signals, causing them to __attenuate__ (weaken)
    - refraction
        - bending of radio signal as it passes from mediums of diff densities
    - diffraction
        - altering of wave as it tries to bend around obj
    - reflection
        - signal hits dense, reflective material resulting in signal loss
    - scattering
        - signal changes dir in unpredictable ways causing loss in signal strength
- signal-to-noise ratio
    - amount of noise compared to signal strength
    - noise can come from eq, wireless devices, wireless networks etc
- throughput - actual amt of data transferred
    - not counting errors & acknowledgements
- goodput - actual app-to-app data transfer speed
- overhead - packet frame headers, acks & retransmissions

### Wifi Standards
![](https://i.imgur.com/BP9BEAU.png)

### Non-Overlapping Channel
- Eg. 802.11b & g has 14 channels
    - 1, 6, 11 are non-overlapping
    - 2, 7, 12 are non-overlapping
    - 4, 8, 13 are non-overlapping etc
![](https://i.imgur.com/fWhQ3Wt.png)

### Wifi Security
- signals can travel several hundred feet - wifi devices outside home/office can detect your signals
- should be protected by encryption protocol that makes data difficult to interpret
- encryption protocols
    - wired equivalent privacy (WEP), Wifi protected access (WPA) & WPA2
    - not all devices support all 3 protocols
        - older devices might only support WEP or/& WPA

Token Ring Networks
---
- based on IEEE 802.5 standard
- star physical topology, ring logical topo
- token passed along network
    - only station with token can transmit
    - frame acknowledged & token released
    - no collisions
- originally operated at 4mbps then increased to 16mbps & later 100mbps
- uses cat 4 & higher UTP
- central device is __Multi-Access Unit (MAU)__
- obsolete

Fiber Distributed Data Interface Tech
---
- phy and logical ring topology
- uses token-passing access method & dual rings for redundancy
- transmits at 100mbps & can include up to 500 nodes over dist of 60miles
- uses fiber-optic cable only
- obsolete on new networks

Summary
---
![](https://i.imgur.com/hkvJzq5.png)
![](https://i.imgur.com/Q1wzOnK.png)



###### tags: `NETF SEM 2` `DISM SEM 2` `School` `Notes`
