---
title: '01 Intro to Windows Server 2016'
disqus: hackmd
---

:::info
ST8091 Securing Microsoft Windows
:::

01 Intro to Windows Server 2016
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

Focus Areas
---
![](https://i.imgur.com/ixy04VS.png)


Secure Computing
---
### Needs for it
- types of threats
    - viruses, worms, programs that steal confidential info
    - hacking via system vulns
- sources of comp security probs
    - bad software design
    - bad implementation

- laws that hold management responsible for data breaches

![](https://i.imgur.com/zyxATIg.png)

- safe computing needs
    - change in behaviour of management, programmers & users
    - make secure computing a priority
    - write secure operating systems & apps
        - yet dont affect productivity
    - train users to always keep security in mind

### Microsoft's Commitment to Security
- areas to make investment
    - isolation & resiliency
    - updating
    - quality
    - access control & auth

#### Isolation & Resiliency
- features included
    - idea to split comp system into smaller pieces
        - make sure ea piece seperated from others so if compromised/malfunction wont affect other entities in system
    - implementations
        - firewalls
        - object lvl access control
        - etc
    - auto block unsolicted downloads & unwanted pop-ups from sites in browser
    - inclusion of better file attachment handling in outlook express & windows messenger instant messaging
    - compilation of core windows components with latest ver of compiler tech
    - intro to exchange edge services
        - designed for email protection, enhanced security & management of junk email for exchange customers
    - integrated set of protection technologies
        - Eg. __microsoft security essentials (MSE)__
            - windows defender (built-in)
    - smart screening tech
        - smart spam-filtering solution
    - client inspection tech
        - Eg. MBSA

#### Software Updates
- primary way to protect against software vulns
- microsoft monthly release of software updates
- variaous products incorporated by microsoft to make updates seamless include
    - __system center config manager (SCCM)__
        - formerly known as system management server (SMS)
    - __microsoft baseline security analyser (MBSA)__
    - __windows software update services (WSUS)__

#### Quality
- use of quality standards & processes
- use of best practices in all phases of software dev
- development of new internal tools that auto check code for common errors
- through testing of software before release

#### Access Control & Auth
- changes to improve access control & auth
    - passwords
    - smart cards
    - public key infrastructure (PKI)
    - internet protocol security (IPSec)
    - active dir rights management services (AD RMS)

Trustworthy Computing
---
- microsoft trustworthy computing memo
    - dev emphasis - security over features
- way to ensure safe & reliable computing

### Requirements
- comps need to be reliable
- software that operates machines must be equally reliable
- service components need to be dependable

### Dimensions where Microsoft's Objective of Trustworthy Computing Relies
- goals - to deliver
    - security
    - privacy
    - business integrity
- means
    - security be design, by default & by deployment 
    - privacy/fair info principles
    - availability, manageability & accuracy
    - usability, responsiveness & transparency

#### Microsoft Security Initiative Update 2015
![](https://i.imgur.com/bUbbQXn.png)

### Trusted Cloud 
- trustworthy computing is long term initiative
- currently expanding to cloud
- __trusted cloud initiative__
    - based on 4 foundational principles
        - security
        - privacy
        - compliance
        - transparency

![](https://i.imgur.com/NIUKwF8.png)

### Secure Code
- many steps taken to implement & maintain security
    - train windows engineers in
        - writing secure code
        - specialised testing techniques
        - threat modeling
    - write documentation with security in mind

#### Common Language Runtime
- runtime env for .NET framework
- manages running of .NET programs regardless of programming language
- goals for design
    - simplify dev env
    - simpler & safer deployment
        - get rid of concept of registry (using XML confi files instead)
        - use zero impact installation


Windows Server 2016 Editions
---
![](https://i.imgur.com/UvMu0EP.png)

### Windows Server 2016 Essentials Edition
- supports max of
    - 25 users
    - 16.8m connections for file sharing through __server message block (SMB)__ services
    - 2 central processor sockets
    - 50 remote desktop connections
    - 50 routing & remote access conns
- in addition
    - cannot join domain
        - can only migrate files & data from 1 server to another
    - provides most but not all server roles
        - dont provide role for hosting vms
        - cannot provide cloud services

### Windows Server 2016 Standard Edition
- provides
    - file & print services
    - secure internet conn
    - centralised management of users
    - centralised managements of apps & networks res
- new features
    - start btn & start menu back on desktop
    - active dir easier to setup
        - has improved file security
    - domain controller can be cloned to quickly create more domain controllers
    - __generic routing encapsulation (GRE)__ tunneling to enable virtual private networks to go over external networks
    - __desired state config__ used to monitor specific server states & roles so desired states dont change as other elements are changed on 1 or many servers

![](https://i.imgur.com/4IuL0tH.png)

- all editions of windows server 2016 compatible with common lang runtime used in
    - microsoft .NET framework
    - microsoft visual studio .NET
- another feature of standard edition
    - __clustering__ - ability to increase access to server res & provide fail-safe services by linking 2 or more comp systems so appear to func as one

![](https://i.imgur.com/O4jfbwv.png)



#### Hyper-V
- included
    - __Hyper-V__ - enables servers to offer virtualisation env

- improvements
    - faster cloning
    - migration of indiv vms
    - vm info stored in new file format that prptects vm info from being directly edited
- new to windows server 2016 is option to use __containers__
    - containers enable apps on 1 comp to run in isolated fashion with ability to execute multiple apps
    - 2 types
        - windows server containers
        - hyper-v containers


### Windows Server 2016 Datacenter Edition
- designed for envs with
    - mission-critical apps
    - very large db
    - very large virtualisation requirements
    - cloud computing needs
    - info access requiring high availability
- offers support for clustering up to 64 comps

- diff between standard & datacenter focus on datacenter's industrial strength capabilities in areas of
    - virtualisation
    - cloud computing
    - db handling
- datacenter dont come with db software
    - but designed to provide OS res to accomodate large db apps


Using Windows Server 2016 with Client Systems
---
- client OS most compatible with windows server 2016
    - windows 7, 8, 8.1 & 10
    - win10 most compatible in terms of client management

- overall goal of microsoft is to achieve lower total cost of ownership (TCO)
    - TCO is full cost of owning network
        - including hardware, software, training, maintenance & user support costs

### Linux Integration Services (LIS)
- windows server 2016 supports linux through LIS
    - enables linux clients to access linux vm in hyper-v
- new capabilities in LIS
    - new software for enhanced desktop graphics perf on linux clients
    - improved backup support funcs
    - creation of kernel dumps for linux vms
    - better control of avail ram in linux vms


### Advantages of using Windows Server 2016 with Windows 7-10
- enhanced capabilities to recover from many types of network comm probs
- comp code for more efficient network comms
- more network diagnostic capabilities
- comp code for better use of network comms protocols
- continuing upgrades for windows powershell commands & scripts in both Windows server 2016 & windows 7-10


### Terminology
- client
    - comp that accesses res on another comp via network
- workstation
    - comp that has own CPU & can be used as stand-alone or network comp
- domain
    - grping of network objs like comps, servers & user accs that provides for easier management
    - comps & users in domain can be managed to determine what res they can access
- active directory
    - db of comps, users, grp of users, shared printers, shared folders & other network res


Windows Server 2016 Features
---
- features include
    - server manager
    - security
    - clustering
    - enhanced web services
    - windows server core & nano server
    - windows powershell
    - virtualisation
    - reliability
    - multitasking & multithreading
    - phy & logical processors
    - containers

### Server Manager
- enable server admin to manage critical confi features from 1 tool
- used to
    - config server from beginning
    - view comp config info
    - change server roles & system properties
    - configure networking
    - configure remote desktop
    - configure security
        - includes firewall
    - add/remove features
    - run diagnostics
    - manage storage & backups
    - manage multiple servers from 1 place
- new features includes following advantages
    - local server option makes all local server properties avail to manage
    - multiple servers easier to manage from 1 place
    - servers can be grped so all servers in specific grp received 1 or more commands simultaneously
    - dashboard offers more quick-start guidance for setting 1 or more servers & establishing grpings used to manage specific kinds of servers
    - server manager GUI has new look with addedd features
        - greater ability to add & manage remote servers

### Security
- when installing windows server 2016, adding feature/installing windows component an essential lvl of security auto implemented
    - security be default
- other security features
    - file & folder permissions
    - security policies
    - encryption of data
    - event auditing
    - various auth methods
    - server management & monitoring tools

### Enhanced Web Services
- microsoft internet info services (ISS)
    - transforms windows server 2016 to versatile web server
- ISS designed to
    - include over 40 modules
        - intended to enable IIS to have lower atk surface
    - provide easier app of IIS patches
    - make it easier for network programmers to write network apps & config apps for web

### Windows Server Cor & Nano Server
#### Windows Server Core
- minimum server config
- designed to func similar to traiditional UNIX & linux servers
- dont provide
    - GUI, just command line
    - graphical tools to config server
    - extra services that you dont need
    - mouse pointer on screen
    - windows mail, microsoft word, search windows & other software

#### Windows Nano Server
- new installation option in windows server 2016
- smaller footprint than server core
- provides basic foundation for server computing
- intended to be faster & need less maintenance

- microsoft views nano server as platform to run a 
    - DNS/DHCP server
    - apps server
        - Eg. cloud web server
    - db or file server

### Windows Powershell
- cmd interface that offers shell
    - customised env for executing cmds & scripts
        - scripts - files that contain cmds to be run by comp OS
- can perform following tasks
    - work with files & folders
    - manage disk storage
    - manage network tasks
    - setup local & network printing options
    - install, list & remove software apps
    - view info abt local comp
        - including user accs
    - manage services & processes
    - lock comp/log off
    - manage IIS web services
- offers >130 cmd tools
    - called __cmdlets__

### Reliability
- OS kernel runs in privileged mode
    - protects from probs created by malfunctioning programs/process
- kernel consists of core programs & comp code of OS
- privileged mode gives OS kernel extra lvl of security from intruders
    - prevents system crashes from poorly written apps

#### Terminology
- process
    - comp program/portion of program that is currently running
- protected process
    - 1 for which outside influences restricted


Planning Windows Server 2016 Networking Model
---
- network - comms system enabling comp users to share comp equipment, app software & data, voice & vid transmissions
    - contains comps joined by comms cabling or sometimes by wireless devices
- workstation/client network OS
    - enabled individual comp to access network & share res
- peer-to-peer networking
    - focus on spreading network res admin among server & non-server members of network
- server-based networking
    - centralises network administration on 1/more servers

![](https://i.imgur.com/WtlxIzk.png)

### Peer-to-Peer Networking
- use workstations to share res like files & printers & connect to res on other comps
    - no special comp needed to enable workstations to comm & share res
- effective for small networks
    - dont need server setup or active dir services
- disadvantages
    - management of network res decentralised
    - as network gets bigger, admin more difficult
    - lack of security of res

### Server-based Networking
- server
    - single comp that provides extensive multiuser access to network res
    - can handle hundreds of users at once
        - fast response when delivering shared res
        - less network congestion when multiple workstations access that res
    - advantages
        - users only need to logon once to gain access to network res
        - security strongers
        - all members can share comp files
        - printers & other res can be shared
        - all members can have email & send msgs to other office members through email server
        - software apps stored & shared in central location
        - impt db can be managed & secured from 1 comp
        - all comps can be backed up easier
        - comp res sharing can be arranged to reflect work patterns of grps within org
        - server admin can save time when installing software upgrades


Protocols for Windows Server 2016 Networking Model
---
- protocol consists of guidelines of following
    - how data formatted into discrete units called packets & frames
    - how packets & frames transmitted across 1 or more networks
    - how packets & frames interpreted at receiving end
- packets & frames
    - units of data transmitted from sending comp to receiving comp
- windows server 2016 & clients primarily use the __Transmission Control Protocol/Internet Protocol (TCP/IP)__
    - suite of protocols & utilities that support comm across LANs & internet
- local area network (LAN)
    - network of comps in relatively close proximity

### Transmission Control Protocol (TCP)
- TCP
    - reliable end-to-end delivery of data by controlling dataflow
    - comp agree on "window" for data transmission that includes num of bytes to be sent
    - window constantly adjusted to acc for existing network traffic
- TCP also considered connection-oriented comm
    - ensures packets delivered
    - delivered in right sequence
    - contents accurate

### Physical Address & Address Resolution Protocol (ARP)
- ARP
    - used to acquire phy addr associated with comp's NIC
- every NIC has phy/MAC addr
- for comps to comm with ea other must know MAC of ea other's NIC
- proper comm using TCP/IP rely on both IP & MAC addr
- every comp running windows server 2016 has ARP cache
    - contains recently resolved MAC addr & statically assigned values in ARP cache
    - arp -a cmd shows contents of ARP cache

![](https://i.imgur.com/glOzbqK.png)


### Implementing TCP/IP in Windows Server 2016
- 2 tasks
    - verifying its enabled
    - configuring it
- enabling TCP/IP
    - activity 1-6 - verify TCP/IP & NIC enabled
- configuring TCP/IP
    - activity 1-7 - configuring TCP/IP for static addressing

### Automated Address Configuration
- __automatic private ip addressing (APIPA)__
    - used to auto config TCP/IP settings for comp w/o using DHCP server
    - comp auto assigns itself IP from reserved range of 169.253.0.1 & 169.254.255.254 & subnet of 255.255.0.0
    - appropriate for small orgs that have only 1 network segment & dont need to access another network/internet
- auto config can be disabled through windows server 2016 registry
    - __registry__
        - db used to store inof abt config, program setup, devices, drivers & other data impt to setup windows OSes
- dynamic addressing through DHCP server
    - common for medium-sized & large networks
    - must 1st install & config DHCP server on network
    - in addition to assigning IP, DHCP can also assign subnet, default gateway & other IP settings
    - using DHCP server can save a lot of administrative effort


Summary
---
![](https://i.imgur.com/mR4jTLb.png)

![](https://i.imgur.com/I0cM5LT.png)









###### tags: `SMW` `DISM` `School` `Notes`