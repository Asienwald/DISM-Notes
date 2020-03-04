---
title: 'Lecture 08 Organisational Security'
disqus: hackmd
---

:::info
ST1004 Infocomm Security
:::

Lecture 08 Organisational Security
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


Business Continuity
---
- business continuity - org's abi to maintain operations after disruptive event
- business continuity prepardness involves
    - business continuity planning
    - business impact analysis
    - disaster recovery planning

### Business Continuity Planning (BCP)
- BCP is process of
    - identifying exposure to threats
    - creating preventative & recovery procedures
    - testing them to determine is sufficient
- consists of 3 essential elements
    - business recovery planning
    - crisis management & comms
    - disaster recovery

### Business Impact Analysis (BIA)
- BIA - identifies business funcs & quantifies impact a loss these funcs may have on business operations
- range from impact on
    - property - tangible assets
    - finance - monetrary funding
    - safety - phy protection
    - reputation - status
    - life - wellbeing
- BIA help determine __mission-essential func__
    - activity that's core purpose of enterprise
- BIA can help identify __critical system__
    - support mission-essential func
- identify __single pt of failure__
    - which component/entity will disable entire system if not functioning?
    - minimise these single failure pts result in high availability
- many BIAs contain __privacy impact assessment__
    - used to identify & mitigate privacy risks

#### Privacy Threshold Assessment
- determine if system contains __personally idenfiable info (PII)__

### Disaster Recovery Plan (DRP)
- DRP - focus on protecting & restoring info tech funcs
- written documen detailing process for restoring IT resources
    - follow disruptive event
- comprehensive in scope
    - detailed doc updated regularly
- most DRPs
    - have common set of features
    - cover specific topics
    - need testing for verification

#### Features
-  Typical Outline of DRP
    - unit 1 - purpose & scope
    - unit 2 - recovery team
    - unit 3 - preparing for disaster
    - unit 4 - emergency procedures
    - unit 5 - restoration procedures

#### Topics
- sequence in restoring systems - __order of restoration__
    - which systems have priority & restored first?
- what shld be done if disaster make current location unavail to process data
    - alt processing site must be identified
    - __failback__ - process of resynch data back for primary location

#### Testing
- disaster exercises designed to test effectiveness of DRP
    - objectives
        - test efficiency of interdepartmental planning & coordination in managing disaster
        - test current DRP procedures
        - determine resp strengths & weaknesses
- __tabletop exercises__
    - simulate emergency situation but in informal & stress-free env
- after-action report shld be generated
    - abalyse exercise results to identify strengths to be maintained & weakness to be improved

![](https://i.imgur.com/K7WC4IV.png)


Fault Tolerance Through Redundancy
---
- fault tolerance - system;s abi to deal with malfunctions
- solution to fault tolerance is __redundancy__
    - use of duplicated eq to improve availability of system
    - goal to reduce __mean time to recovery (MTTR)__
        - average amt of time taken for device to recover from failure that's not terminal
- redundancy planing
    - applies to
        - servers
        - storage
        - networks
        - power
        - sites
        - data

### Servers
- servers
    - key role in network infrastructure
    - failure have significant business impact
- clustering
    - combine 2 or more devices to appear as single unit
- server cluster
    - multiple servers appear as single server
    - connected through public & private cluster conns
    - types
        - asymmetric
        - symmetric

#### Asymmetric Server Cluster
- standby server performs no func except be ready if needed
    - used for
        - db
        - msging systems
        - file & print services

#### Symmetric Server Cluster
- all servers do useful work
    - if 1 server fails, remaining servers take on failed server's work
    - more cost effective
    - used for 
        - web
        - media
        - VPN servers

![](https://i.imgur.com/eSbvE9Y.png)


### Storage
- storage
    - trend to use solid state drives (SSDs)
        - SSD more resistant to failure
            - more reliable than HDDs
        - HDDs often 1st component to fail
        - some orgs keep spare hard drives
- mean time between failures (MTBF)
    - average time until component fails & must be replaced
    - used to determine num of spare hard drives org shld keep


- Redundant Array of Independent Devices (RAID)
    - uses multiple hard disk drives to increase reliability & perf
    - can be implemented through software/hardware
    - several lvls of RAID exists
        - lvl 0 - striped disk arr w/o fault tolerance
            - striping partitions hard drive into smaller sections
            - data written to stripes alternated across drives
            - if 1 drive fails, all data on drive lost
        - lvl 1 - mirroring
            - disk mirroring used to connect multiple drives to same disk controller card
            - action on pri drive duplicated on other drive
            - pri drive can fail & data wont lost

        - disk duplexing
            - variation of RAID lvl 1
            - separate cards used for ea disk
            - protect against controller card failures
        - lvl 5 - independent disks with distributed parity
            - distirbute parity (error checking) across all drives
            - data stored on 1 drive & parity info stored on another drive
        - lvl 0+1 - high data transfer
            - nested lvl RAID
            - mirrored array whose segments are RAID 0 arrays
            - can achieve high data transfer rates

![](https://i.imgur.com/6nAGDGQ.png)


### Networks
- redundant networks
    - needed due to critical nature of connectivity today
    - wait in bg during normal operations
    - use replication scheme to keep live network info current
    - auto launch in event of disaster
    - hadrware components duplicated
    - some orgs contract with 2nd ISP as backup
- software defined networks (SDNs)
    - SDN controller can increase network reliability & lessen need for redundant eq

### Power
- maintaining power essential when planning redundancy
- uninterruptible power supply (UPS)
    - maintain power to eq in event of interruption in pri electrical power src
- offline UPS
    - least expensive
    - simplest
    - charged by main power supply
    - begin supplying power quickly when pri power interrupted
    - switches back to standby mode when pri power restored
- online UPS
    - always running off batt when main power run batt charger
    - not affected by dips/sags in voltage
    - can serve as surge protector
- UPS systems comm with network OS to ensure orderly shutdown
    - but can only supply power for limited time
- backup generator
    - powered by diesel, natural gas or propane

### Recovery Sites
- reocver sites - backup sites needed if disaster dmgs buildings
    - 3 types of redundant sites
- hot site
    - run by commercial disaster recovery service
    - duplicate of production site
    - has all needed eq
    - data backups can move quickly to hot site
- cols site
    - provide office space
    - customer must provide & install all eq needed to continue operations
    - no backups immediately avail
    - less expensive than hot site
    - longer to resume full op
- warm site
    - all eq installed
    - no internet/telecomms facilities
    - no current data backups
    - less expensive than hot site
    - time to turn on conns & install backups can be half day/more
- growing trend - use cloud computing tgt with sites
    - backup apps & data to cloud
    - if disaster, restore to hardware in 1 of 3 sites

### Data
- data backup - copy info to diff medium & storing at off-site location
    - so can be used during disaster
- involves
    - data backup calculations
    - using diff types of data backups
    - off-site backups
- 2 elements used to calculating when backup performed
    - __recovery pt objective (RPO)__
        - max time org can tolerate between backups
    - __recovery time objective (RTO)__
        - time taken to recover backup data

#### Types of Backups
![](https://i.imgur.com/bs46PGJ.png)

- more comprehensive backup tech is __continuous data protection (CDP)__
    - perform continuous backups that can be restored immediately
    - maintain historical record of all changes made to data
    - create snapshot of data
        - like reference marker

#### Off-Site Backups
- 321 backup plan
    - shld always have 3 diff copies of backups on 2 diff storage media & 1 backups shld be stored at diff locations
- most org store off site backup using online cloud
    - often use CDP to continually backup data
- many internet services that provide such features
    - auto continuous backup
    - universal access
    - delayed deletion
    - online/media-based restore
- legal implications of off-site backups
    - pri issue is data sovereignity
        - data stored in digital format subject to laws of country whr storage facility resides
- orgs shld identify cloud services provider whose data center locations ensure it fully complies with all applicable data sovereignity laws


Environmental Controls
---
- methods to prevent disruption through env controls
    - fire suppression
    - electromagnetic disruption protection
    - proper config of HVAC systems

### Fire Suppression
- attempt to reduce impact of fire
- requirements for fire
    - fuel/combustible material
    - enough oxygen to sustain combustion
    - enough heat to raise material to ignition temp
    - chemical reaction - fire itself
- in server close/room that contain comp eq
    - stationary fire suppresion system recommended

![](https://i.imgur.com/s2O51Za.png)
![](https://i.imgur.com/aA2PHbf.png)


### Electromagnetic Disruption Protection
- electromagnetic interference (EMI)
    - caused by short duration burst of energy by src called __electromagnetic pulse (EMP)__
- electromagnetic compatibility (EMC)
    - reducing/eliminating unintentional generation, spread & reception of electromagnetic energy
    - goal is correct op of diff types of eq that func in same electromagnetic env
- faraday cage
    - metal enclosure that prevent entry/escape of electromagnetic fields
    - often used for testing in electronic labs

### HVAC
- data centers have special cooling needs
    - more cooling needed for larger num of systems generating heat in confined area
    - precise cooling needed
- heating, ventilating & air conditioning (HVAC) systems
    - maintain temp & relative humidity at needed lvls
- controlling env factors to reduce electrostatic discharge
- hot aisle/cold aisle layout
    - used to reduce hear by managing airflow
    - servers lined up in alternating rows with cold air intakes facing 1 dir & hot air exhausts facing other dir


Incident Response
---
- when unauth incident occurs
    - immediate resp needed
- incident resp
    - use forensics & incident resp procedures

### Forensics
- forensic science
    - apply science to legal qns
        - analyse evidence & apply to tech
    - computer forensics
        - use tech to search for computer evidence of crime
- importance of comp forensics
    - amt of digital evidence
    - increased scrutiny by legal profession
    - higher lvl of comp skills by criminals

#### Forensic Procedures
- 5 steps
    - secure crime scene
    - preserve evidence
    - establish chain of custody
    - examine evidence
    - enable recovery

### Incident Response Plan (IRP)
- IRP - set of written instructions for reacting to security incident
- incident resp process - 6 steps
    - preparation
    - identification
    - containment
    - eradication
    - recovery
    - lessons learnt

- minimally, IRP shld have
    - documented incident definitions
    - cyber-incident resp teams
    - reporting requirements/escalation
    - exercises


Chapter Summary
---
![](https://i.imgur.com/v4wfWII.png)
![](https://i.imgur.com/Zw9O5xy.png)
![](https://i.imgur.com/TZthJ4k.png)



###### tags: `ISEC SEM 2` `DISM SEM 2` `School` `Notes`