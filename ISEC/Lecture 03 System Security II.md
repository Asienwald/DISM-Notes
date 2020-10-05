---
title: 'Lecture 03 System Security II'
disqus: hackmd
---

:::info
ST1004 Infocomm Security
:::

ISEC Lecture 03 System Security II
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

Client Security
---
- securing client involves
    - using hardware system security
    - securing OS software
    - protecting peripheral devices connected

### Hardware System Security
- involves diff tools
    - secure booting tools
    - hardware root of trust
    - preventing electromagnetic spying

__Secure Booting__
- __BIOS (Basic Input/Output System)__
    - firmware used on early comps to hold boot process
    - ability to update BIOS with firmware update allowed threat actor to create malware to infect BIOS
- to combat BIOS attacks __UEFI (Unified Extensible Firmware Interface)__ developed to replace BIOS
    - __secure boot__ security standard also created
- when using UEFI & secure boot, comp checks digital signature of ea piece of boot software
    - if signatures deemed valid comp boots
    - else doesn't boot
![](https://i.imgur.com/8HyXSns.png)

__Hardware Root of Trust__
- chain of trust
    - ea element of boot process relies on confirmation of prev element to know that entire process is secure
- hardware root of trust
    - strongest starting point is hardware which cannot be modified
- security checks "rooted" in hardware checks

__Electromagnetic Spying__
- security researchers found that it's possible to pick up electromagnetic fields & read data that's producing them
- US gov developed classified standard
    - to prevent attackers from picking up electromagnetic fields from gov buildings
- AKA __Telecommunications Electronics Material Protected from Emanating Spurious Transmissions (TEMPEST)__

__Supply Chain Infections__
- supply chain
    - network that moves product from supplier to customer
- diff steps in supply chain allowed for malware to be injected into products during manufacturing/storage
    - AKA __supply chain infections__
- supply chain infections considered dangerous
    - if malware planted in ROM firmware of device, difficult/impossible to clean infected device
    - users may be receiving infected devices at point of purchase, unaware of infection
    - cannot be easily prevented


### Securing OS Software
![](https://i.imgur.com/j5xdKxA.png)

__OS Security Configuration__
- typical OS security config include
    - disabling unnecessary ports & services
    - disabling default accounts/passwords
    - employing least functionality
    - app whitelisting/blacklisting
- instead of recreating same security config on ea comp
    - tools can be used to automate process
- in windows
    - security template is collection of security config settings that can be deployed to other devices

__Patch Management__
- OS has increased in size & compexity
- new attack tools made secure functions vulnerable
- __security patch__ - software security update to repair discovered vulnerabilities
- __feature update__ - includes enhancements to software to provide new/expanded functionality
    - doesn't address security vulnerability
- __service pack__ - accumulates security updates & additional features 
- patch management tools
    - tools for patch distribution
    - patch reception
- __patch distribution__
    - patches sometimes create new problems
        - vendor should thoroughly test before deploying
    - __automated patch update service__
        - manage patches locally than rely on vendor's online update service
        - advantages
            - downloading patches from local server can save bandwidth & time
            - admins can approve/decline updates, force updates to install by specific date, & obtain reports on what updates ea computer needs
            - admins can approve updates for "detection" only
                - allows them to see which comps need update w/o actually installing it
![](https://i.imgur.com/1mjt9OS.png)
- patch reception
    - today patches auto downloaded & installed
    - ensures software always up-to-date
    - Microsoft changed its security update procedures & user options
        - forced updates
        - no selective updates
        - more efficient distribution
        - up-to-date resets

__Antimalware__
- antimalware software packages can provide added security
- software includes
    - antivirus
    - antispam
    - antispyware
- __Antivirus (AV)__ - software that examines a computer for infections
    - scans new documents that might contain viruses
    - searches for known virus patterns
- weakness of anti-virus
    - vendor must continually search for new viruses, update & distribute signature files to users
- newer approach to AV is heuristic monitoring (AKA __dynamic analysis__)
    - uses variety of techniques to spot characteristics of virus instead of attempting to make matches
- one AV heuristic monitoring technique - __code emulation__
    - questionable code executed in virtual env to determine if its virus
- antispam
    - mail gateway - monitors emails for spam & other unwanted content
    - some spam can slip through
    - antispam filtering software traps spam
- spam filtering methods
    - create list of approved & nonapproved senders
        - blacklist - nonapproved senders
        - whitelist - aapproved senders
    - blocking certain file attachment types
    - bayesian filtering - divides email messages into 2 piles
        - spam
        - nonspam
- antispyware - helps prevent comps from becoming infected by diff types of spyware
    - pop-up - small windows appearing over website
        - usually created by advertisers
    - pop-up blockers - separate program as part of anti-spyware package
        - incorporated within browser
        - allows user to limit/block most pop-ups
        - alert can be displayed in browser
            - gives user option to display pop-up
- trusted OS 
    - __OS hardening__ - tightening security during design & coding of OS
    - __trusted OS__ - OS that has been designed through OS hardening
![](https://i.imgur.com/LMotl9L.png)


Physical Security
---
- includes
    - external perimeter defenses
    - internal physical access security
    - security for protecting hardware device itself

### External Perimeter Defenses
- designed to restrict access to equipment areas
- type of defense includes
    - barriers
    - guards
    - motion detection devices

__Barriers__
- fencing - usually a tall, permanent structure
    - modern perimeter fences equipeed with other deterrents like proper lighting & signage
- cage - fenced secure waiting station area
    - Eg. area that contain visitors to facility until approved for entry
- barricade - large concrete ones used
- bollard - short but sturdy vertical post used as vehicular traffic barricade to prevent car from "ramming" into secured area

__Guards__
- human security guards considered active security elements
- video surveillance cameras transmit signal to specified & limited set of receivers called __closed circuit television (CCTV)__
    - frequently used for surveillance in areas that need security monitoring like banks, casinos, airports & military installations

__Motion Detection__
- determining object's change in pos in relation to its surroundings
- movement usually generates audible alarm
![](https://i.imgur.com/WIAGqUv.png)


### Internal Physical Access Security
- include
    - door locks
    - access logs
    - mantraps
    - protected distribution systems for cabling

__Door Locks__
- __standard keyed entry lock__ provides minimal security
- __deadbolt locks__ provide additional security & require that a key be used to both open & lock the door
- __cipher locks__ are combination locks that use buttons that must be pushed in proper sequence
    - can be programmed to allow certain individual's code to be valid on specific dates & times
- key management procedures
    - keep track of keys issued & require users to sign their name when receiving keys
    - receive proper approvals of supervisors or other appropriate persons before issuing keys
    - when making duplicates of master keys, mark them "Do Not Duplicate" & wipe out manufacturer's serial numbers
    - secure unused keys in locked safe
    - change locks immediately upon loss or theft of keys

__Access Logs__
- access list
    - record of individuals who have permission to enter secure area
    - records time they entered and left
- today cipher logs & other tech can create electronic access logs

__Mantraps__
- separates secured from nonsecured area
- monitors & controls 2 interlocking doors
    - only 1 door can open at any time
- used at high-security areas where only authorised persons can enter
    - Eg. cash handling areas & research labs

__Protected Distribution Systems (PDS)__
- system of cable conduits used to protect classified info that's transmitted between 2 secure areas
    - created by US Department of Defense (DOD)
- 2 types of PDS
    - __hardened carrier PDS__ - conduit constructed of special electrical metallic tubing
    - __alarmed carrier PDS__ - specialised optical fibers in conduit that sense acoustic vibrations that occur when intruder attempts to gain access
![](https://i.imgur.com/snDu52v.png)

### Computer Hardware Security
- physical security protecting hardware of host system
    - most portable devices have steel bracket security slot
    - cable lock can be inserted into slot & secured to device & cable connected to lock can be secured to desk/chair
- safe/secure cabinet
    - can be prewired for power & network connections
    - allows devices to charge while stored and receive updates


Application Security
---
- need to protect apps that run on devices
- aspects
    - app development security
    - secure coding techniques
    - code testing
    - virtualisation

### Virtualisation
- virtualisation - means of managing & presenting computer resources w/o regard to phy layout/location
- host virtualisation
    - entire OS env simulated
    - vm - simulated software-based emulation of computer
    - host system runs hypervisor that manages virtual OS & supports 1 or more guest systems
- advantages
    - new virtual server machines can be made available __(host availability)__ & resources can be easily expanded/contracted as needed __(host elasticity)__
    - reduce costs
        - fewer phy comps purchased & maintained
    - provide uninterrupted server access to users
        - supports live migration which allows vm to be moved to diff phy comp with no impact to users
    - test latest patches on vm before installing
    - snapshot of particular state of vm can be saved for later use
    - testing existing security config __(security control testing)__ can be performed using simulated network env
    - suspicious program can be loaded into isolated vm & executed __(sandboxing)__
        - if malware, only vm impacted
- security for virtualised env
    - guest OS remained dormant may not contain latest patches & security updates
    - not all hypervisors have necessary security controls to keep out attackers
    - existing security tools designed for single physical servers & not always adapt well to multiple vm
    - vm must be protected from outside network & other vm on same comp

Chapter Summary
---
![](https://i.imgur.com/ktf1pFV.png)
![](https://i.imgur.com/o29N7nv.png)
![](https://i.imgur.com/NLZptCO.png)




###### tags: `ISEC` `DISM` `School` `Notes`