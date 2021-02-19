

02 Understanding Digital Forensics
===



## Table of Contents

- [02 Understanding Digital Forensics](#02-understanding-digital-forensics)
  * [Table of Contents](#table-of-contents)
  * [Systematic Approach](#systematic-approach)
    + [Assessing Case](#assessing-case)
    + [Planning Investigation](#planning-investigation)
      - [Evidence Forms](#evidence-forms)
    + [Securing Evidence](#securing-evidence)
    + [Conducting an Investigation](#conducting-an-investigation)
    + [Gathering Evidence](#gathering-evidence)
      - [Bit-Stream Copies](#bit-stream-copies)
      - [Acquiring Image of Evidence Media](#acquiring-image-of-evidence-media)
    + [Completing Case](#completing-case)
    + [Critique Case](#critique-case)
  * [Private Sector High-Tech Investigations](#private-sector-high-tech-investigations)
    + [Procedure Examples](#procedure-examples)
      - [Employee Termination Cases](#employee-termination-cases)
      - [Internet Abuse Investigations](#internet-abuse-investigations)
      - [Email Abuse Investigations](#email-abuse-investigations)
      - [Industrial Espionage Investigations](#industrial-espionage-investigations)
    + [Interviews and Interrogations in High-Tech Investigations](#interviews-and-interrogations-in-high-tech-investigations)
  * [Data Recovery Workstations and Software](#data-recovery-workstations-and-software)
    + [Setting Up Workstation for Digital Forensics](#setting-up-workstation-for-digital-forensics)
  * [Acquiring File Evidence with ProDiscover](#acquiring-file-evidence-with-prodiscover)
    + [Acquire USB Drive](#acquire-usb-drive)
    + [Analysing Digital Evidence](#analysing-digital-evidence)
    + [Completing the Case](#completing-the-case)
  * [Summary](#summary)

Systematic Approach
---
![](https://i.imgur.com/EEfwoNK.png)

- steps for prob solving
    - make initial assessment abt case type
        - eg. interview ppl, places to visit etc.
    - determine preliminary design/approach to case
        - eg. when to visit company employees
    - create detailed checklist
        - stay on track
    - determine res needed
    - obtain copy of of evi drive
    - identify risks
    - mitigate/minimise risks
        - ensure evi always avail
    - test design
    - analyse and recover digital evi
    - investigate data recovered
    - complete case report
    - critique case
        - self eval to improve

### Assessing Case
- outline case details including
    - situation
        - eg. employee abuse case
    - nature of case
        - eg. used email for personal stuff
    - specifics of case
        - eg. detailed info of case
    - type of evi
        - eg. usb drive
    - known disk format
        - eg. FAT
    - location of evi
        - eg. usb recovered from employee's desk

### Planning Investigation
- basic inves plan shld include
    - acquire evi
    - evi form and chain of custody
        - shows whr file came from, who created it and type of equipment used
    - transport evi to comp forensics lab
    - secure evi in **approved secure container**
    - prep for **forensics workstation**
    - retrieve evi from secure container
        - ensure info confidential
        - container shld be locked, fireproof locker/cabinet with limited access
    - make forensic copy of evi
    - return evi to secure container
    - process copied evi with comp forensics tools
        - Eg. Encase
- evi custody form helps document what has been done with orig evi and forensics copies
    - AKA **chain of evi form**

#### Evidence Forms
- 2 types
    - single evi form
        - list ea evi on separate page
    - multi evi form

![](https://i.imgur.com/e6jgALd.png)
- model/serial num of comp component
- evi recovered by
    - name of investigator who recovered evi
    - chain of custody starts here - person with stated name is responsible for preserving, transporting and securing the evi
- date and time evi taken into custody

![](https://i.imgur.com/tHynAoA.png)

### Securing Evidence
- use **evidence bags** to secure and catalog evi
- use comp safe products when collecting comp evi
    - antistatic bags
    - antistatic pads
- use well padded containers
- use **evidence tape** to seal all openings
    - cd drive bays
    - insertion slots for power supply electrical cords and usb cables
    - write initials on tape to prove that evi not tampered with
- consider comp specific temp and humidity range
    - ensure have safe env for transporting and storing until secure evi container avail

### Conducting an Investigation
- gather res identified in inves plan
- items needed
    - orig storage media
    - evi custody form
    - evi container for storage media
    - bit stream imaging tool
    - forensics worktstation to copy and examine evi
    - securable evi locker/cabinet/safe

### Gathering Evidence
- avoid damaging evi
- steps
    - meet it manager for interview
    - fill evi form and have it manager sign
    - place evi in secure container
    - carry evi to comp forensics lab
    - complete evi custody form
    - secure evi by locking container

#### Bit-Stream Copies
- bit stream copy
    - bit by bit copy of orig storage medium
    - exact copy of orig disk
    - diff from simple backup copy
        - backup software only copy known files
        - backup software cannot copy deleted files, email msgs or recover file fragments
    - copy image file to target disk that matches orig disk's manufacturer, size and model
- bit stream image
    - file containing bit stream copy of all data on disk/partition
    - AKA image or image file

![](https://i.imgur.com/vquuMJR.png)

#### Acquiring Image of Evidence Media
- 1st rule of comp forensics - preserve orig evi
- conduct analysis only on copy of data
- several vendors provide MS-DOS, linux and windows acquisition tools
    - windows tools require write-blocking device when acquiring data from **FAT or NTFS** file systems

### Completing Case
- produce final report
    - state wha u did and what u found
- repeatable findings
    - repeat steps and produce same result
- if required, use report template
    - report shld show conclusive evi
        - suspect did/did not commit crime or violate company policy
- keep written journal of everything you do
    - notes can be used in court
- answer the 6 Ws
    - who what when whr why and how
- must explain comp and network processes
    - good to identify who your report reader is and write smth suitable for reader

### Critique Case
- ask these qns
    - how to improve perf in case>
    - got expected results? did case develop in ways you didnt expect?
    - is documentation thorough enough?
    - what feedback received from requesting src?
    - discover any new probs?
    - used new techniques during case/research?


Private Sector High-Tech Investigations
---
- need to develop formal procedures and informal checklists
    - cover all issues impt to high tech inves
    - ensure correct techniques used in inves
    - diff cases may have diff procedures

### Procedure Examples
#### Employee Termination Cases
- majority of inves work for termination involves employee abuse of corporate assets
- incidents that create hostile work env are prodominant types of cases investigated
    - viewing porn in workplace
    - sending inappropriate emails
- orgs must have appropriate policies in place
    - consult hr dept

#### Internet Abuse Investigations
- need
    - org's internet proxy server logs
    - suspect comp's ip addr
    - suspect comp's disk drive
    - preferred comp forensics analysis tool
- recommended steps
    - use standard forensic analysis techniques and procedures
    - use appropriate tools to extract all webpage url info
    - contact network firewall admin and request proxy server log
    - compare data recovered from analysis to proxy server log
    - continue analysing comp's disk drive data

#### Email Abuse Investigations
- need
    - electronic copy of offending email with msg header data
    - if avail, email server log records
    - for email systems that store user's msgs on central server, access to server
    - access to comp so can perform forensic analysis on it
    - preferred forensics tool
- recommended steps
    - use standard techniques
    - obtain electronic copy of suspect's and victim's email folder/data
    - for web-based email inves, use tools like FTK'S internet keyword search option to extract related email addr info
    - examine header data of all msgs of interest to inves

#### Industrial Espionage Investigations
- all suspected such cases shld be treated as criminal investigations
    - very common
- staff needed include
    - **computing investigator**
        - resp for disk forensics examinations
    - **tech specialist**
        - knowledgable of suspected compromised technical data
    - **network specialist**
        - can perform log analysis and setup network sniffers
    - **threat assessment specialist**
        - typically an attorney
- guidelines for inves
    - determine if inves involves industrial espionage incident
    - consult corporate attorneys and upper management
    - determine what info needed to substantiate inves
    - generate list of keywords for disk forensics and sniffer monitoring
    - list and collect res for inves
    - determine goal and scope of inves
    - initiate inves after approval from management
- planning considerations
    - examine all email of suspected employees
    - search internet newsgrps or msg boards
    - initiate phy surveillance
    - examine facility phy access logs for sensitive areas
    - determine suspect location in relation to vuln asset
    - study suspect's work habits
    - collect all incoming and outgoing phone logs
- steps for inves
    - gather all personnel assigned to inves and brief on plan
    - gather res for inves
    - place surveillance systems at key locations
    - discreetly gather extra evi
    - collect all log data from networks and email servers
    - report regularly to management and corporate attorneys
    - review inves's scope with management and corporate attorneys

### Interviews and Interrogations in High-Tech Investigations
- becoming skilled interviewer and interrogator can take many years of exp
- definitions
    - interview - usually conducted to collect info from witness/suspect
        - abt specific facts related to inves
    - interrogation - process of trying to get suspect to confess
- computing investigator role
    - instruct investigator on what qns to ask and what answers shld be
- ingredients for successful interview/interrogation
    - patience throughout session
    - repeating/rephrasing qns to zero in on specific facts from reluctant witness/suspect
    - being tenacious


Data Recovery Workstations and Software
---
- inves conducted in comp forensics lab/data recovery lab
    - in data recovery, client just wants data back
- computer forensics workstation
    - specially configured pc
    - loaded with extra bays and forensics software
- to avoid altering evi use **write-blocker devices**
    - enable u to boot windows w/o writing data to evi drive

### Setting Up Workstation for Digital Forensics
- basic requirements
    - workstation running win xp or later
    - write-blocker device
        - prevent writes to storage devices
    - digital forensics acquisition tool
    - digital forensics analysis tool
    - target drive to receive src or suspect disk data
    - spare PATA (parallel) or SATA (serial) ports
    - usb ports
- extra useful items
    - nic
    - extra usb ports
    - firewire 400/800 ports
    - SCSI card
    - disk editor tool
    - txt editor tool
    - graphics viewer program
    - other specialised viewing tools

Acquiring File Evidence with ProDiscover
---
### Acquire USB Drive
- use prodicsover basic to acquire usb drive
    - create work folder for data storage
- steps
    - on usb drive locate write-protect switch and place drive in wirte-protect mode
    - start prodiscover basic
    - in main windows, action > capture image from menu
    - click src drive drop down list and select thumbdrive
    - click >> btn next to dst txt box
    - type name in technician name txt box
    - prodiscover basic acquires an image of the usb drive
    - click ok in completion msg box

![](https://i.imgur.com/3D5Sz1C.png)
![](https://i.imgur.com/mcLEcTh.png)

### Analysing Digital Evidence
- job to recover data from
    - deleted files
    - file fragments
    - complete files
- deleted files linger on disk until new data saved on same phy location
    - or reformat performed
- prodiscover basic can retrieve deleted files
- steps to analyse usb drive
    - start basic
    - create new case
    - type project num
    - add image file
- steps to display contents of acquired data
    - click expand content view
    - click all files under image filename path
    - click letter1 to view contents in data area
- analyse data - search for info related to complaint
- data analysis can be most time-consuming task

![](https://i.imgur.com/cj1kr8G.png)
- prodiscover basic can
    - search for keywords of interest in case
    - display results in search results window
    - click ea file in search results window and examine content in data area
    - export data to folder of your choice
    - search for specific filenames
    - generate report of activities

![](https://i.imgur.com/DQB6YOA.png)
![](https://i.imgur.com/PqQHaSI.png)
![](https://i.imgur.com/iDvxmSk.png)

### Completing the Case
- produce final report
- include prodiscover report to document work
- everything similar to point above


Summary
---
![](https://i.imgur.com/ktdiAz2.png)
![](https://i.imgur.com/jsO2lw8.png)
![](https://i.imgur.com/GoSKOge.png)





###### tags: `DFI` `DISM` `School` `Notes`