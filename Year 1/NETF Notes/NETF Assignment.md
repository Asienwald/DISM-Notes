---
title: 'NETF Assignment'
disqus: hackmd
---

:::info
ST1010 Network Fundamentals
:::

NETF Assignment
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
- Rest & Relax Designs Pte Ltd - company that provides residential & commercial interior design services

### Staff Breakdown
- 90 staffs
    - 1 CEO
    - 2 directors
    - 3 dep directors
    - 15 office admin staff
    - 2 IT staff
    - 22 senior interior designers
    - 45 interior designers
- considerations
    - projects handled by 1 interior designer or grp of designers
        - interior designers often need to access ea others' work to effectively work on projects
            - in their own subnet with network data folders
    - CEO, directors, dep directors and designers need access to designs & documents from home
        - cloud storage?
    - data security is major concern - designs & docs shld not be accessible to other people on internet
        - in their own private org network
    - staff need facility to print their designs, bills, invoices etc.
        - printing room - another network

### Company Layout
- leased 5 units at Bell Towers
- occupies
    - 1 unit on lv6
    - 2 units on lv7
    - 2 units on lv8

![](https://i.imgur.com/zfAU5ki.png)

### Project Scope
- allow flexibility in following areas
    - file & print services
    - internet access
        - definitely wireless lan
    - remote access to office network
        - [Remote-Access VPN](https://computer.howstuffworks.com/vpn3.htm)
    - security
    - data backup
    - network scalability
    - high availability/fault tolerance
    - any other services beneficial to company

Task
---
- report to propose network setup for company
    - not more than 8 pages

![](https://i.imgur.com/6FKrzBD.png)

### Benefits of having a network in the Company
- reliable way of sharing information and resources within an org
- file sharing
    - easily share data between diff users or access it remotely
- resource sharing
    - share peripherals like printers and scanners between the org
    - saves money as don't need to buy one for each room
- share internet connection
    - cost-efficient
    - can protect the system as a whole if you properly secure the network
- increase storage capacity
    - can acces files/folders remotely on other machines/network-attached storage
    - don't have to use your own physical storage

- shared access to customer/product databases
    - handle more customers in lesser time (improve productivity)
- centralised admin management
    - all handled centrally, easy to maintain and troubleshoot
    - less IT support needed (lesser manpower)
- all staff works from single source of information
    - reduce errors
    - improve consistency

- Access Flexibility 
    - Portable Business with wireless system connectivity
    - Move laptops or tablets during meetings (no constrains of movements)

- Reduce cost on Software 
    - Purchase single license for a particular software and run it on the server. Individual computers within that network can run the software w/o installing a seperate license


### Suitable Internet Access Plan
![](https://i.imgur.com/RjTe2Bq.png)
https://www.singtel.com/business/promotions/sitex-show-offers-2019/business-fibre-broadband-offers#sme-security-pack

- 300mbps  - adequate bandwidth for a small office to browse internet and access emails and services
- comes with 4G wireless network
    - personnel can use their devices and stay connected wireless anywhere in the office - convenient (seamless connectivity)
- has automatic 4G wireless backup and a backup & disaster recovery solution
    - handy when systems go down and their designs are saved

__Find 2 more from ea big ISP and make comparison!__

---
### Proposed Network Setup

#### Network Topologies
- star in star/pt to multiple topology
- switched logical topology

#### Protocols
- basic data communication
    - HTTPS for web
    - TCP/IP
    - UDP
- security protocols - implement security over network comms
    - HTTPS
    - SSL - encryption layer
    - SFTP - secure file sharing
- network management protocols - network governance & maintenance
    - ICMP
    - SNMP - for mail
- SSH for remote access to workstations
- DHCP for dynamic IP addressing


#### Communication Media
- wired
    - use fiber-optic [single mode fiber] for cables connecting networks separated by level (since its more than 90m)
        - level 6, 7 and 8
    - use shielded twisted pair for networks in same level
        - #07-123 and #07-125
        - #08-123 and #08-125
- wireless
    - use wireless access point
    - 5ghz and not 2.4ghz
        - 5ghz has smaller range but faster data rate compared to 2.4ghz
            - higher freq, higher bandwidth
        - since has one AP in each network, don't need huge range
        - better security too, since no leakage of wireless network

---
### Hardware recommendations

#### Router
Model C1111-8P 

The router is ideal for small and medium enterprise branch providing 1 WAN port and 8GE LAN ports. It has remote configuration and management,risk mitigation with multilevel security and high performance to run concurrent services.

Price: $878.57(incl of GST)
https://www.cisco.com/c/en/us/products/routers/1000-series-integrated-services-routers-isr/compare-model.html

https://www.router-switch.com/c1111-8p.html 


#### Switches
Model S3900-48T4S

The reason why we choose this specific switch is because it has up to 176Gbps switching capacity. It also have 4 built-in 10G SFP+ ports for stack and uplinks which improves link reliability through redundant to achieve high-availabilty. Furthermore, the switch can contain 16K MAC addresses and jumbo frame of 9K.

Price: $638.79(incl of GST)
https://www.fs.com/sg/products/72946.html?currency=SGD&paid=google_shopping&gclid=EAIaIQobChMI5tvJ0L-C5wIVmh0rCh1Z2gsmEAQYASABEgKKLPD_BwE


#### Wireless Access Points
Model FS-AP1167C

The chosen Access Point delivers both 2.4GHz and 5GHz bands each with two dedicated spetial stream that support two single-user multiple input multiple output (2.4GHz) as well as two multi-user multiple input multiple output(5GHz). It can serve a maximum of 248 devices with a transmission rate up to 1167Mbps, providing 32 SSIDs. 

Price: $159.43(incl of GST)
https://www.fs.com/sg/products/84027.html

#### Workstations
Model ThinkStation P330Tiny 

The reason why we chose this model is because it has Intel Core i3-8100T Processor (6MB Cache, 3.10GHz) which is relatively fast to handle multiple computer's process and a memory of 4GB DDR4 2666MHz SoDIMM. Double Data Rate processes data approximately twice as fast as a standard memory module, and currently DDR4 is the latest module.

Price: $1,199.00 (incl. GST)
https://www.lenovo.com/sg/en/deals/workstation-offer/


#### PC
Model Yoga C740 (14" inch)

The reason why we choose this model is because it is equipted with 10th Generation Intel, Core i7-10510U processor supporting 1.80GHz to 4.90GHZ turbo boost, with 4 Cores and 8MB cache.

It has 16GB memory space and up to 4TB SSD PCle along with 14 inch full high definition IPS, touchscreen, antiglare and 300nits with Dolby Vision. The given spectrum is suitable for office work. 

Price: $800 (incl. GST)
https://www.lenovo.com/us/en/laptops/yoga/700-series/Lenovo-Yoga-C740-14/p/88YGC701292

Model MacBook Pro (16" inch 2.6GHz 6-Core Processor 512 GB Storage AMD Radeon Pro 5300M) 

We chosw this model for the designers as it has a 16-inch Retina display with True, a ToneTurbo Boost up to 4.5GHz, AMD Radeon Pro 5300M with 4GB of GDDR6 memory, 16GB 2666MHz DDR4 memory and 512GB SSD storage.These are essential to process multiple graphics programs simultaneously.

Price: $$3,499.00 (Incl. GST)

https://www.apple.com/sg/shop/buy-mac/macbook-pro/16-inch

#### Printers
Model MFC-L8900CDW (x10)

The reason why we choose this model is because it can support wireless transmission such as IEEE 802.11b/g/n  either Infrastructure or  Ad-Hoc mode IEEE 802.11g/n for peer-to-peer transmission. 

It also provide LAN transmission for 10Base-T,100Base-TX and 1000Base-T. For instance where the wifi is down, employess can still print the materials needed. 

Near Field Communication feature is available allowing users within range to connect and exchange data easily.

Fax and broadcast up to 350 location with Modem speed of 33,600bps

Price S$1,088 (incl of GST)
https://www.brother.com.sg/en/products/all-printers/printers/mfc-l8900cdw

#### File Servers
Model ReadyNAS 214

It has faster file backups and access up to 200 Mbps read and 160 Mbps write speeds also, storing up to 24 TB of storage with four available bays. It is suitable for streaming and data backup for multiple users which is perfect for a small business enterprise. Furthermore, in the scenario where there is a power loss, the server is able to auto shutdown and auto-restart on power recovery with their system monitoring, 

Price: $911.35 (Incl. GST)
https://sg.rs-online.com/web/p/nas-drives/1218152?cm_mmc=SG-PLA-DS3A-_-

#### Cables
Model 9/125μm Single Mode Bend Insensitive Fiber Optic Cable

The reason we chose this is because when bent or twisted lesser attenuation is lost as compared to tradition fiber optic cable which is makes installation and maintenance of fiber optic cables more efficient.

By using Single Mode Fiber Cable it can transport data for up to 10km at 1310nm, or up to 40km at 1550nm.(high transmission speed)

Length 30m, Price: $18.19(incl of GST)
https://www.fs.com/sg/products/40206.html

Model Cat6 Snagless UTP Cable 24AWG, 1000Base-T

We chose this snagless cable as it can be used to connect computer and various network components. The 8 cores are twisted in 4 pairs, and each core is twisted by 7 strands of Oxygen-free Copper wire, ensuring the stability of signal transmission thus, effectively counteracting the cross-talk. Lastly, FS Cat6 patch cables pass the Fluke Channel Test

Length 30m, Price: S$ 34.37 (Incl. GST)
https://www.fs.com/sg/products/70733.html (UTP cat6)

Model Cat6a Snagless Shielded (SFTP) PVC CMX Ethernet Network Patch Cable

The shielded foiled twisted pair prevents the cables from RFI/EMI and cross-talk interference. It is ideal for a noisy, RFI/EMI or highly confidential environment. The PVC CMX keeps the cable durable, safe and fire retardant.

Length 30m, Price: S$ 35.75(Incl. GST)
https://www.fs.com/sg/products/64200.html(SFTP cat6)


### Patch Panels
Model RS PRO Cat6 24 Port RJ45 RJ Patch Panel STP 1U Black

We chose this model as it has rear cover to improve shielding and protect terminals, LSA style termination blocks also, with easy field label systems and port identification providing integral cable management. 

Price: $161.02 (incl. GST)
https://sg.rs-online.com/web/p/rj-patch-panels/0557183

Model RS PRO Cat6 24 Port RJ45 RJ Patch Panel UTP 1U Black

The shuttered patch panel has dual block 110 and LSA style terminations. With easy field label system
and port identification.

Price: $180.77 (incl. GST)
https://sg.rs-online.com/web/p/rj-patch-panels/0556635

---

### Software recommendations

- Adobe Creative Cloud
    - all 20+ apps (Photoshop, Illustrator, Premiere etc)
    - https://www.adobe.com/sea/creativecloud/plans.html

- Blender
    - for 3D designs
    - https://www.blender.org/about/license/

- Microsoft Office
    - for basic admin work like excel, word etc
    - https://www.microsoft.com/en-sg/p/office-365-business/cfq7ttc0k62t?activetab=pivot%3aoverviewtab

- VPN service 
    - for remote access to company network
    - https://www.starhub.com/business/products-and-services/data-connectivity/connecting-internationally/global-vpn/benefits.html

- Antivirus - Malwarebytes Endpoint Protection
    - Company antivirus software to keep the workstations safe
    - https://www.malwarebytes.com/pricing/business/

- Cloud software - Google Drive Enterprise
    - Cloud storage allows for employees to store their data there and increase security as it acts as backup
    - https://cloud.google.com/drive-enterprise/

---
### Additional Info 
- Security issues
    - switch port security
- Staff training
- future explansion plan


### Network Diagram
![](https://i.imgur.com/vFRx8bJ.png)

- wires connecting each level's switches to the main router will run through ceilings
- file servers will be located in physically in #06-123
- each room will have more than 5 workstations (even though diagram only shows 5)
    - specific amount to be decided later
- internet access plan allows for a built-in VPN hence allowing designers to access the company network remotely from home
- router connecting to internet has firewall to prevent unwanted internet traffic from entering the compppany's network


#### Room Allocation
- 06-123
    - contain file servers
    - all 15 office admin staff
        - no reason to put them tgt with designers
    - 1 IT staff
        - look after file servers
            - be thr first if anything goes wrong
        - can move between lvl 6 and 7 swiftly if anything goes wrong
- 07-123
    - 7 senior int designers
    - 13 int designers
- 07-125
    - 6 senior designers
    - 13 int designers
- 08-123
    - CEO, directors and dep directors
        - 6 total
        - put them tgt as they prob need regular meetings & interactions
    - 3 senior interior designers
    - 6 interior designers
- 08-125
    - 6 senior designers
    - 13 int designers
    - 1 IT staff
        - can move swiftly between lvl 7 or 8 if anything happens
---
### Hybird Network

We are using Hybrid Network for our Network Design Proposal. A hybrid network uses both wireless and wired connection for a network. The reason why we chose hybrid network is because it is scalable and flexible...

### Advantages of Wired Network
- Reliable
    - prevent eavesdropping, not susceptible to interference (fiber-optic)
    - Resolved connection dropped issues
- Higher/Faster internet speed
    - No signal attenuation 
    - 
- Increased security
    - Cannot be easily intercepted since there is no transmission of medium (air waves) involved. 

### Advantages of Wireless network
- Access and Availability 
    - Allows users to communicate on the move within the same network area. 
- Cost Saving
    - Cheaper and easier to install
- Flexibility
    - Employees can continue with their work from home without needing a dedicated computer

---
Appendix
--- 
*INSERT IMAGES*

---
Resources
---
- https://securenetworksitc.com/small-business-network-setup
- [Tool to draw Network Diagram](https://www.conceptdraw.com/How-To-Guide/LAN-Diagrams)
- [PDF file with a lot of info](https://www.scte.org/documents/pdf/CCNA4%20Sample.pdf)
    - a lot of information but very long
- https://www.nibusinessinfo.co.uk/content/benefits-computer-networks
- https://www.inspiredtechs.com.au/computer-networking/
- https://oit.colorado.edu/software-hardware/software-downloads-and-licensing

### Internet Access Plans
- https://blog.moneysmart.sg/budgeting/best-fibre-broadband-singapore/
- https://www.singtel.com/business/products-services/connectivity/internet
    - https://www.singtel.com/business/products-services/connectivity/internet/fibre-broadband-dynamic-ip

- https://www.starhub.com/business/promotions/fibre-broadband-promotions.html?cid=ps-122B-SEM_AlwaysOn_BB_Gen_BMM-201902-alwayson-BusinessInternet_promotions&utm_medium=Paid_Search&utm_source=alwayson&utm_campaign=SEM_AlwaysOn_BB_Gen_BMM&utm_content=BusinessInternet_promotions&gclid=EAIaIQobChMIpfLM1cav5gIVmB0rCh3dQwVtEAAYASAAEgKidPD_BwE&gclsrc=aw.ds



###### tags: `NETF SEM 2` `DISM SEM 2` `School` `Notes`