

11 IOS Forensics
===




## Table of Contents

- [11 IOS Forensics](#11-ios-forensics)
  * [Table of Contents](#table-of-contents)
  * [IOS](#ios)
    + [Enhanced Features on IOS](#enhanced-features-on-ios)
    + [How does it Work?](#how-does-it-work-)
    + [Partitions](#partitions)
    + [Operating System](#operating-system)
      - [Core Layers](#core-layers)
      - [Core Services](#core-services)
      - [Media Layer](#media-layer)
      - [Cocoa Touch (UI)](#cocoa-touch--ui-)
    + [App Integration with IOS](#app-integration-with-ios)
      - [Commonly Used Dirs in IOS](#commonly-used-dirs-in-ios)
      - [Typical Users Home Dir](#typical-users-home-dir)
    + [Jailbreaking](#jailbreaking)
  * [Forensics Values](#forensics-values)
    + [Iphone Forensics Evidence](#iphone-forensics-evidence)
    + [IOS Handling Procedures](#ios-handling-procedures)
    + [Check Apps](#check-apps)
    + [Forensic Acquisition](#forensic-acquisition)
      - [iPhone/iPad/iTouch Advanced](#iphone-ipad-itouch-advanced)
      - [iPhone/iPad/iTouch Acquisition](#iphone-ipad-itouch-acquisition)
    + [Device Seizure and IOS](#device-seizure-and-ios)
    + [EXIF Files](#exif-files)
      - [Images](#images)
    + [Plist Files](#plist-files)
    + [Important Folders](#important-folders)
    + [iTunes](#itunes)
    + [Importing iPhone Backup Files](#importing-iphone-backup-files)


IOS
---
- iphone os = ios

### Enhanced Features on IOS
- maps
    - updated views
        - more recorded data
    - siri
        - avail on more devices = user expansion
    - facebook
        - cross integration = more shared data
    - shared photo streams
        - easy ios device shares = data copies
    - passbook AKA apple wallet
        - purchasing system = security holes
    - facetime
        - works with cellular networks = more data access with vid
    - phone
        - threaded for activities
        - timestamp overlap
    - mail, safari, accessibility
        - improved usability for increased users = more cases for forensics

### How does it Work?
- iphone has 2 processors
    - 1st works on GSM conn
        - phone calls
    - 2nd has mac os
- **device seizure (DS)**
    - software in paraben AKA E3 platform
    - can acquire 2nd part of data
- acquisition done in 2 steps
    - mac os img received from device
    - mac os img parsed and investigated

### Partitions
- os partition
    - 500mb
    - uses HFSX
        - ext of HFS plus file system
        - currently updated to apple file system (APFS)
- data partition
    - focus on investigation
    - contains user data and files

### Operating System
- ios built on darwin foundation
    - unix env behind all apple os
    - forms core set of components which mac os x and ios is based
- os uses <1gb mem to operate

![](https://i.imgur.com/Da50Syx.png)

#### Core Layers
- core os and services layer contains these fundamental interfaces
    - those used for accessing files
    - low lvl data types
    - bonjour services
    - network sockets

#### Core Services
- mostly c-based
- include tech/frameworks like
    - core foundation
        - AKA CF
        - low lvl routines
            - eg. facilitate internalisation
    - CF network
        - eg. socket
    - sqlite
    - access to POSIX (portable os interface) threads and unix sockets

#### Media Layer
- OpenAL
- audio mixing and recording
- video playback
- img file formats
- Quartz
- core animation
- OpenGL ES
    - graphic rendering

#### Cocoa Touch (UI)
- manage multi-touch events and controls
- use accelerometer
- view hierarchy
- localisation
    - i18n
- use of embedded camera


### App Integration with IOS
- app isolated in sandbox
    - only create data in home dir
- during installation of new app, installer creates num of container dir for app inside sandbox dir

![](https://i.imgur.com/04Mq3Dc.png)

#### Commonly Used Dirs in IOS
- home dir
    - `<App Home>/AppName.app`
    - contains app and all its res
- user data
    - `<App Home>/Documents/`
    - store user-generated content
- outside access
    - `<App Home>/Documents/InBox`
    - used to access files that app asked to open by outside entities
- temp files
    - `<App Home>/tmp`
    - use to write temp files that dont need to persist between launches of app

#### Typical Users Home Dir
- applications
    - user specific apps
- desktop
- documents
- downloads
- library
    - user specific app files but hidden
- movies
- music
- pictures
- public
    - content user wants to share
- sites
    - webpages used by user


### Jailbreaking
- jailbreaking
    - unlocks security settings on device so have admin control
    - others can potentially have admin control too
- provides root access to os
- opens up all security on device
    - no sandbox for apps
    - no security patches
    - can use device on any carrier
    - opens device for malware/spyware


Forensics Values
---
### Iphone Forensics Evidence
- exchangeable img file (EXIF) data
    - img files
- plist (property list) files
    - settings file AKA properties file
- desktop backups
    - backup data by itunes
    - can use program to extract desktop backup data
- device data/backup

### IOS Handling Procedures
- use faraday protection bag
    - copper lining in interior seal
    - stop phone from contacting others to avoid being remotely wiped or tracked
- charge device to 100%
    - avoid power hogs
- plan for long acquisition time
- look for backup records on comp


### Check Apps
- login to itunes
- check most popular apps
    - texting
    - documents
    - com
    - comp related
- check on device


### Forensic Acquisition
- use paraben's device seizure (DS) acquisition wizard to acquire evidence

#### iPhone/iPad/iTouch Advanced
- used with most ios devices
- backup of user oriented files
    - this plugin uses itunes to create backup of device
- doesnt access pri file system (sys files) of device
- recovers deleted dta
- allows logical acq of backup from iphones

#### iPhone/iPad/iTouch Acquisition
- acquires the following data
    - address book
    - sms history
    - call history
    - imessages
    - calendar
    - notes
    - file system
    - maps bookmarks/history/directions
    - mac addr

### Device Seizure and IOS
- during acq device might need conn to itunes
    - use device seizure (DS) to establish this conn
- parsed data includes
    - voice memo
    - properties
    - cookies
    - sms history
    - imessages
    - youtube bookmarks
    - mailaccounts
    - safari suspended state
    - safari bookmarks
    - safari history
    - dynamic text
    - notes
    - calendar
    - maps history/bookmarks/dirs
    - contacts
    - call history
- parsed deleted data
    - sms history
    - safari bookmarks
    - notes
    - calendar
    - contacts
    - call history

### EXIF Files
- exchangeable img file formats (exif)
    - standard that specifies formats for systems handling img and sound files like cams, scanners etc.
- use exif reader

![](https://i.imgur.com/pFdblpE.png)


#### Images
- ea img associated with 2 files
    - img viewed on iphone screen
    - thumbnail

![](https://i.imgur.com/CDRmzAA.png)

- iphone dont name img using data and timestamp
    - named in numerical order
        - eg. IMG_0065.jpg, IMG_0066.jpg
    - thumbnails too
        - eg. IMG_0065.thm
- images stored in same folder

### Plist Files
- .plist files
    - used to store various types of data
    - file storage containing info on cache, history and config settings
    - is usually plaintxt .xml file or binary file
- need to be examined for evidence
    - valuable repo for historical system and user specific configs and actions

### Important Folders
- email uses html headers
    - run keyword search of .html to scan for active and deleted mail
- notes
- maps
    - xml format storage for google maps
    - `Route.plist` shows when the user queried the map device for dirs
- other network info, cookies and bookmarks


### iTunes
- data sync
- other funcs
    - manage files, apps, software ver etc.
- info avail
    - serial num with itunes
    - IMEI
    - ICCID (integrated circuit card id) SIM num
    - dat and time of conn

![](https://i.imgur.com/TdcRf41.png)
- can backup iphone data with itunes
    - depending on os, backup location varies

### Importing iPhone Backup Files
- ds parben has feature to import backup files
    - must have access to comp the iphone synced with
    - backup files copied to portable device
    - use file dropdown menu to start import wizard and pt ot backup files



###### tags: `DFI` `DISM` `School` `Notes`