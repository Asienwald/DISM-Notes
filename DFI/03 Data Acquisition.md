

03 Data Acquisition
===




## Table of Contents

- [03 Data Acquisition](#03-data-acquisition)
  * [Table of Contents](#table-of-contents)
  * [Data Acquisition](#data-acquisition)
    + [Storage Formats for Digital Evidence](#storage-formats-for-digital-evidence)
      - [Raw Format](#raw-format)
      - [Proprietary Formats](#proprietary-formats)
      - [Advanced Forensics Format (AFF)](#advanced-forensics-format--aff-)
    + [Determining Best Acquisition Method](#determining-best-acquisition-method)
      - [Disk-to-Image File](#disk-to-image-file)
      - [Disk to Disk](#disk-to-disk)
      - [Logical or Sparse Acquisition](#logical-or-sparse-acquisition)
    + [Contingency Planning for Image Acquisitions](#contingency-planning-for-image-acquisitions)
    + [Using Acquisition Tools](#using-acquisition-tools)
    + [Capturing Image with ProDiscover Basic](#capturing-image-with-prodiscover-basic)
    + [Capturing Data with AccessData FTK Imager Lite](#capturing-data-with-accessdata-ftk-imager-lite)
  * [Validating Data Acquisitions](#validating-data-acquisitions)
    + [Windows Validation Methods](#windows-validation-methods)
    + [Remote Network Acquisition Tools](#remote-network-acquisition-tools)
    + [Other Forensics Acquisition Tools](#other-forensics-acquisition-tools)
      - [Magnet Axiom](#magnet-axiom)
      - [PassMark Software ImageUSB](#passmark-software-imageusb)
      - [Runtime Software](#runtime-software)
      - [SourceForge](#sourceforge)
  * [Summary](#summary)


Data Acquisition
---
- before analyse data, need to secure
- goal of forensic data acquisition is to create forensic copy of piece of media that is suitable to use as evi in court of law


### Storage Formats for Digital Evidence
- data in forensics acquisition tool stored as **image file**
- image file in 1 of 3 formats
    - raw format
    - proprietary formats
    - advanced forensics format (AFF) - newer

#### Raw Format
- possible to write bit stream data to files
    - sequence flat file
    - in past only do bit by bit copy to media same size or bigger to create evi
- advantages
    - fast data transfers
    - ignores minor data read errors on src drive
    - most comp forensics tools can read raw format
        - eg. .dd
- disadvantages
    - need same storage amt as orig disk/data
    - tools may not collect marginal (bad) sectors
        - due to low threshold of retry reads on weak media spots on drive

#### Proprietary Formats
- features
    - can compress image files
        - save space
    - can split img into smaller segmented files
        - provide integrity check for split data
    - can integrate metadata into img file
- disadvantages
    - cannot share img between diff tools/vendors
    - file size limit for ea segmented volume
        - usually 650mb
        - can adjust up/down at limit of 2gb
- expoer witness format is unofficial standard
    - default for guidance software encase
    - eg. ex01, e01

#### Advanced Forensics Format (AFF)
- open src acquisition format
- design goals
    - compressed or uncompressed img files
    - no size restriction for disk to img files
    - provide space in img/segmented file for metadata
    - simple design with extensibility
    - open src for multiple platforms and OS
    - vendors have no implementation restrictions on this format
        - possible future standard
    - internal consistency checks for self auth
- file ext use `.afd` for segmented img and `.afm` for AFF metadata


### Determining Best Acquisition Method
- types of acquisitions
    - static
    - live
- 4 methods of data collection
    - disk to img file
    - disk to disk
    - logical disk to disk
    - sparse data copy of file/folder
- when making copy, consider
    - size of src disk
        - lossless compression can be useful
            - dont permenantly remove data
            - orig data can be reconstructed
        - target dont need to be so big
        - use digital sig for verification
    - with large drives, alt is to use tape backup systems
        - eg. SDLT
        - can be slow if data large
    - whether can retain disk
        - sometime after copy, orig disk may need to be returned

#### Disk-to-Image File
- most common method
    - most flexible
- can make more than 1 copy
- copies are bit for bit replications of orig drive
- prodiscover, encase, ftk, SMART, sleuth kit, x-ways, ilookIX
    - tools that perform disk to img
    - read disk to img file as if orig disk

#### Disk to Disk
- when disk to img copy not possible
- tools can adjust disk's geometry config
    - eg. track, sectors etc.
- encase, snapcopy, safeback

#### Logical or Sparse Acquisition
- collecting evi from large device can take several hours
- reasons to use these methods
    - time limited
        - logical acq. captures only specific files of interest to case
            - eg. only investigate outlook
        - sparse acq. collects fragments of unallocated/deleted data
    - for large disks
    - for PST or OST mail files, RAID servers
        - up to several tb

### Contingency Planning for Image Acquisitions
- create duplicate copy of evi img file
    - in case failure
    - but time consuming
- make at least 2 imgs of digital evi
    - use diff tools or techniques
- copy host protected area (HPA - area not visible for os on drive) of disk too
    - consider using hardware acq. tool that can access drive at BIOS lvl to access HPA
- be prepared to deak with encrypted drives
    - whole disk encryption feature in windows called **BitLocker** makes static acq. difficult
    - may need user to provide decryption key
        - suspect might not cooperate

### Using Acquisition Tools
- advantages
    - acquiring evi from suspect drive more convenient
        - many tools for windows
        - especially with hot-swappable devices
            - eg. usb, fireware
- disadvantages
    - must protect acquired data with well-tested write-blocking hardware device
    - tools cant acquire data from disk's host protected area
    - some countries havent accept use of write-blocking devices for data acquisition
        - need check with legal

### Capturing Image with ProDiscover Basic
- connecting with suspect's drive to your workstation
    - document chain of evi for drive
    - remove drive from suspect's pc
    - config suspect's drive jumpers as needed
    - connect suspect drive to write blker device
    - create storage folder on target drive
- using prodiscover's proprietary acq. format
    - pd creates img files with `.eve` ext
        - log file with `.log`
        - special inventory file `.pds`
    - if compression option selected, pd uses `.cmp` instead of `.eve` on all segmented volumes

### Capturing Data with AccessData FTK Imager Lite
- ftk imager is windows acq. tool included with accessdata forensic toolkit
    - designed for viewing evi disks and disk to img files
- makes disk to img copies of evi drives
    - at logical partition and phy drive lvl
    - can segment img file
- evi drive must have hardware write blking device
    - or run from live cd like mini-winfe
- ftk imager cannot acquire drive's HPA
- use write blking device and follow
    - boot to windows
    - connect evi disk to write blker
    - connect target disk to write blker
    - start ftk imager lite
    - create disk img
        - use phy drive option

![](https://i.imgur.com/3x04Wpn.png)


![](https://i.imgur.com/NTXaK5j.png)
![](https://i.imgur.com/u0CxgeP.png)


Validating Data Acquisitions
---
- validating evi is most critical aspect of comp forensics
- needs **hashing algo utility**
- validation techniques
    - CRC-32
    - MD5
    - SHA-1
    - SHA-512

### Windows Validation Methods
- windows have no builtin algo tools
    - use 3rd pt utilities
        - hex editors like win hex
- commercial comp forensics programs have builtin validation features
    - ea program has own technique
    - prodiscover's .eve files contain metadata in acq. file or segmented files including hash val for suspect drive/partition
- raw format img files dont have metadata
    - separate manual validation recommended for all raw acquisitions

### Remote Network Acquisition Tools
- can remotely connect to suspect comp via network conn and copy data from it
- remote acq. tools vary in config and capabilities
    - some need manual intervention on remote suspect comps to initiate data copy
- tools like encase, prodiscover allow remote acq.
- drawbacks
    - antivirus, antispyware and firewall tools can be configed to ignore remote access programs
        - access can be blked
    - suspects can easily install own security tools that trigger alarm to notify them of remote access intrusions
- connecting remotely allows to
    - preview suspect's drive remotely while in use or powered on
    - perform live acq. (AKA smear as disk data being altered while comp active) while comp's comp powered on
    - encrypt conn between suspect and examiner
    - copy suspect's comp ram while comp on
    - use optional stealth mode to hide remote conn from suspect while data previewed/acquired
- other funcs
    - capture volatile system state info
    - analyse current running processes on remote system
    - locate unseen files and processes that might be running malware/spyware
    - remotely listen and view ip ports
    - run hash comparisons on remote system to search for trojans and rootkits
    - create hash inventory of all files on system remotely to establish baseline if it gets attacked
        - negative hash search capability

### Other Forensics Acquisition Tools
- magnet axiom
- passmark software imageusb
- asrdata smart
- runtime software
- ilookix investigator iximager
- sourceforge projects repository

#### Magnet Axiom
- able to recover digital evi from most sources including smartphones, cloud services, comps, iot devices and 3rd party images
- examination tool help forensics professionals find most relevant data and visualise for better analysis
- gaining popularity as user base increases

#### PassMark Software ImageUSB
- has acq. tool called imageusb for its os forensics analysis product
    - imageusb downloaded from osforensics website
- imageusb is free utility
    - can write img concurrently to multiple usb drives

#### Runtime Software
- offers shareware programs for data acq. and recovery
    - diskexplorer for FAT and NTFS
- features
    - create raw format img file
    - segment raw format or compressed img for achiving purposes
    - acces network comp drives

#### SourceForge
- provides several applications for security, analysis and investigations
    - preferred sc code repo and distribution platform for free and open src software (FOSS) projects
- [list of current tools](http://sourceforge.net/directory/security-utilities/storage/archiving/os:windows/freshness:recently-updated)

Summary
---
![](https://i.imgur.com/sCxzDR6.png)
![](https://i.imgur.com/KQFxZTR.png)




###### tags: `DFI` `DISM` `School` `Notes`