---
title: 'Lecture 05 Troubleshooting & Support'
disqus: hackmd
---

:::info
ST1010 Networking Fundamentals
:::

Lecture 05 Troubleshooting & Support
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

Documenting Your Network
---
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
- phy & logical addressing, connectivity to devices & data abt cabling shld be documented

#### Documentatin & IT Staffing
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
- doc security patches & virus protection updates helps you adhere to security policies & cfm your resistacne to current threats

### Change Management
- when workstation moved, must know which patch panel & switch ports used so they can be disconnected
    - w/o doc, cables must be traced
- additions to network faster & lesser chance for erros if doc up to date
- change management - document reasons for changee, potential impact for change, notifs & approval procedures

### What to Document?
- descrip of network
    - include netowkr topology, tech in use, OS installed, num of devices & users served
- cable plant
    - describes phy layout of network cabling, terminations used, conventions used for labeling cable & eq & results of test completed on ea cable plant
- eq rooms/telecomms closets
    - doc items in ea room & location
- internetworking devices
    - know which devices connected to which, networking management features, port usage, phy & logical addr, model nums & hardware/software revision nums
- servers
    - doc hardware config, OS & app ver num, NIC info & system serial & model nums
- workstations
    - hardware & software config, phy & logical addr


Problem Solving Process
---
- steps 
    - determine prob definition & scope
    - gather info
    - consider possible causes
    - device solution
    - implment solution
    - test solution
    - document solution
    - device preventative measures

### Step 1 - Determine Prob Definition & Scope
- prob def shld describe what works & what doesnt
    - know who & what affected by prob
- qns to ask
    - anyone else having same prob?
    - how abt other areas?
    - prob in 1 app or more?
    - does prob occur on diff comp?
- assign priority to prob once defined

### Step 2 - Gather Info
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

### Step 3 - Consider Possible Causes
- create checklist of possible things that could have gone wrong

![](https://i.imgur.com/I1IzM96.png)

### Step 4 - Devise Solution
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

### Step 5 - Implement Solution
- create intermediate testing opportunities
    - testing small steps in limited num of things can go wrong easier than testing complex solution with lots of prob areas
- inform users of possible disruption to network services
- put plan into action
    - take note of every change you make

### Step 6 - Test Solution
- testing shld emulate real-world situation
- if testing workstation prob
    - attempt to logon to network as user with similar privileges as main user
    - attempt to access apps that would run on workstation
- if testing network upgrade
    - start some workstations on upgraded part of network & run network-intensive apps
    - gather info abt how network behaves & compare with prev results (before upgrade)

### Step 7 - Document Solution
- include everything pertinent to prob
    - prob def
    - solution
    - implementation
    - testing
- if prob & solution have implications for entire network, include this info

### Step 8 - Devise Preventive Measures
- after solving prob, do everything you can to prevent this prob/similar probs from recurring

![](https://i.imgur.com/gTaUfsY.png)

- devise preventive measures is proactive rather than reactive network management


Approaches to Network Troubleshooting
---
- diff methods
    - trail & error
    - solve by example
    - replacement method
    - step by step with OSI model

### Trial & Error
- require assessment of prob, educated guess to solution & test of results
- used under following conditions
    - system newly configed, no data can be lost
    - system not attached to live network
    - can undo changes easily
    - other approaches take more time than few trail & error attempts
    - few possible causes to prob
    - no doc & other res available to draw on to arrive at a solution more scientifically
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

### Solve by Example
- process of comparing sth that doesnt work with sth that does
    - easiest/fastest ways to solve prob
- general rules
    - use approach only when working sample has similar env as prob machine
    - dont make config changes that will cause conflicts
        - dont change TCP/IP addr of nonworking machine to same addr as working machine
    - dont make changes that can destroy data that cant be restored

### Replacement Method
- need narrowing down possible srcs of prob & having known working replacement parts on hand so they can be swapped out
- follow these rules
    - narrow list of potentially defective parts down to few possibilities
    - make sure have correct replacement parts on hand
    - replace only 1 part at a time
    - if 1st replacement dont fix prob, reinstall orig part before replacing another part

### Step by Step with OSI Model
- test prob starting with app layer & keep testing ea layer until have successful test/reach phy layer
    - can also start at phy layer & work way up
- must understand how networks work & shld use troubleshooting tools


Problem-Solving Resources
---
- res avail
    - experience
    - internet
    - network doc

### Experience
- make most out of it
    - take notes abt what you see & learn
- if happened once, will happen again
    - dont think prob so obscure that wont happen again - take time to make not of it
- colleague's experience
    - use people as res
- experience from manufacturer's tech support
    - best time to call when you have specific err num or msg that can report to manufacturer
    - have software ver nums or hardware serial num avail when calling

### Internet
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

### Network Documentation
- doc shld read like user's manual for network admins
- network diagrams
    - include network diagrams showing logical pic of network & another diagram showing network phy aspects
        - Eg. rooms, devices, connections

![](https://i.imgur.com/L5i7XvI.png)
![](https://i.imgur.com/c741KJL.png)

- internetworking devices
    - need diff lvls of doc
        - simple, unmanaged switches need least info
    - shld include model & serial nums, locations, IP, MAC & num of ports (total & num of free ports)

![](https://i.imgur.com/NjLptAe.png)


Network Troubleshooting Tools
---
- common tools
    - ping & trace route
    - network monitors
    - protocol analysers
    - time domain relfectometer (TDR)
    - cable testers
    - additonal tools

### Ping & Tracert
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

### Network Monitors
- software packages that can track all/part of network traffic
    - can track packet type, errors & traffic to/from ea comp
    - can generate reports & graphs
    - some programs can email admins when prob detected

### Protocol Analysers
- protocol analysers allows you to capture packets & analyse network traffic generated by diff protocols
    - can be used to troubleshoot probs related to dns, auth, dhcp, ip addressing, remote access etc
    - also used to create baselines for network perf
- most advanced analysers combine hardware & software in self-contained unit
    - Eg. savvius (wildpackets), omnipeek, fluke network optiview network analyser, wireshark

### Time-Domain Reflectometer (TDR)
- used to determine whether there's break/short in cable & measure cable length
- TDR sends electrical pulse down cable that reflects back when encounter break or short
    - measures time takes for signal to return & can estimates how far down cable the fault located
- shld use TDR to document actual lengths of all cables

### Basic Cable Testers
- usually cost less than $100
- only test correct termination of twsited-pair cable/continuity of coaxial cable
- great for checking patch cables & testing correct termination at patch panel & jack
- cannot check for attenuation, noise or other possible perf probs

### Advanced Cable Testers
- more expensive than TDRs or basic cable testers
- performs several test for crosstalk, attenuation, EMI & impedance mismatches
- some advanced cable testers can measure frame counts, CRC errs & broadcast storms
- can cost from $1000 to several thousand dollars

### Additional Tools
- multimeter - can measure voltage, current & resistance on wire
    - resistance (impedance) measures opposition to electrical current & impt in determining faults
- tone generator & probe - generator issues an electrical signal & probe (tone locator) detects signal & emits tone
    - useful for locating wire that might be in bundle of wires
- optical power meter (OPM) - used to measure amt of light on fiber-optic circuit
    - often used to determine amt of signal loss on fiber-optic cable between transmitter (emitter) & receiver
    - amt of signal loss can determine whether the fiber-optic termination was done correctly & whether receiver can interpret signals correctly


Common Troubleshooting Situations
---
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


Disaster Recovery
---
- disaster can be anything from server disk crash to fire/flood
- section focus on
    - backup procedures
    - recovery from system failure

### Backing Up Network Data
- determine what data shld be backed up & how often
- develop schedule for backing up data
- identify people responsible for performing backups
- test backup system regularly
- maintain backup log listing what data backed up, when backed up, who performed backup & what media used
- develop plan for storing data after has been backed up

### Backup Types
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


#### Backup Schedule
- good model for creating backup schedule combines weekly full backup with daily differential backups
- when creating schedule, post schedule & assign 1 person to perform backups & sign off on them
- windows systems have extra backup type called __system state backup__
    - copies boot files, registry, active dir on domain controllers & other critical info

### Business Continuity
- consist of policies, procedures & res required to ensure business can func after major catatrophe
- if bulk of IT infrastructure maintained in house, company shld consider 1 of following
    - __cold site__ - phy location that house hardware needed to get IT functioning again
    - __warm site__ - location containing all infrastructure needed for operations to continue
    - __hot site__ - can be running at moment's notice


Chapter Summary
---
![](https://i.imgur.com/hNusV5S.png)
![](https://i.imgur.com/jjnLi7k.png)
![](https://i.imgur.com/Xj7pPr3.png)
![](https://i.imgur.com/aPJSrOt.png)



###### tags: `NETF` `DISM` `School` `Notes`