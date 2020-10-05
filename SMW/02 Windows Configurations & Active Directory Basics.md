

02 Windows Configuration & Active Directory Basics
===




## Table of Contents

- [02 Windows Configuration & Active Directory Basics](#02-windows-configuration---active-directory-basics)
  * [Using Server Manager](#using-server-manager)
    + [Installing & Remove Server Roles](#installing---remove-server-roles)
    + [Best Practices Analyser (BPA) for Server Roles](#best-practices-analyser--bpa--for-server-roles)
      - [Guidelines](#guidelines)
      - [General Steps](#general-steps)
  * [Using System File Checker](#using-system-file-checker)
    + [Verify System & Critical Files with Sigverif](#verify-system---critical-files-with-sigverif)
  * [Understanding the Windows Server 2016 Registry](#understanding-the-windows-server-2016-registry)
    + [Data contained in Registry](#data-contained-in-registry)
    + [Precautions when Working with Registry](#precautions-when-working-with-registry)
  * [Registry Contents](#registry-contents)
    + [HKEY_LOCAL_MACHINE](#hkey-local-machine)
    + [HKEY_CURRENT_USER](#hkey-current-user)
    + [HKEY_USERS](#hkey-users)
    + [HKEY_CLASSES_ROOT](#hkey-classes-root)
    + [HKEY_CURRENT_CONFIG](#hkey-current-config)
    + [Backing up Registry](#backing-up-registry)
  * [Active Directory Basics](#active-directory-basics)
    + [Understanding Active Dir](#understanding-active-dir)
      - [Schema](#schema)
      - [Global Catalog](#global-catalog)
      - [Namespace](#namespace)
    + [Active Directory Structure](#active-directory-structure)
    + [Containers in Active Directory](#containers-in-active-directory)
      - [Forests](#forests)
      - [Tree](#tree)
      - [Domain](#domain)
      - [Organisational Unit (OU)](#organisational-unit--ou-)
      - [Site](#site)
    + [Active Dir Guidelines](#active-dir-guidelines)
  * [Security Configuration Wizard](#security-configuration-wizard)
    + [SCW Can...](#scw-can)
    + [Components](#components)

Using Server Manager
---
- server manager
    - consolidates administrative funcs to make server easier to manage
    - mainly 2 panels

### Installing & Remove Server Roles
- server roles & associate features
    - for ea server role
        - diff role services to choose to include/omit
- 2 common roles for windows server 2016
    - file & storage services
        - focus on sharing files from server or using server to coordinate & simplify file sharing through __distributed file system (DFS)__
    - print & document services role
        - used to manage network printing services & can offer 1/more network printers connected to network through server itself

### Best Practices Analyser (BPA) for Server Roles
- once installed role & setup
    - impt to determine that followed best prac for role
- can run BPA to determine if 1 / more roles installed & configed to follow guidelines recommended by Microsoft
- when probs found, analysis of ea role shows 3 lvls of severity
    - information
    - warning
    - error

#### Guidelines
- config
- security
- predeployment
- postdeployment
- performance
- BPA requisites

#### General Steps
![](https://i.imgur.com/6d0NjLa.png)


Using System File Checker
---
- system file checker
    - scan system files for integrity
    - run to
        - scan all sys files to verify integrity
        - scan & replace files as needed
        - scan only certain files
    - can be manually run from cmd or powershell
        - need admin
        - `sfc /scannow`

### Verify System & Critical Files with Sigverif
- sigverif verifies syst & crit files to determine if they have a signature
    - only scans files 
    - dont overwrite inappropriate files
        - hence can use tool when users logged on
    - results written to log file `sigverif.txt`
    - if tools finds file w/o signature that you believe need to be replaced
        - can replace file when users off system


Understanding the Windows Server 2016 Registry
---
- windows server 2016 registry
    - complex db with all info OS needs abt entire server
    - registry is coordinating center for specific server
- registry editor launched from `win + R` as regedit

### Data contained in Registry 
- info abt hardware components
- info abt windows server 2016 services installed
- *data abt user policies & win server 2016 grp policies
- data on last current & last known setup used to boot comp
- config info abt all software in use
- software licensing info
- server manager & control panel param configs

### Precautions when Working with Registry
- establish specific grp of admins with privileges to open & modify regsitry
- only make changes to registry as last resort
- regularly backup registry as part of backing up server 2016 windows folder
- nvr copy over registry from 1 windows-based system over registry of diff system

Registry Contents
---
- hierarchical in structure
    - made up of keys, subkeys & entries
- registry key
    - category/division of info within registry
- regsitry subkeys
    - single key may contain 1 or more lower-lvl keys
- registry entry
    - data param associated with software/hardware characteristic under key/subkey
- root key
    - can be shortcut to subkey
    - primary/highest lvl cat of data contained in registry
    - total 5 root keys

### HKEY_LOCAL_MACHINE
- HKEY_LOCAL_MACHINE root key
    - contains info on every hardware component in server
    - includes info abt drivers loaded & ver lvls
    - what IRQ lines  used, setup configs, BIOS ver & more
- few subkeys stored as set
    - called __hives__
    - hold related info

### HKEY_CURRENT_USER
- HKEY_CURRENT_USER root key
    - contains info abt desktop setup for acc signed in to server role
    - alias for HKEY_USERS\ logged on user's hive

### HKEY_USERS
- HKEY_USERS root key
    - contains profile info for ea user who has logged onto comp
    - ea profile listed under this root key
- within ea user pfoile is info identical to that within HKEY_CURRENT_USER root key
    - profile used when signed in is 1 of profiles stored in HKEY_USERS

### HKEY_CLASSES_ROOT
- HKEY_CLASSES_ROOT key
    - holds data to associate file exts with programs
    - alias for `HKEY_LOCAL_MACHINE\Software\Classes`
- associations exist for exe files, txt files, graphic files, clipboard files, audio files etc
    - associations used as defaults for all users logged in

### HKEY_CURRENT_CONFIG
- HKEY_CURRENT_CONFIG root key
    - info abt current hardware profile
    - info abt monitor type, keyboard, mouse, other hardware characteristics for current profile

### Backing up Registry
- before working with registry shld backup
    - easy way create restore pt
        - use `Checkpoint-Computer cmdlet` in powershell
    - if registry damaged can go back to restore pt


Active Directory Basics
---
- active dir
    - dir service that hosue info abt all network res 
        - Eg. servers, printers, user accs, grps of user accs, security policies etc.
- dir service
    - responsible for providing central listing of res & ways to quickly find & access specific res
    - provide way to manage network res
- win server 2016 uses active dir to manage accs, grps & more network management services

- domain controllers (DC)
    - server that have AD DS server role installed
    - contain writable copies of info in active dir
- member servers
    - servers on network managed by active dir that dont have active dir installed
- domain
    - container that holds info abt all network res grped within it
    - every res called obj

![](https://i.imgur.com/4PMl8iL.png)

- multimaster replication
    - ea DC equal to other DC in that it contains full range of info that composes active dir
    - if info on 1 DC changes its replicated to all other DCs
- active dir built to make replication efficient
- active dir in win server 2016 can
    - replicate indivi properties instead of entire accs
    - replicate active dir on basis of speed of network link
- 3 general concepts for understanding active dir
    - schema
    - global catalog
    - namespace

### Understanding Active Dir

#### Schema
- active dir schema
    - defines obj & info pertaining to those objs (attributes) that can be stored in active dir
    - Eg. obj classes
        - user accs
        - comps
        - grps
- caveat
    - replication between DCs require involved parties to be having identical active dir schema

![](https://i.imgur.com/4Zt7ADO.png)

#### Global Catalog
- global catalog
    - stores info abt every obj within forest
    - 1st DC configed in forest becomes global catalog server
        - have option of configuring another DC to be global catalog server 
        - or designating multiple DCs as global catalog servers
- global catalog server
    - stores full replica of every obj within its own domain & partial replica of ea obj within every domain in forest
    - enables forest-wide searches of data
- serves following purposes
    - central storehouse of key pbj info in forest with multiple domains
    - provide lookup & access to all res in all domains
    - provide rpelication of key active dir elements
    - keeping copy of most used attributes for ea obj for quick access 

#### Namespace
- active dir uses domain name system (DNS)
    - must be DNS server on network that active dir can access
- namespace
    - logical area on network that contains dir services & named objs
    - has abi to perform name resolution
- active dir depends on 1 or more dns servers
- active dir employs 2 kinds of namespaces
    - contiguous namespace
        - child obj contains name of parent obj
    - disjointed namespace
        - child obj dont resemble name of parent obj
        - eg. parent is `university.edu` while child is `researchcompany.com`

![](https://i.imgur.com/Omlgv6g.png)

### Active Directory Structure
![](https://i.imgur.com/OSZmBne.png)


### Containers in Active Directory
- active dir has treelike structure
- hierarchical elements AKA __containers__
    - forests
    - trees
    - domains
    - org units (OUs)
    - sites

![](https://i.imgur.com/q3OA2w2.png)

#### Forests
- forest
    - consists of 1 or more active dir trees in a common r/s
- have following characteristics
    - trees use disjointed namespace
    - all trees use same schema
    - all trees use same global catalog
    - domains enable administration of commonly associated objs
        - Eg. accs & other res within a forest
    - 2 way transitive trsust are automatically configured between domains within single forest

![](https://i.imgur.com/1wVUcJ0.png)

- forest provides means to relate trees that use contiguous namespace in domains within ea tree
    - but have disjointed namespace in r/s to ea other
- advantage of joining trees into forest
    - all domains share same schema & global catalog
- forest functional lvl
    - refers to active dir funcs supported forest-wide

- types of forest functional lvls recognised by win server 2016 active dir

![](https://i.imgur.com/Fvaq7ju.png)

- when servers upgraded, might make sense to raise forest func lvls to match server OSes in use

![](https://i.imgur.com/una8it5.png)

#### Tree
- tree
    - contains 1 or more domains in common r/s
- following characteristics
    - domains rep in contiguous namespace
        - can be in hierarchy
    - 2 way trust r/s exist between parent & child domains
    - all domains in single tree use same schema for all types of common objs
    - all domains use same global catalog
- domains in tree typically have hirarchical structure
    - eg. root domain at top & other domains under root
- domains within tree is in a __kerberos transitive trust r/s__
    - consists of 2 way trusts between parent domains & child domains
    - because of the trust r/s, any domain can have access to the res of all others

![](https://i.imgur.com/We64zsY.png)

#### Domain
- microsoft views domain as logical partition within active dir forest
    - domain is grping of objs that typically exists as primary container within active dir
- basic funcs of domain
    - provide active dir "partition" in which to house objs that have common r/s, particularly in terms of management & security
    - establish set of info to be replicated from 1 DC to another
    - expedite management of set of objs

![](https://i.imgur.com/OpyaRq9.png)

- domain functional lvls
    - refers to win server OSs on DCs & domain-specific funcs they support

![](https://i.imgur.com/B56DYMN.png)


#### Organisational Unit (OU)
- org unit (OU)
    - offers way to achieve more flexibility in managing res associated with business unit, department or div
        - not possible through domain admin alone
    - OU is grping of related objs w/o domain
        - allow grping of objs so can be administered suing same grp policies
    - can be nested within OUs

- 3 concerns when planning to create OUs
    - recommended to limit OUs to 10 lvls or fewer
    - active dir works more efficiently when OUs set up horizontally instead of vert
    - creation of OUs involves more processing res as ea request through OU needs CPU time

![](https://i.imgur.com/AtoBeHU.png)

#### Site
- site
    - tcp/ip based concept/container within active dir linked to ip subnets
- site has following funcs
    - reflects 1 or more interconnected subnets
    - reflects phy aspect of network
    - used for DC replication
    - used to enable client to access DC that's phy closest
    - composed of only 2 types of objs, servers & config objs
- sites based on connectivity & replication funcs
- reasons to define a site
    - enable client to access network servers using most efficient phy route
    - DC replication most efficient when active dir has info about which DCs in which locations
- advantage of creating site
    - it sets up redundant paths between DCs
        - paths used for replication

- bridgehead server
    - DC designated to have role of exchanging replication info
    - only 1 bridgehead server set up per site

![](https://i.imgur.com/Y7eLLb1.png)


### Active Dir Guidelines
- keep active dir as simple as possible
    - plans structure before implementation
- implement with least num of domains possible
    - with 1 domain being ideal & building from thr
- implement only 1 domain on most small networks
- use OUs to reflect org's structure
- create only num of OUs that are absolutely necessary
- dont build active dir with >10 lvls of CPU
- use domains as partitions in forests to demarcate commonly associated accs & res governed by grp & security policies
- implement multiple trees & forests only necessary
- use sites in situations whr there's multiple IP subnets & multiple geographic locations
    - as means to improve logon & DC replication perf

Security Configuration Wizard
---
- security config wizard (SCW)
    - very useful security tools for win server 2008-2012 R2
    - steps you through analysing & configuring security settings on server
- SCW examines roles a server plays
    - then tries to adjust security settings to match these roles
    - unlike BPA, SCW allows admin choice of applying the adjustment immediately or not

### SCW Can...
- disable unnecessary services & software
- close network comm ports & other comm res that aint in use
- examine shared files & folders to help manage network access through access protocols
- configure audit policy

### Components
- 3 components
    - GUI interactive wizard
    - database
    - cmd tool called `scwcmd`
- __security configuration database (SCD)__ is grp of XML files that establish security policy

![](https://i.imgur.com/RvfvaVE.png)
![](https://i.imgur.com/iJuOYGS.png)
![](https://i.imgur.com/0flAwje.png)



###### tags: `SMW` `DISM` `School` `Notes`