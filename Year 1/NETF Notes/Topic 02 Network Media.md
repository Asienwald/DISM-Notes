---
title: 'Topic 02 Network Media'
disqus: hackmd
---

:::info
ST1010 Network Fundamentals
:::

Topic 02 Network Media
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


Wired Networking
---
- uses tangible physical media called cables
- 2 broad categories of cables
    - copper wire
    - fiber optic
    - main diff between them
        - composition of signals (electicity & light)
        - speed of signals
        - distance signal can travel

### Criteria for Choosing Network Media
- bandwidth rating - num of bits per sec that can be transmitted across medium
    - factor determining bandwidth is how bit signals represented on medium (called __encoding__)
    - ![](https://i.imgur.com/cEOI8Pg.png)
    - when possible choose cabling cat that's compatible with the standard you want to implement now but will support growth & faster speeds
- max segment length - max cable length between 2 network devices
    - ea cable type can transport data only so far before its signals begin to weaken beyond what can be read by a receiving device (__attenuation__)
    - intermediate passive devices (Eg. wall jacks) are part of total segment length
![](https://i.imgur.com/06dlzEY.png)
- interference & eavesdroppping susceptibility
    - interference to electrical signals on copper media comes in form of __electromagnetic interference (EMI)__ & __radio frequency interference (RFI)__
        - motors, transformers, fluorescent lights or other sources of intense electrical activity can emit both EMI & RFI
        - RFI can also affect wireless networks if freq in same range
    - __Crosstalk__ - inteference 1 wire generates on another when in bundle
    - copper wires susceptible to electronic eavesdropping
        - fiber-optic carry light signals so not susceptible to interference or eavesdropping
- cable grade
    - building & fire codes include specific cabling requirements
    - cables ran between false ceiling
        - true ceiling (plenum) must be plenum-rated
    - UTP cabling marked as __communication cable riser (CMR)__ or __comm cable plenum (CMP)__
        - CMR can only be used for building risers/cable trays
        - CMP suitable for use in plenum spaces
- connection hardware
    - every type of cable has connectors that influence kinds of hardware cable can connect to
    - must make sure media selected can support network device

__Other Considerations__
- ease of installation
    - media's minimum bend radius
        - limits angle cable can be bent to run around corners
    - cost & time to terminate medium
    - phy environment - types of walls, ceilings, EMI or RFI
- testability - network that "works" might be crippled by excessive errors
    - important to certify whether cable meets requirements for its cat
- total cost
    - cabling, connectors, termination panels, wall jacks, termination tools, testing eq, time etc.

Cables
---
### Coaxial Cable
- AKA coax
- once was predominant form of network cabling
    - started to phase out in early 1990's
- inexpensive & easy to install
- still used primarily in connecting cable modem to wall outlet your cable TV/internet provider installs

### Twisted-Pair Cable
- 2 types
    - unshielded
    - shielded
- consists of 1 or more pairs of insulated strands of copper wires twisted around 1 another & housed in outer jacket
- twists necessary to improve resistance to crosstalk from wires & EMI from outside sources
    - more twists per unit length, better resistance to EMI & crosstalk
    - more expensive TP wisted more than less expensive
        - provides better pathway for higher bandwidth networks
        - tbh you won't bother, just make sure its cat is high
![](https://i.imgur.com/6U7DUEz.png)

### Unshielded Twisted-Pair Cable
- most networks use unshielded twisted pair (UTP)
- consists of 4 pairs of insulated wires
- rated accordingly to cats devised by __Telecommunications Industry Assocation (TIA)__ & __Electronic Industries Alliance (EIA)__ & __American National Standards Institutes (ANSI)__
- cat 1 to 6a accepted in US
    - 2 additional cat aren't yet TIA/EIA standards & might never be in US
    - Europe has accepted cat 7 & 7a, which specify that ea wire pair is shielded
![](https://i.imgur.com/LN7QPfG.png)
![](https://i.imgur.com/GSDIxtT.png)
- cat 5e & 6 UTP cabling characteristics
    - most popular types of UTP cabling today

### Shielded Twisted-Pair Cable
- includes shielding to reduce crosstalk & interference
    - has wire braid inside sheath material/foil wrap
    - best to use in electrically noisy environments/very high-bandwidth apps

__Twisted-Pair Cable Plant Components__
- __RJ-45 connectors__ - STP & UTP uses registered jack 45
    - most commonly used in patch cables
        - used to connect computers to hubs, switches & RJ-45 wall jacks
- Rj-45 jacks - what you plug an RJ-45 connector into when computer not near a switch/hub
    - usually placed behind wall plates when cables run inside walls
- patch cable
    - short cable for connecting computer to RJ-45 wall jack or connecting a patch-panel port to switch/hub
        - can be made with inexpensive tols, 2 RJ-45 plugs & length of TP cable
- patch panels
    - used to terminate long runs of cable from where computers are to wiring closet (where switches & hubs are)
- distribution racks
    - hold network equipment
        - Eg. routers, switches, patch panels, rack-mounted servers etc.
    - AKA 19" racks as upright rails are 19" apart

### Medium Dependent Interface
- network devices that connect using RJ-45 plugs over twisted-pair cabling classified as __medium dependent interface (MDI)__ or __MDI crossed (MDI-X) devices__
    - Eg. PC, NICs & routers
- MDI devices receive on pins 1 & 2 and transmit on pins 3 & 6
    - Eg. hubs & switches
- when 2 switches etc. need to be connected, use crossover cable so that transmit & receive wires get crossed

__why 2 transmit & 2 receive wires?__
- 1 wire pair used for transmit (labeled transmit+/transmit-) and 1 pair for receive (labeled receive+/receive-)
- plus & minus symbols indicate that wires carry positive & negative signal
    - this __differential signal__ mitigates effect of crosstalk & noise on cable

### Fiber-Optic Cable
- bits transmitted as pulses of light instead of electricity
- immune to electrical interference
- highly secure
    - electronic eavesdropping eliminated
- composition
    - slender cylinder glass fiber called core surrounded by concentric layer of glass called __cladding__
    - fiber jacketed in thin transparent plastic material called __buffer__
![](https://i.imgur.com/m1Yx40k.png)
- ea fiber-optic strand carries data in only 1 dir
    - network connections consist of 2 or more strands
- fiber-optic cable used as backbone cabling often comes in bundles of 12 or more fiber strands
    - even only using 2 in backbone, running more is good idea so ready for future expansion
- some testing shown that glass fibers can carry several terabits (1000 gigabits) per second
    - fiber-optic may 1 day replace copper for all types of network connections
![](https://i.imgur.com/okP43wd.png)

__Fiber-Optic Connectors__
- types
    - straight tip (ST)
    - straight connection (SC)
    - locking connection (LC)
    - mechanical transfer registered jack (MT-RJ)
    - fiber channel or ferrule connector (FC)
    - medium interface connector (MIC)
    - subminiature type A (SMA)
![](https://i.imgur.com/Nfn9z1y.png)

__Fiber-Optic Installation__
- more difficult & time consuming than copper media installation
    - however advances in connector tech closing gap
- connectors & test eq required for termination still more expensive than copper
- many methods for terminating fiber-optic cables due to many connectors & cable types available
    - installation details beyond scope of this book

__Fiber-Optic Cable Types__
- single-mode fiber (SMF)
    - includes single, small-diameter fiber at core 
        - 8 microns
    - generally works with laser-based emitters
    - longest dist
    - used in higher-bandwidth apps
- multimode fiber (MMF)
    - larger diameter fiber at core
        - 50 & 62.5 microns
    - cheaper than SMF
    - works with lower-power light emitting diodes (LEDs)
    - shorter dist


Structured Cabling
---
### Managing & Installing UTP Cable Plant
- structured cabling
    - specifies how cabling should be organised, regardless of media type or network architecture
    - large networks typically use most/all of these
        - work area
        - horizontal wiring
        - telecommunications closets
        - equipment rooms
        - backbone or vertical wiring
        - entrance facilities
- work area
    - where workstations & other user devices located
    - faceplates & wall jacks installed in work area
    - patch cable connect computers & printers to wall jacks
![](https://i.imgur.com/KdpzW3m.png)
- horizontal wiring
    - runs from work area's wall jack to telecomm closet
        - wiring from wall jack to patch panel should be no longer than 90 meters (plus 10m for patch cables)
- telecommunications closet
    - TC provides connectivity to computer equipment in nearby work area
    - typical eq includes
        - patch panels to terminate horizontal wiring runs
        - hubs
        - switches
    - TC that hosues cabling & devices for work area computers referred as __intermediate distribution frame (IDF)__
![](https://i.imgur.com/T0CVVmc.png)
- equipment room
    - houses servers, routers, switches & other major network equipment
    - serves as connection point for backbone cabling
        - eq room that's connection point between IDFs called __main distribution frame (MDF)__
        - MDF can be main cross-connect for entire network or serve as connecting point for backbone cabling between buildings
            - ea building has own MDF
- backbone cabling
    - interconnects IDFs & MDFs
    - runs between floors/wings of building & between buildings
    - frequently fiber-optic cable but can also be UTP if dist between TC is < 90m
- entrance facility
    - location of cabling & equipment that connects a corporate network to 3rd party telecomm provider
        - can also serve as eq room & main cross-connect for all backbone cabling
    - where WAN conection made
    - __demarcation point__ - point where corporate LAN eq ends & 3rd party provider's equipment & cabling begins

__Installing UTP Cabling__
- cable termination - putting RJ-45 plugs on ends of cable/punching down wires into terminal blocks on jack/patch panel
- tools needed
    - wire cutters
    - crimping tool
    - cable tester
    - punchdown tool
    - cable stripper
    - RJ-45 plugs/jacks
- when making cable/terminating cable at a jack or patch panel
    - important to get colored wires arranged in correct order
    - 2 standards: 568A & 568B

__Straight-Through VS Crossover Cable__
- standard patch cables called __straight-through cables__
    - same wiring standard on both ends
- __crossover cables__ - use 568A standard on 1 side & 568B on other
    - crosses transmit & receives wires so that transmit on 1 end connects to receive on other
    - this type of cable often needed when you connect 2 devices of same type to 1 another
    - for 1000BaseT crossover cable, have to cross blue & brown pins as used in 1000BaseT
![](https://i.imgur.com/HusbsNW.png)


Cable-Testing Equipment
---
- common tools for testing & troubleshotting wired networks
    - cable certifier
    - basic cable tester
    - tone generator
    - time domain reflectometer (TDR)
    - multimeter
    - optical power meter (OPM)


Wireless Networking
---
- demand increased considerably
    - many home users turn to wireless networks
- often used with wired to interconnect geographically dispersed LANs or groups of mobile users with wired servers & resources on wired LAN
    - AKA hybrid networks
- AP or router usually connects to internet via wired connection to cable modem though clients through wireless

### Wireless Benefits
- create temp connections to wired networks
- establishes backup/contingency connectivity for existing wired networks
- extends network's span beyond reach of wire-based or fiber-optic cabling
    - especially in older buildings where rewiring might be too ex
- allows businesses to provide customers with wireless networking easily, offering service that gets customers in & keeps them
- enables users to roam around a corporate/college campus with their machines
![](https://i.imgur.com/qMLlRYl.png)


### Types of Wireless Networks
- __local area networks (LAN)__
    - usually provides connectivity for mobile users or across areas that couldn't otherwise be networked
- __extended LANs__
    - usually used to increase LAN's span beyond normal dist limitations
- __internet service__
    - used to bring internet access to homes & businesses
- __mobile computing__
    - users communicate by using wireless networking medium that enable them to move while remaining connected

### Wireless LAN Components
- network interface attaches to antenna & emitter instead of cable
- transceiver/access point (AP) - transmitter /receiver device must be installed to translate between wired & wireless networks
    - includes antenna & transmitter to send & receive wireless traffic but also connects to wired side of network
    - shuttles traffic back & forth between network's wired & wireless sides

### Wireless LAN Transmission
- signals take form of waves in electromagnetic (EM) spectrum
- frequency of wave forms used for comm measured in cycles per second __(hertz HZ)__
- lower-frequency transmissions can carry less data more slowly over longer distances
    - higher-freq transmissions can carry more data faster over short dist
    - high freq radio waves has higher signaling rate
- common frequencies for wireless data comm
    - radio - 10Khz to 300Mhz
    - microwave - 300Mhz to 300Ghz
    - infrared - 300Ghz to 400Thz (terahertz)
- wireless LANs use 4 primary tech for transmitting & receiving data
    - infrared
    - laser
    - narrowband (single-freq) radio
    - spread-spectrum radio

Wireless LAN Technologies
---

### Infrared LAN Tech
- use infrared light beams to send signals between devices
    - works well for LAN apps due to high bandwidth
    - 4 main kinds
        - __line-of-sight networks__ - require unobstructed view between transmitter & receiver
        - __reflective wireless networks__ - broadcast signals from optical transceivers near devices to central hub
        - __scatter infrared networks__ - bounce transmissions offwalls & ceilings to deliver signals
        - __broadband optical telepoint networks__ - provide broadband services

### Laser-Based LAN Tech
- also need clear line of sight between sender & receiver
- subject to many same limitatons as infrared
    - aren't as susceptible to interference from visible light sources as infrared

### Narrowband Radio LAN Tech
- use low-powered, 2 way radio comm
- receiver & transmitter must be tuned to same freq to handle incoming/outgoing data
- need no line of sight between sender & receiver as long as both stay within broadcast range
    - 70m or 230 feet
- depending on freq, walls or solid barriers can block signals
- interference from other radio sources possible
![](https://i.imgur.com/nrTAQ4t.png)

### Spread-Spectrum LAN Tech
- uses multiple freq simultaneously, improving reliability & reducing susceptibility to interference
    - also makes eavesdropping more difficult
- 2 main kinds
    - freq-hopping - switches data between multiple freq at regular intervals
    - direct-sequence modulation - breaks data into fixed-size segments called __chips__
        - transmits data on several diff freq at once
![](https://i.imgur.com/zg6f9fS.png)


LAN Media Selection Criteria
---
- 3 main media choices: UTP, fiber-optic & wireless
- when choosing consider
    - bandwidth - higher = more expensive & higher installation costs
        - if >40gbps, fiber-optic only choice
    - budget
        - typical UTP cable installation costs $100 to $200 per cable run
        - fiber-optic costs twice
        - wireless has no phy installation costs but need to install access points & verify connectivity
    - environmental considerations
        - how electrically noisy?
        - how important is data security?
        - more weight factor has, more likely fiber-optic/secured wireless is right choice
    - span
        - what dist must network span?
        - longer spans need fiber-optic or wireless to use between buildings
        - strategic placement of small switches/hubs give UTP surprising reach
    - existing cable plant
        - for upgrade, existing cable plant must be considered
![](https://i.imgur.com/HDQNg2B.png)


Chapter Summary
---
![](https://i.imgur.com/FUIpG6d.png)
![](https://i.imgur.com/Wc3wvvR.png)




###### tags: `NETF SEM 2` `DISM SEM 2` `School` `Notes`