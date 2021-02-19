

10 Android Forensics
===




## Table of Contents

- [10 Android Forensics](#10-android-forensics)
  * [Table of Contents](#table-of-contents)
  * [Android](#android)
    + [Architecture](#architecture)
    + [Android Structure](#android-structure)
    + [DVM](#dvm)
    + [Android Data](#android-data)
      - [Logical Data](#logical-data)
      - [Location of Data](#location-of-data)
  * [Android Security](#android-security)
    + [Security Program](#security-program)
    + [Key Security Features](#key-security-features)
    + [Rooting Device](#rooting-device)
    + [Access to Personal Information](#access-to-personal-information)
  * [Data Acquisition on Android](#data-acquisition-on-android)


Android
---
- is open src phone platform based on linux kernel
    - developed by google, now maintained by open handset alliance
        - is grp of 47 companies tgt to produce better mobile experience

### Architecture
- apps
    - builtin and user's apps
- app framework
    - written in java to provide standard platform and api
    - work as toolkit used by all apps
- libraries
    - includes
        - sqlite
        - c/c++ libs
        - 3d graphics
    - is whr core android platform power comes from
- android runtime
    - **Dalvik VM (DVM)** and Libs (Java 5 Std Edition)
    - designed to run in env with limited batt/memory and cpu
        - DEX files (bytecode) run in this env
- linux kernel
    - provides many useful device drivers and
        - process management
        - memory management
        - networking and security in core infrastructure
            - robust and well proven

### Android Structure
- apps for android developed in java
- run in separate dalvik vm AKA **sand box**
    - due to compactness, multiple vm can be run on mobile
    - run under unique user id and process
        - enforce data security
- apps can only access data within their DVM unless another app and phone owner specifically allows data to be shared

### DVM
- dalvik vm alows multiple apps to run concurrently
    - ea app is separate vm
- compiled .java/.class into dalvik exe (.dex) files
    - compact and efficient
    - use `dx` to transform java bytecode to .dex-formatted bytecodes
- data stored in sqlite db
- NOTE
    - android 5 onwards uses **android runtime (ART)** that leverages DVM tech

### Android Data
- android forensics diff from regular disk forensics
    - supports various file systems specific to android
- create baseline for examiniation
    - sms
    - google play
    - phone call and call history
    - email
    - cam/vid
    - browser and browser history
    - etc.
- use paraben

#### Logical Data
- common user data
    - eg. contacts, sms, mms, history, call logs, media files etc.
- can also sort the data found

![](https://i.imgur.com/PAsL6OK.jpg)

#### Location of Data
- files stored in device storage
    - and removable secure digital (SD) mem card
- data locations
    - dalvik-cache
        - .dex files run
    - anr (app not response)
        - debug/thread info with timestamps
    - app
        - .apk files - install bundles for apps
    - data
        - subdirs per app with sqlite db
    - misc
        - dhcp
        - wifi
        - etc.
    - system
        - packages.xml - installed apps
    - checkin.db
        - conn up/down info etc.


Android Security
---
### Security Program
- key component of android security program
- design review
    - open src design allow for multi tier review of system
        - internal
            - major features reviewed with security control integrated into system
        - pentest
            - reviewes performed by
                - android security team
                - google's infosec engineering team
                - independent security consultants
        - community
            - android open src proj enables broad security review by any interested party
- incident response
    - live updates to devices
        - fulltime android sec team monitors android-specific and general sec community for discussion of potential vulns

### Key Security Features
- robust security at os lvl through linux kernel security
- compulsory app sandbox for all apps
- app signing
- app and user granted perms
- etc.

### Rooting Device
- run with root lvl perms
    - ful access to all apps and app data
    - inc security exposure to malicious apps and potential app flaws
- allow user to reinstall new ver of os
- bypass protection on device

### Access to Personal Information
- limited by api
    - sensitive apis intended for use by trusted apps only
    - protected through security mechanism AKA **permissions**
- by default android app can only access limited range of sys res on phone

![](https://i.imgur.com/34Tyfxh.png)



Data Acquisition on Android
---
- DS (paraben) performs these actions
    - before acq
        - `AndroidService.apk` installation pkg written to `/data/local/tmp` folder
    - `com.paraben.service` service installed to sys folder
    - after acq
        - installed service uninstalled automatically
        - installation pkg removed
- does not dmg the device






###### tags: `DFI` `DISM` `School` `Notes`