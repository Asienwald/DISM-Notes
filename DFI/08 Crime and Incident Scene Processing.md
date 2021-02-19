

08 Crime and Incident Scene Processing
===



## Table of Contents

- [08 Crime and Incident Scene Processing](#08-crime-and-incident-scene-processing)
  * [Table of Contents](#table-of-contents)
  * [Identifying Digital Evidence](#identifying-digital-evidence)
    + [Rules of Evidence](#rules-of-evidence)
      - [Computer Records](#computer-records)
      - [Properties](#properties)
  * [Collecting Evidence in Private-Sector Incident Scenes](#collecting-evidence-in-private-sector-incident-scenes)
  * [Processing Law Enforcement Crime Scenes](#processing-law-enforcement-crime-scenes)
    + [Concepts and Terms in Warrants](#concepts-and-terms-in-warrants)
  * [Preparing for a Search](#preparing-for-a-search)
    + [Preparing to Acquire Digital Evidence](#preparing-to-acquire-digital-evidence)
  * [Processing Incident or Crime Scene](#processing-incident-or-crime-scene)
    + [Guidelines](#guidelines)
    + [Processing Data Centers with RAID Systems](#processing-data-centers-with-raid-systems)
      - [Technical Advisor](#technical-advisor)
  * [Documenting Evidence in Lab](#documenting-evidence-in-lab)
    + [Processing and Handling Digital Evidence](#processing-and-handling-digital-evidence)
    + [Storing Digital Evidence](#storing-digital-evidence)
    + [Evidence Retention and Media Storage Needs](#evidence-retention-and-media-storage-needs)
    + [Documenting Evidence](#documenting-evidence)
    + [Obtaining Digital Hash](#obtaining-digital-hash)
  * [Reviewing a Case](#reviewing-a-case)
    + [Sample Civil Investigation](#sample-civil-investigation)
    + [Sample Criminal Investigation](#sample-criminal-investigation)
  * [Summary](#summary)

Identifying Digital Evidence
---
- digital evi
    - any info stored/transmitted in digital form
- diff between doc evi and digital evi
    - doc evi always visible on its face
- US court accept digital evi as phy evi
    - treated as tangible obj
    - eg. scientific working grp on digital evi (SWGDE) set standards for recovering , preserving and examining digital evi
- tasks performed with digital evi
    - identify digital info/artifacts that can be used as evi
    - collect/preserve/document evi
    - analyse/identify/organise evi
    - rebuild evi or repeat situation to verify that results can be reproduced reliably

![](https://i.imgur.com/PumUMSF.png)
- systematic approach for collecting digital devices and processing criminal/incident scene

### Rules of Evidence
- consistent practices help verify work and enhance cred
    - handle evi consistently
- comply with state's rules of evi or federal rules of evi
    - eg. security and accountability control for evi
- evi submitted in criminal case can be used in civil suit
    - vice versa
- keep current on latest rulings and directives on collecting, processing, storing and admitting digital evi
- digital evi diff from phy since changed more easily
    - only way to detect changes by comparing hashes
- most courts interpret comp records as hearsay evi
    - hearsay is second hand/indirect evi
        - evi of statement made other than witness
- digital records admissible if business record

#### Computer Records
- 2 types of comp records
    - comp generated records
        - data maintained by system
        - not created by human
        - eg. log files
    - comp stored records
        - data created by human saved on comp
        - eg. spreadsheet/word doc
- comp and digital records must be shown to be authentic and trustworthy to admit into court
    - comp gen records authentic if program creating it is functioning correctly
        - no bugs
        - exception to hearsay rule
    - collect evi according to proper steps fo ensure its authentic
- when attorneys challenge digital evi, they raise issue whether comp gen records are altered or damaged
- one test to prove comp stored records auth is demonstrating that a specific person created them
    - eg. file metadata to see author
    - HOWEVER records recovered from slack space/unallocated disk space usually dont identify author
- process of establishing digital evi's trustworthiness originated from **best evidence rule**
    - best evi rule states
        - to prove content of written doc/recording/photo, the orig is required
        - allow dupe when its produced by same impression as orig
            - not always possible to produce orig
            - eg. when cannot use orig evi
                - network servers - cannot remove from network to acquire evi since will cause harm to business/owner (innocent)
- data can be admitted in court as long as bit-stream copies of data created and maintained
    - though not best evi

#### Properties
- 5 props
    - admissible
    - authentic
    - complete
    - reliable
    - believable



Collecting Evidence in Private-Sector Incident Scenes
---
- use inventory db too understand what hardware/software needed to analyse policy violation
- corporate policy statement abt misuse of digital assets
    - allow corporate inves. to conduct **covert surveillance**
        - survelliance on someone w/o person noticing it
    - access company systems w/o warrant
- companies must display warning banner and publish policy
    - state that they reserve the right to inspect comp assets at will
- corporate inves. shld know what circumstance they can examine employee's comp
    - every org must have well-defined process describing this
- if inves finds employee guilty of a crime
    - employer can file criminal complaint with police
    - inves. shld immediately report to corporate management
- employers interested in enforcing company policy, not seek and prosecute employees
    - corporate inves. concerned with protecting company's assets
- if discover evi of crime during company policy inves.
    - determine whether incident meets elements of law
    - inform management of incident
    - stop inves. to ensure dont violate 4th amendment restrictions on obtaining evi
    - work with corporate attorney on how to respond to police req for more info


Processing Law Enforcement Crime Scenes
---
- must be familiar with crminal rules of search and seizure
    - understand how search warrant works and how to process
- law enforcement officer can search and seize evi only with **probable cause**
    - reasonable grounds to believe that person has committed crime
        - to justify making search/preferring charge
    - refers to standard specifying whether police officer has right to make arrest, conduct search or obtain warrant for arrest
- with probable cause, officer can obtain search warrant from judge
    - authorise search and seizure of specific evi
- 4th amendment states that only warrants describing place to be searched and persons/things to be searched can be issued

### Concepts and Terms in Warrants
- **innocent info**
    - unrelated info
        - often included in info u looking for
        - sort info to obtain what u need
    - eg. enron case - by use of accounting loopholes and poor financial reporting
- judges often issue **limiting phrase** to warrant
    - allow police to separate innocent info from evi
    - warrant must list items to be seized
- plain view doctrine
    - objs falling in plain view of officer has right to be viewed and subject to seizure w/o warrant
        - can be introduced as evi
    - 3 criterias
        - officer is legally allowed to be whr he/she is
        - ordinary sense must not be enhanced by advanced tech
        - discovery must be by chance
    - HOWEVER, plain view's doctrine rejected in digital forensics
        - eg. if examiner finds extra info relating to diff crime, must get extra warrant/expansion of existing warrant to cont search for said crime


Preparing for a Search
---
- tasks
    - get ans from victim/informant
        - manager/coworker of person of interest to inves.
        - police assigned to case
        - law enforcement witness

- steps
    - Identify Nature of Case
        - private or public sector
        - dictates how u proceed and types of assets/res to use
    - Identify type of os or digital evi
        - for law enforcement
            - difficult since crime scene not controlled
        - identify os/device by estimating size of drive on suspect comp
            - how many devices to process at scene
        - determine os/hardware involved
    - determine whether u can seize comps/devices
        - type of case and location of evi
            - can u remove the evi?
        - law enforcement inves need warrant to remove comps from scene and transport to lab
            - if removing comps will irreplacable harm business, shldnt be taken offsite
        - extra complications
            - file stored offsite accessed remotely
            - avail of cloud storage - cannot locate physically
                - stored on drives with multiple subscribers
        - determine res needed to acquire evi and tools to speed data acquisition if not allowed to take comps
    - use extra technical expertise
        - specialised help to process incident/scene
            - specialists in
                - OS
                - RAID servers
                - db
        - educate specialists in inves. techniques too prevent evi dmg
    - determine tools needed
        - after info gathering on incident/scene
        - create **initial resp field kit**
            - lightweight and easy to transport
        - create **extensive resp field kit**
            - all tools u can take to field
            - extract only items needed when at scene

![](https://i.imgur.com/W2oPuOK.png)
![](https://i.imgur.com/hdLFGXw.png)


### Preparing to Acquire Digital Evidence
- depends on nature of case and alleged crime
- ask supervisor/senior
    - need take entire comp and all peripherals in immediate area?
    - how to protect comp and media during transportation to lab?
    - comp powered on when arrive?
        - data might be lost if machine powered down
    - is suspect in immediate area?
        - sometimes company dw employee to know inves. is happening
    - did suspect dmg/destroy comp/peripherals?
    - need to seperate suspect from comp?

Processing Incident or Crime Scene
---
### Guidelines
- keep journal to doc activities
- secure scene
    - professional and courteous to onlookers
    - remove unrelated people
- video and record area around comp
    - return belongings to orig locations
    - pay attention to details
- sketch incident/scene
- check state of comps asap
- dont cut power to running system unless is older windows 9x or MS-DOS system
    - might lose essential network activity records w/o proper shutdown
- save data from current apps as safe as possible
- record all active windows/shell sessions
- note everything u do from live suspect comp
- close apps and shutdown comp
- bag and tag evi
    - assign 1 person to collect and log all evi
        - min num of people handling evi
        - ensure integrity
    - tag all evi with current date time, serial nums or unique features, make and model, and name of person collecting it
    - 2 separate logs of collected evi
        - verification and audit purpose
    - maintain constant control of collected evi and crime scene
- look for related info
    - pwd, pin, bank acc
- collect doc and media related
    - hardware/software/backups/doc/manuals

### Processing Data Centers with RAID Systems
- space acquisition
    - technique for extracting evi from large systems
    - only extract related data
    - disadvantage
        - dont reciver data in free/slack space

#### Technical Advisor
- can help
    - list tools needed to process incident
    - guide whr to locate data and help extract log records
        - or other evi from large RAID servers
    - create search warrant by itemising what u need for warrant
- responsibilities
    - know all aspects of seized item
    - direct investigator handling sensitive material
    - help secure scene
    - document planning strategy
    - conduct ad hoc trainings on tech and components seized and searched
    - document activities
    - conduct search and seizure


Documenting Evidence in Lab
---
- record activities and findings
    - maintain journal
    - serves as reference for methods used to process evi
- goal to reproduce same results when another investigator repeat steps

### Processing and Handling Digital Evidence
- maintain integrity of evi in lab
- steps to create img files
    - copy all files to large drive
    - use forensics tool to analyse evi
    - run md5 or sha1 hashing algo on img files
    - secure original media in evi locker

### Storing Digital Evidence
- media used to store evi depends on how long u need to keep it
- cd, dvd, dvd-r, dvd+r, dvd-rw
    - ideal
    - capacity
        - up to 17 gb
    - lifespan
        - 2 to 5 years
- magnetic tapes - 4mm DAT
    - capacity
        - 40 to 72 gb
    - lifespan
        - 30 years
    - costs
        - drive
            - $400 to $800
        - tape
            - $40
- super digital linear tape (super DLT or SDLT)
    - designed for large RAID data backups
    - can store > 1tb
    - smaller SDLT drives can connect to workstation through SCSI card
- dont rely on media storage method to preserve evi
    - make 2 copies of every img to prevent 2 imgs

### Evidence Retention and Media Storage Needs
- help maintain chain of custody for digital evi
    - paper trial that records sequence of custody
    - restrict access to lab & evi storage area
- lab shld have sign in roster for all visitors
    - maintain logs for period based on legal requirements
- might need to retain evi indefinitely
    - check with local prosecuting attorney's office or state laws to ensure u in compliance

![](https://i.imgur.com/cvhbJSG.png)


### Documenting Evidence
- create/use evi custody form
    - has funcs
        - identify evi
        - identifies who handled evi
        - lists date and times evi handled
    - extra info
        - section listing md5 and sha1 hashes
    - include detailed info to ref
- evi bags also include labels or evi forms to document evi
    - use antistatic bags for electronic components

### Obtaining Digital Hash
- cyclic redundancy check (crc)
    - math algo that determines wheher file's contents changed
    - not forensic hashing algo
- message digest 5 (md5)
    - math formula that translates file into hex val or hash val
    - hash changes if bit or byte changes
    - verify non tampered file
- 3 rules
    - cant predict hash val of file or device
    - no 2 hash vals can be same
    - hash change if anything in file change
- secure algo ver 1 (sha1)
    - newer hash algo
        - not secure now

Reviewing a Case
---
- general tasks to perform
    - identify case requirements
    - pplan inves.
    - conduct inves.
    - complete case report
    - critique case

![](https://i.imgur.com/qFwuWTR.png)

### Sample Civil Investigation
- most cases in corporate env considered low level investigations
    - or non criminal cases
- common activities and practices
    - recover specific evi
        - eg. outlook
    - covert surveillance
        - must be well defined in company policy
        - risk of civil or criminal liability
    - sniffing tools for data transmissions
        - eg. wireshark

### Sample Criminal Investigation
- comp crimes eg
    - fraud
    - check fraud
    - homicides
    - etc
- need search warrant to seize evi
    - limit area

Summary
---
![](https://i.imgur.com/cI9dYMb.png)
![](https://i.imgur.com/hovlrXl.png)
![](https://i.imgur.com/Gw0xFZ2.png)





###### tags: `DFI` `DISM` `School` `Notes`