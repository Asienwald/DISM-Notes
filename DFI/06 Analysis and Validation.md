

06 Analysis and Validation
===




## Table of Contents

- [06 Analysis and Validation](#06-analysis-and-validation)
  * [Table of Contents](#table-of-contents)
  * [What Data to Collect and Analyse](#what-data-to-collect-and-analyse)
  * [Digital Forensics Cases](#digital-forensics-cases)
    + [Basic Steps](#basic-steps)
    + [Refining and Modifying the Investigation Plan](#refining-and-modifying-the-investigation-plan)
  * [Analysing and Validating Data](#analysing-and-validating-data)
    + [Using OSForensics to Analyse Data](#using-osforensics-to-analyse-data)
    + [Validating Forensic Data](#validating-forensic-data)
      - [Validating with Hex Editors](#validating-with-hex-editors)
      - [Validating with Digital Forensics Tools](#validating-with-digital-forensics-tools)
    + [Data Hiding Techniques](#data-hiding-techniques)
      - [Hiding Files using OS](#hiding-files-using-os)
      - [Hiding Partitions](#hiding-partitions)
      - [Making Bad Clusters](#making-bad-clusters)
      - [Bit-Shifting](#bit-shifting)
    + [Steganalysis Methods](#steganalysis-methods)
    + [Examining Encrypted Files](#examining-encrypted-files)
    + [Recovering Passwords](#recovering-passwords)
  * [Summary](#summary)


What Data to Collect and Analyse
--
- depends on nature of inves. AND amt to process
    - investigators often locate and recover specific items like emails - simplify speed processing
- **scope creep** - when inves. expands beyond orig description
    - due to unexpected evidence
    - attorneys may ask investigators to examine other areas or more evi
    - inc time and res needed to extract, analyse and present evi
    - document extra time spent on recovering extra evi
- scope creep more common now
    - criminal inves. needs more detailed examination of evi just before trial
    - helps prosecutors fend off atks from def attrneys
- new evi discovered often isnt revealed to proscution
    - more impt for prosecution teams to ensure they analysed evi exhaustively before trial

Digital Forensics Cases
---
- begin case with inves. plan that defines
    - goal and scope of inves.
    - materials needed
    - tasks to do
- approach depends on type of case
    - corporate
        - easier due to easy access to evi
    - criminal
        - more difficult due to scope
            - eg. need contact ISP to gather evi
    - civil

### Basic Steps
- for target drives, use recently wiped media that is reformatted and inspected for viruses
- inventory the hardware on suspect's comp
    - note condition of the comp too
- for static acq., remoe orig drive and check date and time vals in system's CMOS
- record how u acquire data from the drive
- process drive content methodically and logically
    - eg. emails > jpg > spreadsheet > word
- list all folders and files on drive
    - note whr xx file found
- recover file content for all pwd protected files
    - use pwd recovery tools
- identify func of every exe file that dont match hash vals
    - if needed run file for more info
- maintain control of all evi and findings

### Refining and Modifying the Investigation Plan
- sometimes need to deviate from init plan and follow evi
- know data types to look for
- key to start with plan but be flexible


Analysing and Validating Data
---
### Using OSForensics to Analyse Data
- osforensics support these file systems
    - microsoft FAT12, FAT16, FAT32
    - microsoft NTFS
    - mac HFS+ and HSFX
    - linux EXT2fs and EXT4fs
- can analyse data from many sources
    - includes img files from other vendors

![](https://i.imgur.com/t87lZS7.png)

### Validating Forensic Data
- ensure integrity of data essential for presenting evi in court
- tools offer hashing of image files
    - eg. prodiscover runs hash and compares hash with orig hash when loaded file

#### Validating with Hex Editors
- some tools have limitations for hashing so use advanced hex editors for data integrity
- advanced hex editors have features not in forensic tools
    - hashing specific files or sectors
    - with hash val, use tool to search for suspicious file that might have name changed to look unsuspecting
- winhex provides md5 and sha-1 hashing algo

![](https://i.imgur.com/YHve4VE.png)
- use hash vals to **discriminate data**
    - accessdata has own hashin db AKA **known file filter (KFF)**
    - KFF filters known program files from view and contain hash vals of known illegal files
    - compares file hash with files on evi drive if contain suspicious data
    - other tools can import the **NSRL db** and run hash comparisons

#### Validating with Digital Forensics Tools
- prodiscover
    - .eve files have metadata with hash val
    - has preference u can enable for auto verify img checksum feature when files loaded
        - if auto verify img checksum and hash in .eve metadata dont match, prodiscover will notify that acq. corrupted and not reliable evi

![](https://i.imgur.com/0rN6mBb.png)
- raw frmat img files dont have metadata
    - must validate manually
- in accessdata ftk imager, when selecting Expert Witness (.e01) or SMART (.s01) format,
    - extra options for validating acq. avail
    - validation report lists md5 and sha-1 hashes

### Data Hiding Techniques
- data hiding - changing/manipulating file to conceal info
- techniques
    - hiding entire partitions
        - use disk management
    - changing file exts
    - setting file attributes to hidden
        - change file sig
    - bit shifting
        - shift 1 bit to left
    - use encryption
    - pwd protection

#### Hiding Files using OS
- change file ext
- tools check file headers
    - compare file ext to verify
    - if there's discrepancy, tool flags file as possible altered file
- other hiding technique by selecting hidden attribute in file's properties dialog box in windows

#### Hiding Partitions
- use windows `diskpart remove <letter>` command
    - can unassign partition's letter which hides it from file explorer
    - use `diskpart assign <letter>` to unhide
- other disk mannagement tools
    - partition magic
    - partition master
    - linux grand unified bootloader (GRUB)
- to detect whether partition hidden,
    - acc for all disk space when examining drive
    - analyse all disk areas containing space u cannot acc for
- in prodiscover, hidden partition appears as highest avail drive letter in bios
    - other tools have own methods to assign drive letters

![Uploading file..._fzb2ncmgj]()

#### Making Bad Clusters
- data hiding technique in FAT is placing sensitive data in free/slack space on disk partition clusters
    - involve old utilities like norton diskedit
- can mark good clusters as bad so os consider them unusable
    - only way to access by changing back to good cluster with disk editor
- diskedit runs only in ms-dos and can only access FAT-formatted disk media

#### Bit-Shifting
- some user use low lvl encryption program that changed order of binary data
    - makes altered data unreadable
        - to secure file, users run assembler program AKA macro to scramble bits
    - run another program to restore scrambled bits to orig order
- bit shifting changes data from readable code to data that looks like binary exe code
- winhex includes bit shifting feature

### Steganalysis Methods
- steganography - greek word for hidden writing
    - hiding msg only for intended recipient
    - steganalysis - detecting and analysing stego files
- digital watermarking - developed as way to protect file ownership
    - usually not visible when using stego
- way to hide data is use stego tools
    - many are freeware/shareware
    - insert info into variety of files
- if encrypt plaintxt file with pgp and insert encrypted txt into stego file, cracking encryped msg is very dificult
- steganalysis methods
    - stego only atk
        - only have converted covered file to analyse
    - known cover atk
        - has both covered file and converted covered file to analyse
    - known msg atk
        - when hidden msg revealed ltr
    - chosen stego atk
        - stego tool used
    - chosen msg atk
        - steganalyst generates stego-obj from some stego tool/algo of chosen msg

### Examining Encrypted Files
- to decode encrypted file,
    - supply pwd/passphrase
- many encryption programs use tech called **key escrow**
    - designed to recover encrypted data if users forget pwd or if user key corrupted after system failure
- key sizes of 2048bits to 4096bits make breaking them impossible with current tech
- OR try to make suspect reveal encryption passphrase

### Recovering Passwords
- pwd cracking tools avail for handling pwd protected data
    - some integrated into tools
- standalone tools
    - last bit
    - accessdata prtk
    - ophcrack
    - john the ripper
    - passware
- brute force atks
    - use every possible letter, number and char
    - need a lot of time and processing power
    - brute force atks require convertinng dict pwd from plaintxt to hash val
        - needs more cpu cycle time
- dictionary atk
    - use common words in dict
    - use variety of langs
    - many programs can build profiles of suspect to determine pwd
    - many pwd-protected OS and app store pwd in form of md5 or sha hash vals
- rainbow table
    - file containing hash vals for every possible pwd generated
    - no conversion needed
        - faster than brute force/dict atk
- salting pwds
    - make pwd cracking difficult
    - alter hash vals with extra bits added to pwd
        - make cracking more difficult


Summary
---
![](https://i.imgur.com/bhy1teA.png)
![](https://i.imgur.com/9fdjpIR.png)
![](https://i.imgur.com/eUjn8MS.png)





###### tags: `DFI` `DISM` `School` `Notes`