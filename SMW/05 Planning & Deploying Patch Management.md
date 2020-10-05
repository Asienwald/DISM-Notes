---
title: '05 Planning & Deploying Patch Management'
disqus: hackmd
---

:::info
ST2612 Securing Microsoft Windows
:::

Lecture 05 Planning & Deploying Patch Management
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

Planning the Deployment of Service Packs & Hotfixes
---
- need to keep tech env secure & reliable
    - need identifying security vulns & responding quickly
- patch management
    - method for keeping comps up to date with new software releases
- security patch management
    - patch management with concentration on reducing security vulns
    - essential for secure IT management & operations
    - vital for system security
- NOTE
    - security patch management shld be continuous and well-established process
        - though costly
    - well-planed strategy required for every org to keep security patch management process cost-effective


Managing Updates
---
- microsoft update and automatic updates
    - auto downloads & install latest updates from microsoft windows updates services
- windows server update services (WSUS)
    - setup centralised & local update service at enterprise level
- microsoft endpoint manager
    - comprise many config tools
    - microsoft system centre config manager (SCCM)
        - including software deployment management
            - goes beyond software update/patch management to include software marketplace solution with centralised services at enterprise lvl

#### Get updates from Microsoft Website Only
- microsoft may send email notifs abt security updates
    - shld download from website
    - dont distribute using email 
        - fake

### Microsoft Update and Automatic Updates
- for consumers & small businesses (< 50 comps)
- updates can be installed with minimal/no user interaction
- uses internet connection to search for downloads from microsoft updates website
- dont need understand technical details of security update
    - though users shld ensure they dont have apps affected by update
- service is free for licensed users
- NOTE
    - simplest approach
    - applicable to client systems that dont run mission crit services
    - if let microsoft update auto update to servers, many services will be disrupted during update
        - hence, enterprise dont adopt this approach for servers

### Windows Server Update Services (WSUS)
- for medium/large businesses
- admins can manage update settings & control distribution of updates
    - can also test updates on selected comps before deploying to rest of network
- updates downloaded once from microsoft update website & stored on local server
    - frees up internet bandwidth
- limitations
    - dont support deployment of non-microsoft updates
- free for licensed users
- NOTE
    - approach is to install local windows update server at enterprise network
    - source of patches from standard windows update services
    - unlike 1st approach, admins can hold back deployment of patches and defer actual updates to clients based on schedule
        - essential to servers running mission crit services


### Microsoft Endpoint Manager
- supports mnanagement & distribution of microsoft & non-microsoft software updates & apps
    - supports various types of endpts
        - windows/non-windows platform
        - WSUS part of it
- advanced admin control features
- charges apply
- NOTE
    - includes services & tools used to manage & monitor mobile devices, desktop pcs, VMs, embedded devices & servers
        - from their official product overview

#### Similar Alternatives
![](https://i.imgur.com/S0J7aYz.png)

### Additional Resources
- security update guide
    - AKA security bulletin
    - contains detailed guidance & info abt security update & vuln
    - supportng search/filter feature to locate specific entries
    - NOTE
        - is authoritative src of info on microsoft security updates
        - managed by __microsoft security resp center (MSRC)__

![](https://i.imgur.com/xZlVgvx.png)

- microsoft technical security notifications
    - few free of charge notification services for sign-up users
        - security update email alerts
            - provide new/major revision microsoft product security content
            - covers same content published in security update
        - security advisories alerts
            - helps admins plan for coming security updates
            - provides advance notif of upcoming security bulletins & timely notif of any minor changes to prev released microsoft security bulletins 
                - also notifs of new/revised security advisories
                - these notifs written for IT profs
                    - contains in-depth tehcnical info
        - NOTE
            - microsoft technical security notifs offer few emailers for free subscriptions


WSUS
---
- needs following
![](https://i.imgur.com/E368BVJ.png)

### Advantages
- system admin can control updates applied
- clients can be configed to get updates from local WSUS server instead of downloading from microsoft's site
    - reduces network traffic
- provide updates to comps w/o internet access

![](https://i.imgur.com/OOf0lHJ.png)
- WSUS server gets update files from common microsoft update services from internet
    - local wsus server acts as agent to maintain curated update repo to provide enterprise lvl control to distribute these updates accordingly

### Features
- admins must approve updates before wsus clients can install them
- wsus clients can be controlled by grp policy to connect to wsus server to check for updates
    - after updating, wsus clients notify wsus server
- wsus server can maintain update status of all clients

### Operations
- configuring wsus server
    - need internet access to microsoft update server to get info abt security updates
    - AKA synchronisation
        - initial sync might take awhile depending on selection choices

### Common Administration Tasks/Logging
- wsus has 2 logs for tracking events
    - synchronisation log, keeps these info
        - time of last & next scheduled sync
        - success & failure notif
        - update packages that have been downloaded/updated since last sync
            - or failed sync
        - whether sync is manual/automatic
    - approval log
        - keeps track of content that's approved/not approved

### Content Synchronisation
- during sync, new security updates can be handled in 2 ways
    - auto approve new vers of prev approved updates
    - dont auto approve new versions
- in testing env, 2nd option better
    - else testers may overlook & skip testing of new updates

### WSUS Policy Options for Clients
![](https://i.imgur.com/kAiVuFI.png)

- common windows update options for clients
- in enterprise network, domain admins can set effective options for all domain machines through GPOs
    - domain users w/o rights cannot override grp policy based settings

### WSUS Computer Groups
- wsus clients can be placed into comp grps
![](https://i.imgur.com/ppOpvLK.png)
- NOTE
    - wsus comp grps independent to security grping & OU assignment of comps
    - these grps only relevant in wsus context
        - this feature helps admins plan for their patch management strategy
        - Eg. comps in diff grps can receive diff sets of patches at diff schedules
        - testing grps can be setup to do pre-deployment test for new updates


### Patch Management Process - 8 step
![](https://i.imgur.com/bbIF2hz.png)
- typical 8 step patch management process
    - inventory process most impt
        - admins must maintain up-to-date inventory of all system & app software
        - helps admins to identify relevancy & priority of patching needs
- but we learn 5 stage approach lol

Managing Updates through 5 Stages
---
- 5 stage approach
    - stage 1
        - receive microsoft security
            - release communications
    - stage 2
        - evaluate risk
    - stage 3
        - evaluate mitigation
    - stage 4
        - deploy updates
            - 6 steps
    - stage 5
        - monitor systems

### Stage 1 - Receive Microsoft Security Release Communications
- microsoft sends out notif if there's issue affecting comp's security
    - if security changes required, security updates released
- patch tuesday
    - security updates on corresponding security bulletin normally released on 2nd tues (sometimes 4th of month)
    - exploit wednesday
        - named this as many exploitation events seen shortly after release of patch
    - since 2015, security updates released to home pc, tablets and phones asap
        - enterprise users stay on monthly update cycle
- urgent updates released immediately
- microsoft provides several ways or receiving info abt updates
    - email - security notif service comprehension edition
        - update installers nvr attached to email
    - RFS - comprehensive alerts
        - https://msrc-blog.microsoft.com/feed/
    - Twitter
        - https://twitter.com/msftsecresponse
    - website
        - https://portal.msrc.microsoft.com/en-us/security-guidance
- NOTE
    - admins can subscribe to advisories alert email notifs to get info in advance
    - admins shld be familiar with microsoft update release pattern to avoid being pattern to fake patches

### Stage 2 - Evaluate Risk
- admins shld ask
    - does vuln apply to org?
        - system admin shld keep update to date inven list of all IT assets of org
    - does vuln represent risk high to org?
- deployment of security update has cost
    - cost of testing the updates
    - costs of deploying updates
    - support costs in case of negative result after update
        - Eg. impt app doesn't work properly after update
- NOTE
    - outcome if evaluation might include
        - not apply the patch
            - since update not relevant to inven or risk ver low which cost to deploy is very high
        - defer deploy until next scheduled system maintenance down time
            - for time being, choices bare risk
                - apply some interim mitigation procedures
                - Eg. shutting down non mission critical services or configure ad hoc firewall rules to protect affected servers
        - in an unusual case, emergency patch operation needed asap & will disrupt normal operations

![](https://i.imgur.com/fOTqPd1.png)

#### Severity Ratings
- microsoft has 4 severity ratings
    - critical
        - vuln whos exploitation could enable propagation of internet worm with little/no user action
        - highest severe risk
    - important
        - vuln whos exploitation could result in compromise of confidentiality, integrity or availability of user's data, or integrity/avail of processing res
    - moderate
        - vuln whos exploitation mitigated to significant degree by factors like default config, auditing or difficulty of exploitation
    - low
        - vuln whose exploitation is extremely difficult or impact minimal
- NOTE
    - rating based on how easy of related exploitation could propagate to other internet systems

![](https://i.imgur.com/QSVbtP2.png)

### Stage 3 - Evaluate Mitigation
- short term security control can be applied when admins evaluating security updates
    - Eg. adjust firewall policies, restrict port to only specific subnet of whole network
- microsoft may provide suggested mitigation/workarounds in security advisories if security update cant be applied immediately
    - such measures meant for short-term, cant replace security updates
- NOTE
    - stage 3 & 4 usually go in parallel
    - goal of stage 3 is to identify & apply short-term work-around to manage vuln of relevant systems
        - safeguard systems until patch eventually applied

#### Examples of Mitigation Factors from Microsoft Security Bulletin
![](https://i.imgur.com/0A5Sw1I.png)

### Stage 4 - Deploy Updates
- 6 steps
    - plan deployment
        - determine which updates to roll out quickly and which to subject to more thorough testing process
        - __deployment schedule__
            - do some comp grps need updates more urgently?
            - by which date/time must comps be updated
    - determine whether security update avail for download
        - if no security update avail, microsoft will advise appropriate actions to protect comp systems
    - obtain required update files
        - obtained from src like
            - microsoft security guide
            - microsoft deployment tools
                - Eg. microsoft update, windows update, WSUS, endpt manager
            - microsoft download center
            - microsoft update catalog service
    - create update package
        - if security updates need customisation
    - test package
        - goals
            - ensure business-crit systems continue to run after update deployed
            - ensure package can be uninstalled/rolled back
            - ensure system can be restarted properly
            - ensure update effective
        - update tested in 2 ways
            - test env
                - test lab with comps mirroring actual env
                - extra overhead incurred
            - pilot env
                - test on selected production comps
                - authentic
                - can test deployment plan too
                - extra risk incurred
    - rolling out deployment
            - which to use depends on case by case basis
        - carry out deployment of update to comps that need it
        - compliant to standard patch deployment timeline
- NOTE
    - stage 4 is process that deal with actual patching deployment
        - step 1 is to complete deployment of update
            - includes confirmation of roll out schedule & target systems
            - also need obtain approval to roll out from appropriate parties (Eg. business owners)
        - step 2 to identify reliable src of update files for patch
        - step 3 to obtain files from reliable source
        - step 4 may be required to customise update for roll out
        - step 5 - proper and thorough test required to identify potential issues & effectiveness of updates
            - out of all tests, uninstallation/roll back capability test is most impt
                - negative effects of patch may only be encountered over period of time after actual deployment
        - step 6 - actual roll out
                - may need to uninstall patch to rectify probs
    - if any of 1st 5 steps encounter unforeseen issues, deployment plan might be postponed
        - Eg. time taken to complete deployment exceeds allocated maintenance window


### Step 5 - Monitor Systems
- determine which systems successfully deployed update & which didnt
    - wsus, endpoint manager features
- monitor system to detect anomaly
    - anomaly may include unsuccessful deployment cases, system malfunction cases & system/network performance issues
- possible reasons why update not successfully deployed
    - comp offline
    - comp being rebuilt/reimaged
    - comp insiffucient disk space
    - comp not communicating with update server
    - required update client software not running on comp
    - comp missing dependent software
- need resolve prob to get update applied

### Post-Deployment Review
- conducted after deployment
- steps in review
    - review org's performance during incident
    - discuss changes to service windows
    - assess total incident dmg & cost if any
    - update existing baseline for env
- NOTE
    - shld be conducted right after stage 5
        - also can be considered part of stage 5
    - goal to ensure operatinal standard & quality of org

Common Approaches to Fix Windows Update Errors
---
- check disk storage
    - system might not have sufficient disk storage to support download & installation requirement
- windows update catalog
    - download specific update package from windows update catalog website
        - to install update locally
- windows update troubleshooter
    - free tools from microsoft which can fix most of common windows updates errors







###### tags: `SMW` `DISM` `School` `Notes`