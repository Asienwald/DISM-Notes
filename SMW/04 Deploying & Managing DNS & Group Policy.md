---
title: '04 Deploying & Managing DNS & Group Policy'
disqus: hackmd
---

:::info
ST2612 Secure Microsoft Windows
:::

Topic 04 Deploying & Managing DNS & Group Policy
===

<style>
img{
/*     border: 2px solid red; */
    margin-left: auto;
    margin-right: auto;
    width: 90%;
    display: block;
}
</style>


## Table of Contents

[TOC]

Implementing Microsoft DNS 
---
- dns - tcp/ip app protocol that enables dns server to resolve
    - __forward lookup__ - domain to ip
    - reverse lookup - ip to domain/comp name
- dns server - provide dns namespace for enterprise
    - requirement for AD to have
        - installed as server role in win server 2016
        - need to config elements like zones in dns
- windows server dns most compatible with AD
    - non-microsoft servers must be compatible with ad
    - microsoft-based dns provide more info to help domain clients locate DCs and GCs

### DNS Zones
- dns name resolution enabled through tables of info that links comp names & ip
    - called __zones__
        - contains resource records
- __forward lookup zones__
    - link comp name to ip
    - holds hostname records called __address records__
    - most dns queries handled based on res records from this zone
- __reverse lookup & stub zones__
    - later
- note
    - in ipv4 host record called __host address (A) resource record__
        - ipv6 called __ipv6 host address (AAAA) resource record__
    - when install dns on DC, forward lookup zone auto created with dns server's addr record entered
    - use DNS manager to manage dns zones

#### DNS Resource Records
- host
    - link comp/network host name to ip
- canonical name (CNAME)
    - link alias to computer name
- load balancer
    - spreads load of dns lookup requests among multiple dns servers for faster resolution for clients and better network response
- mail exchanger (MX)
    - provides ip of simple mail transfer protocol (SMTP) servers that can accept emails in a domain
- Name servers (NS)
    - provides info on secondary dns servers for an authoritative server
    - and info on off-site pri servers that are not authoritative in the domain
- pointer record (PTR)
    - associates ip addr to comp/network host name
- service (SRV) locator
    - associates particular tcp/ip service to server tgt with its domain & protocol
- start of authority (SOA)
    - 1st record in zone
    - indicates if server is authoritative for current zone
- windows internet naming service (WINS)
    - forwards lookup request for netbios name to wins server when hostname cannot be found in dns
- windows internet naming service reverse (WINS-R)
    - forwards reverse lookup request to wins server
![](https://i.imgur.com/6YhYs9l.png)

### Using DNS Dynamic Update Protocol
- microsoft dns AKA __Dynamic DNS (DDNS)__
    - modern form of dns that enables client comps & dhcp servers to auto register ip addr
- dns dynamic update protocol
    - enabled info in dns server to auto update in coordination with dhcp
- after configuring dns
    - make sure configed to secure dns dynamic update protocol
        - saves admin time since dont need manually regsiter ea new workstation/new ip lease issued
    

![](https://i.imgur.com/6NEu7SO.png)

- based on security by default example, dynamic updates only allow "secure only" transactions
    - only info from trusted parties accepted
    - can lower to nonsecure, secure, none etc.

![](https://i.imgur.com/xBSQGQG.png)
- by default windows dhcp server enables ddns updates at scope lvl if running ad


### DNS Replication
- primary dns server
    - main administrative server for zone
    - authoritative server for zone
- secondary dns server
    - contains copyt of pri dns server's zone db
        - but not used for administration
        - also not authoritative
    - obtains copy of zone db through zone transfer over network
    - vital services
        - make sure always have copy of pri dns server's data
        - enable dns load balancing among pri & secondary servers
        - let secondary dns face & ans queries from public network
        - reduce congestion in 1 part of network
- if AD have 2 or more dcs
    - set up microsoft dns services on at least 2 of dcs
- __note__
    - dns replication not working in multi-master mode
        - zone data updates only on pri dns
    - secondary dns cannot replace pri
    - only authorised secondary dns can request zone transfer from master
    - replication process protects transfer data using auth & encryption

### How does DNS Queries Work?
- client requests local dns for name to ip addr resolution
- local dns give ans when
    - its authoritative server for domain
    - local dns has required info from its cache
- when local dns dont have ans
    - lookup ip of corr authoritative server from one of "root" servers
        - root servers addr are built-in to dns installation
            - also see __root hints servers__ and __top level dns servers__
            - though now more commonly used __recursive lookup__ approach - based on forwarded dns 
        - involves multiple rounds of inquiries
        - local dns acts as client to visit multiple authoritative dns to get final ans
        - AKA __iterative lookup__
    - once actual authoritative server identified,
        - local dns contacts remote dns directly & gets required info

### Stub Zone
- has only bare necessities for dns funcs which are copies of following
    - SOA record zone
    - name server (NS) records to identify authoritative servers 
    - record for name servers that are authoritative
- 1 common use to quickly resolve comp names between 2 namespaces
- zone transfer privilege
    - local dns needs zone transfer privilege granted from target dns that owns forward zone
    - Eg cannot setup stub zone for google.com unless local dns has privilege granted from authoritative dns of google.com
- __note__
    - stub zone is inline with iterative lookup approach
        - can skip root hints & top lvl dns servers & visit authoritative dns
    - fastest way to find ans (aside from local cache) but needs manual setup for indiv domains
        - local dns must also obtain zone transfer privilege from targeted dns
        - hence only applicable to enterprises with multiple domains

### Additional DNS Server Roles
#### Forwarder Approach
- common to designate 1 dns to forward name resolution requests to specific remote dns
- dns forwarding can be setup if dns server that receives forwarded request cannot resolve name
    - server that originally forwarded request attempts to resolve via other ways
    - AKA __nonexclusive forwarding__
- win server 2016 supports use of forwarder & root hints
    - though root hints may be blocked by higher lvl ISP for security measure
- __note__
    - local dns simply forwards query that cant resolve to higher lvl dns
        - only relays back ans to own clients
    - local dns can setup multiple forwarders
        - when all forwarders cannot provide ans, local dns can use root hints approach

![](https://i.imgur.com/BNBjhls.png)
- local dns in west college received dns query
    - forwards query to common dns forwarder server
    - this common dns forwarder server may not host any zone data, but accepts queries from all subdomains
- main duty is to keep local cache of all popular queries & ans
    - also forward new queries to upper lvl dns (commission network) to get ans from internet

![](https://i.imgur.com/ZelEf8z.png)
- dns properties setup menu at its management console
    - can define 1/more forwarders in forwarders tab

#### Caching Server
- dns server can func as caching server
    - provide fast queries as results stored in RAM
- dns server w/o zones is caching-only server
    - caching-only server queries pri or secondary dns & cache results to provide fast response for next identical query
    - used to reduce num of secondary server & reduce extra network traffic
- limitations
    - take time for ea to build up comprehensive set of resolved names to ip
    - sometimes need to flush dns server cache
- __note__
    - in practical, .2 addr of nat acts as virtual dns forwarder to resolve dns queries
    - .2 only relays queries to host machine's upper lvl dns to complete dns lookup

### Forwarder VS Root Hints
- both have pros and cons in terms of operational concerns or security concerns
    - forwarder
        - faster - resursive query
            - try to provide ans
            - possibly non-authoritative
        - local dns has no way to ensure security config of external forwarder
        - potential to enable customizable dns service within enterprise for security enhancement at dns lvl
            - Eg. dns filtering, logging
    - root hints
        - slower due to interactive queries
            - try to provide best ans
        - more reliable
            - 13 root hints supported by >200 actual load-balancing servers
- __note__
    - we prob cant use root hints approach since connection to internet is non-business plan
        - ISP won't allow conn to send direct request to any root hint servers
    - Root hints are a list of the DNS servers on the Internet that your DNS servers can use to resolve queries for names that it does not know
        - if local dns cannot resolve dns data, send to root hints

### Creating DNS Implementation Plan
- best practice
    - implement winserver2016 dns servers instead of other vers of dns & use AD
    - res records & zones setup for ipv4 can be setup for ipv6
    - use namespaces to rep natural org boundaries
    - ensure dns servers on priv network well secured in winserver2016 security options
    - plan to locate dns server across most site links
    - create 2 or more dns servers to take advantage of load balancing, __multi-master__ r/s (with AD-integrated zones) and fault tolerance
    - designate 1 dns server as forwarder to reducd traffic
    - num of dns servers setup can be related to analysis of org
    - if have multiple servers used for 1 app use round robin to distrbute load
        - only applicable to namespace with cluster setup
    - if branch location with read-only domain controller (RODC) needs local dns services as too many users, make rodc secondary not pri dns server
        - unidirectional replication (compromised rodc wont spread malicious updates)
        - not caching any passwords on rodc
- note
    - setup secondary dns as read only domain controller
        - RODC do not necessarily be more robust or secure than norm dc
    - advantage of rodc 
        - rodc carries less sensitive info 
        - cause less dmg to AD if compromised
        - rodc is best suit for deploying to site/branch that we cant ensure logical & physical security


### DNS Enhancement in Win Server 2016
- dns grp policies for
    - filtering malicious ip & redirect malicious clients to dead end rather than their target
    - redirecting clients to specific data sources/servers according to time of day
    - managing client access to acc for high traffic situations
    - directing clients to best scr for specific app
- abi for dns to work with client comps that have >1 NIC
- new powershell cmdlets for configing dns

### Troubleshooting DNS
- steps
    - restart dns server & dns client services
    - check for recent log errs related to dns

![](https://i.imgur.com/ENy2WGu.png)
![](https://i.imgur.com/xoY9Obn.png)
- DNS client service
    - sometimes dns issue might be client side

### DNS Threats
- enterprise admins watch out for following
    - ddos with dns amp atk
        - bogus queries sent to dns to trigger it to send high vol of replies to victim
    - cache poisoning
        - dns cache/stub zone/forwarder compromised, causing dns to return incorrect ip, diverting traffic to atker's comp
    - registrar hijacking
        - AKA domain hijacking
            - act of changing registration of domain w/o perm of orig registrant
        - done in several ways
            - generally by exploiting vuln in domain name registration system/social engineering
- note
    - amp atk easier on dns due to nature of protocol
    - cache poisoning can be found at many diff lvls in dns operations
        - common effect is for impersonation atks
            - lead victim to trust fake sites/msgs
    - registrar hijacking is another form of cache poisoning but at higher lvl

### Securing Windows DNS Server
- interfaces
    - limit ip addr that dns server service listens on to ip that clients use for the dns server
    - by default it listens on all addr
![](https://i.imgur.com/ewZSGQ3.png)


Using Microsoft Baseline Security Analyser
---
- mbsa - tool to scan windows comps for security holes
    - compares comp's settings against microsoft's released patches & listed vulns
    - runs on win2k3, 2k7, server 2012 r2 & server 2016
- provides streamlined method to identify missing security updates & common security misconfigs
    - mbsa 2.3 release adds support for win 8.1, 8, server 2012 r2 & server 2012
- microsoft security compliance toolkit 1.0 (SCT)
    - new set of tools for win10 & server 2019
- mbsa checks following desktop app params
    - internet explorer security zone settings per local user
    - outlook security zone settings per local user
    - office products security zone settings per local user
- for mbsa to be run on multiple machines remotely, must enable
    - server service, remote registry service, file & print sharing
    - may disable all by default & use grp policies to enable them prior to routine mbsa scan for entire network/subnet
- note
    - lots of users might misunderstand its usage & funcs
        - tool not for reporting if machine missed few updates
        - mbsa is bpa for client system
            - help identify common misconfigs of client based on set rules
    - microsoft provided new set of MSC toolkit for latest client system
        - mbsa still good as provide remote scanning abi

### Application
- mbsa applicable to following microsoft products
    - win vista, 7, 8, 8.1, 2k3, 2k8, 2012 r2
    - internet info services (IIS)
    - sql server 2012
    - internet explorer 5.01 or later
    - exchange
    - windows media player 6.4 & later
    - microsoft office
    - microsoft data access components (mdac)
    - msxml
    - microsoft virtual machine
    - commerce server
    - content management server
    - sharept server
    - host integration server

![](https://i.imgur.com/NqptMUw.png)
- features that mbsa provides

Microsoft Security Compliance Manager
---
- utility to enable automation of deployment & monitoring baseline compliance
    - another security hardening tool
    - operations fully integrated with AD & GPOs
- key features & benefits
    - download security baselines from microsoft
    - compare & customise security baselines
    - export baselines in formats (Eg. XML, GPOs)
- note
    - msc provides baseline updates
        - these baselines can be applied for diff vers of windows servers & clients
        - specific baselines avail for systems with diff roles

![](https://i.imgur.com/F7TytjD.png)
![](https://i.imgur.com/VviP8cN.png)


Overview of Security Features in WinServer 2016
---
- create to emphasise on security
    - reduced atk surface of kernel through server core & nano server
    - expanded & evolving grp policies
    - windows firewall
    - windows defender
    - security templates & security config & analysis tools
    - user acc control
    - bitlocker drive encryption
- server core/nano server can be good solution for server that handles critical network operations (Eg. DNS & DHCP)
    - also good for web/other servers in demilitarised zone (DMZ) of network
        - dmz = portion of network between 2 networks (Eg. private & internet)
        - comps in dmz have fewer security def via routers & firewalls
    - offer better perf & fewer probs
- grp policy
    - way to bring consistent security & other management to winserver2016 & clients connecting to server
- windows firewall & ipsec
    - settings merged for consistency
- windows defender
    - software that scans for malware
    - winserver2016 is 1st win server OS to have win defender
- security templates & security config & analysis tools
    - enable to config server-wide security
- user acc control (UAC)
    - designed to keep user running in standard user mode as way to
        - fully insulate kernel
        - keep OS & desktop files stabilised
    - another element is Admin Approval Mode
        - prevents malware/intruder from acquiring control through backdoor w/o admin knowing
- bitlocker drive encryption
    - prevents intruder from bypassing acl file folder protections


Introduction to Group Policy
---
- grp policy in win server 2016
    - enable you to standardise working env of clients & servers by setting policies
- defining characteristics of grp policy
    - can be set for site, domain, OU or local comp
    - cannot be set for non-OU folder containers
    - settings stored in grp policy objs
    - can be local/non local
    - can setup to affect user accs & comps
    - when updated, old policies removed/updated for all clients

### Config Settings
![](https://i.imgur.com/Yans5Cc.png)
![](https://i.imgur.com/RzPML9J.png)


Securing WinServer2016 Using Security Policies
---
- sec policies are subset of indiv policies
    - within larger grp policy for site/domain/OU/local comp
- security policies include
    - acc policies
    - audit policy
    - user rights
    - security options
    - ip sec policies

### Establishing Account Policies
- acc policies
    - applies to all accs/all accs in container when AD installed
- options you can config affect 3 main areas
    - password security
    - acc lockout
    - kerberos security

#### Password Security
- 1 option to set passwd expiration period, requiring users to change passwords at regular intervals
- some orgs require all passwds to have min length
- specific passwd sec options
    - enforce passwd history
    - max/min password age
    - min passwd length
    - must meet complexity requirements
    - store passwd using reversible encryption

#### Account Lockout
- OS can employ acc lockout to bar access to acc (includes true acc owner) after num of unsuccessful tries
    - commonly 5-10 tries
- lockout can be set to release after period of time
    - or intervention from server admin
- acc lockout params
    - acc lockout duration
    - acc lockout threshold
    - reset acc lockout count after
- mainly for prevention of brute force on passwd
    - may create opportunity for dos atks

#### Kerberos Security
- involve use of tickets exchanged between client who requests logon & network services & server/AD that grants access
    - when AD used, ea dc is key distribution center
    - one user authenticated, kerberos ticket-granting service granst permanent ticket (called __service ticket__) to comp
        - service ticket good for duration of logon session
- enhancements on winserver 2016 & win10
    - use of advanced encryption standard (AES) encryption
    - when AD installed, acc policies enable kerberos
        - when AD not installed, default auth through windows NT LAN manager ver 2 (NTLMv2)
- responsible for AD user auth 
    - key component to support res access management
- options avail for configing kerberos
    - enforce user logon restrictions
    - max lifetime for service tix/user tix/user tix renewal
    - max tolerance for comp clock synchronisation
    - note
        - these options directly affect security lvl of kerberos options
        - longer lifetime of these prams imrpvoe system perf but increase risk of atks

### Establishing Audit Policies
- examples of events that org can audit
    - acc logon/logoff events
    - acc management
    - dir service access
    - logon/logoff events at local comp
    - obj access
    - policy change
    - privilege use
    - process tracking
    - system events
- system logging provide essential data for system audit & monitoring operations
    - although log monitoring operations considered passive defensive measure, cannot underestimate usefulness on detecting anomaly caused by potential threats

### Configuring User Rights
- user rights enable acc/grp to perform predefined tasks
    - most basic right is abi to access server
    - more advanced rights give privileges to create accs & manage server funcs
    - can be easily mixed up with res perms
- 2 general categories of rights
    - privileges
        - abi to manage server/AD funcs
    - logon rights
        - how accs, comps & services accessed

#### Examples of Privileges
![](https://i.imgur.com/lK055uj.png)
- perms & user rights work tgt
    - some operational task might need both to carry out tasks

#### Examples of Logon Rights
![](https://i.imgur.com/RRJMU10.png)

### Configuring Security Options
- many specialised security options divided into following categories
    - accs
    - audit
    - DCOM
    - devices
    - domain controller
    - interactive logon
    - microsoft network client
    - network access
    - network security
    - recovery console
    - shutdown
    - system cryptography
    - system objects
    - system settings
    - user acc control

### Settings Under User Configuration
![](https://i.imgur.com/fHBGOyg.png)

Policy Application Order & Troubleshooting
---
- policies can be applued at domain lvl, OU lvl etc.
    - any settings that dont conflict with other settings applied
    - what if settings conflict?
        - http://www.rebeladmin.com/2018/01/deal-group-policy-conflicts/
- in win server 2003 & prev vers, settings related to acc policies can only be set at domain lvl
    - from win server 2008, can have diff password policies & acc lockout policies for diff OUs
    - dont need to rmb old and outdated settings
- note
    - every GPO has same num of possible system configs setting entries
        - ea of these entries can be in 1 of 2 states - defined or undefined
        - dc can send defined entries to target machine so sending GPO wont need a lot of network bandwidth
    - policy settings conflicts only occur when 2 diff GPOs have defined same entires (but diff definitions) & both received by same domain client system


### Group Policy Predence
- impt to understand order in which settings in grp policy configed
- usual order appplied is __LSDOU - local, site, domain & OU__
    - settings that conflict applied based on usual order of application
        - last setting applied become effective
- Policy Application Order AKA Grp policy precedence determines final winner of GPO conflicts

#### Example
- policy at domain lvl states that only admins can shutdown comps
- policy at sales OU lvl states that admins & mgr1 can shutdown comps
![](https://i.imgur.com/EL7iIUV.png)
- comps not in SalesOU wont receive GPO hence Mgr1 only have shutdown privilege on certain comps

### Special Configuration Options
- blocking grp policy inheritance
    - container option
        - prevent from inheriting GPO
    - enforced
        - gpo options
            - force down to all child containers & win all setting conflicts (take highest precedence)
    - multiple grp policy link order setting
    - [Read More](https://blogs.technet.microsoft.com/musings_of_a_technical_tam/2012/02/15/group-policy-basics-part-2-understanding-which-gpos-to-apply/)
- note
    - blocking inheritance & enforced gpo may override/alter norm policy app order effect
    - blk inheritance is container option
        - enforced gpo is attribute of gpo

### More Examples
![](https://i.imgur.com/Xgzw8TG.png)
![](https://i.imgur.com/xhq1f1O.png)
![](https://i.imgur.com/XXv7jxq.png)
![](https://i.imgur.com/NrfdQIn.png)
![](https://i.imgur.com/zVGV6mT.png)

#### Avoid Complexity in Group Policies
- limit num of grp policy objs
    - can single domain policy apply to all?
- minimise use of blk inheritance & enforced to avoid complexity

### Resulttant Set of Policy (RSoP) & gpresult
- rsop
    - make implementation & troubleshooting of grp policies simpler for admin
    - can query existing policies in place & provide reports & results of policy changes
    - rsop supports 2 modes
        - planning
        - logging
    - avail within GMPC & command line interface
- gpresult
    - cmd run to check current accepted & active GPOs




###### tags: `SMW` `DISM` `School` `Notes`