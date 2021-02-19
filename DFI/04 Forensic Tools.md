

04 Forensic Tools
===




## Table of Contents

- [04 Forensic Tools](#04-forensic-tools)
  * [Table of Contents](#table-of-contents)
  * [Digital Forensic Tools](#digital-forensic-tools)
    + [Evaluating Tool Needs](#evaluating-tool-needs)
    + [Types of Tools](#types-of-tools)
    + [Tasks Performed by Digital Forensic Tools](#tasks-performed-by-digital-forensic-tools)
      - [Acquisition](#acquisition)
      - [Validation and Verification](#validation-and-verification)
      - [Extraction](#extraction)
      - [Reconstruction](#reconstruction)
      - [Reporting](#reporting)
  * [Considerations for Tools](#considerations-for-tools)
    + [GUI Tools](#gui-tools)
    + [Hardware Tools](#hardware-tools)
    + [Forensic Workstations](#forensic-workstations)
      - [Recommendations](#recommendations)
    + [National Institute of Standards and Technology Tools](#national-institute-of-standards-and-technology-tools)
    + [Validating and Testing Software](#validating-and-testing-software)
    + [Validation Protocols](#validation-protocols)
  * [Write-Blocker](#write-blocker)
    + [Using Write-Blocker](#using-write-blocker)
  * [Summary](#summary)


Digital Forensic Tools
---
### Evaluating Tool Needs
- consider open src tools
    - best val for many features
- qns to ask
    - which os it run on
    - what file systems to analyse
    - can scripting lang be used with tool to automate repititive funcs?
    - have automated features?
    - vendor's reputation for support?

### Types of Tools
- hardware forensic tools
    - range from single purpose components to complete comp systems and servers
- software forensic tools
    - up to $300
    - types
        - command line apps
        - gui apps
    - commonly used to copy data from suspect's disk drive to img file

### Tasks Performed by Digital Forensic Tools
- follow guidelines by NIST's comp forensic tool testing (CFTT) program
    - ISO standard 27037 states that digital evi first responders (DEFRs) shld use validated tools
- all comp forensic tools (hardware and software) perform specific funcs
    - funcs grped into 5 categories
        - acquisition
        - validation and verification
        - extraction
        - reconstruction
        - reporting

#### Acquisition
- making copy of orig drive
- acq. subfunctions
    - phy data copy
    - logical data copy
        - logical partition
    - data acq. format
        - raw data format
    - gui acq.
    - remote, live (logon) and memory acq.
- 2 types of data copying methods used
    - phy copying of entire drive
    - logical copying of disk partition
- formats for disk acq. vary
    - from raw data to vendor-specific proprietary
- can view contents of raw img with hex editor

![](https://i.imgur.com/Pe2YToQ.png)
- creating smaller segmented files is typical feature in vendor acq. tools
    - segmented files are smaller and hence can be stored in smaller media
- remote acq. of files is common in larger orgs
    - popular tools like accessdata and encase can do remote acq. of forensics drive imgs on network

#### Validation and Verification
- validation
    - way to cfm that tool is functioning as intended
        - ensure integrity of data copied
- verification
    - prove that 2 sets of data are identical by calculating hash or using similar method
    - related process if **filtering**
        - involves sorting and searching through inves. findings to seperate good and suspicious data
- subfunctions
    - hashing
        - ensure data not changed
        - CRC-32, MD5, SHA-1
    - filtering
        - separate good files and files that need to be investigated
        - based on hash val sets
    - analysing file headers
        - check on change file type
        - discriminate files based on types
- national software reference lib (NSRL) has compiled list of known file hashes
    - for variety of OS, apps and imgs
- validation and discrimination
    - many comp forensics programs include list of common header vals
        - can see whether file ext is incorrect for file type
    - most tools can identify header vals

#### Extraction
- recovery task in digital inves.
    - most challenging to master
- recovering data is 1st step in analysing inves.'s data
- subfunctions
    - data viewing
        - diff tools provide diff way of viewing data
        - keyword searching
            - good func but if wrong keyword used may produce noise
            - speeds up analysis for investigators
        - decompressing
        - carving
            - reconstructing fragments of files
        - decrypting
            - potential prob for inves.
            - password recovery tools have feature for generating password lists
                - AKA password dict atk
                - if pwd dict atk fails, can run brute force atk
        - bookmarking/tagging

#### Reconstruction
- recreate suspect drive to show what happened during crime or incident
    - or to create copy of suspect drive for other inves.
- methods
    - disk to disk copy
    - partition to partition
    - image to disk
    - image to partition
    - rebuilding files from data runs and carving
- to recreate img of suspect drive,
    - copy img to another location/partition/phy disk or vm
    - simplest method use tool to make direct disk to img copy
        - linux dd command
        - prodiscover
        - voom technologies shadow drive


#### Reporting
- perform forensic disk analysis and examination, need to create report
- subfunctions
    - bookmarking/tagging
    - log reports
        - document inves. steps
    - report generator
- use this info when producing final report


Considerations for Tools
---
- considerations
    - flexibility
    - reliability
    - future expandability
- create software lib with older vers of forensic utilities, OS and other programs

### GUI Tools
- can simplify inves.
    - simplified training for beginner examiners
- most put tgt suite of tools
- advantages
    - ease of use
    - multitasking
    - dont need learn older OS
- disadvantages
    - excessive res requirements
        - eg. ram
    - inconsistent results
        - because of type of OS used
        - eg. 32 bit vs 64 bit
    - create tool dependencies
        - inves. may want to use only 1 tool
            - refuse to change
        - shld be familiar with more than 1 type of tool

### Hardware Tools
- technology changes rapidly
    - hardware eventually fails
- schedule equipment replacements periodically
- when planning budget consider
    - amt of time for workstation to be running
    - how often it fails
    - consultant and vendor fees
        - support h/w
    - anticipate eq replacement
        - more u use, more eq will break

### Forensic Workstations
- categories
    - stationary
    - portable
    - lightweight
- balance what u need and what your system can handle
    - rmb that ram and storage need updating as tech advances
- policy agency labs
    - need many options
    - use several pc configs
        - due to diverse inves.
- keep hardware lib with software lib
- priv corporate labs
    - handle only system types used in org
- nnot difficult to build
    - advantages
        - customised needs
        - save money
    - disadvantages
        - hard to find support for probs
        - can become expensive if careless
- need to identify what u intend to analyse

#### Recommendations
- workstations designed for forensics
- vendor support to save time and frustration if probs
- mix and match components to get capabilities needed
- determine whr data acq. will take place
    - eg. acquire data in field, may want to carry smth light
- for stationary and lightweight workstations,
    - full tower to allow expansion devices
    - as much memory and processor power as budget allows
    - diff sizes of hard drives
    - 400w or better power supply with batt backup
    - external firewire and usb 2.0 ports
    - assortment of drive bridges
    - ergonomic keyboard and mouse
    - good gpu
    - >17 inch monitor
    - high end gpu and dual monitors
- if limited budget, 1 option for outfitting lab is to use high end game pc
    - can perform well with modifications

### National Institute of Standards and Technology Tools
- NIST publishes articles, provides tools and creates procedures for testing/validating forensics software
- comp forensic tool testing (CFTT) project
    - manages research on comp forensics tools
- NIST created criteria for testing comp forensic tools based on
    - standard testing methods
    - ISO 17025 criteria for testing items that have no current standards
- lab must meet these criteria
    - establish categories for tools
    - identify category requirements
    - develop test assertions
        - based on requirements, create tools to test tool's capability
    - identify test cases
    - establish test method
    - report test results
- ISO 5725 - specifies result must be repeatable and reproducible
- NIST created national software ref lib (NSRL) project
    - collects all known hash for commercial software apps and os files
        - uses sha-1 to gen known set of digital sigs called **reference data set (RDS)**
    - helps filtering known info
        - can help speed up inves. time
    - can use rds to locate and identify known bad files

### Validating and Testing Software
- impt for evi u recover and analyse to be admitted in court
- test and validate software to prevent damaging evi

### Validation Protocols
- always verify results by doing same tasks with other tools
    - use at least 2
        - retrieving and examination
        - verification
- understand how forensics tools work
- 1 way to compare results and verify new tool is using disk editor like hex workshop or winhex
    - disk editor can view data on disk in raw format
    - dont have flashy interface
        - still reliable
        - can access raw data
- comp forensic examination protocol
    - perform inves. with gui tool
    - verify results with disk editor
    - compare hash with both tools
- digital forensics tool upgrade protocol
    - ensure evi data wont be corrupted, we need to
        - test
            - new releases for tools
            - os patches and upgrades
        - if find prob, report to forensic tool vendor
            - dont use tool until prob fixed
        - use test hard disk for validation
        - check web for new editions, updates, patches and validation tests for tools




Write-Blocker
---
- prevents writes to hard disk
    - any tool that permits read only access to data storage devices w/o compromising integrity of data
- software enabled blkers
    - typically run in shell mode (windows cli)
        - eg. pdblock from digital intelligence
- hardware options
    - ideal for gui forensic tools
        - prevent windows/linux from writing data to blocked drive
    - act as bridge between suspect drive and forensic workstation

### Using Write-Blocker
- can navigate to blked drive with any app
    - no prob accessing blked drive's apps after write-blker installed
- discards written data
    - from os if data copy successful
- connecting tech
    - firewire
    - usb 2.0 and 3.0
    - sata, pata and scsi controllers


Summary
---
![](https://i.imgur.com/2EMYQHl.png)
![](https://i.imgur.com/0UyP4um.png)






###### tags: `DFI` `DISM` `School` `Notes`