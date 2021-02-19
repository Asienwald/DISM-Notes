

12 Rooting and Jailbreaking
===



## Table of Contents

- [12 Rooting and Jailbreaking](#12-rooting-and-jailbreaking)
  * [Table of Contents](#table-of-contents)
  * [Rooting and Jailbreaking](#rooting-and-jailbreaking)
    + [Rooting in Android](#rooting-in-android)
    + [Jailbreaking in IOS](#jailbreaking-in-ios)
    + [Motivation for End Users](#motivation-for-end-users)
    + [Warnings before Rooting/Jailbreaking](#warnings-before-rooting-jailbreaking)
    + [Jailbreaking iPhone](#jailbreaking-iphone)
    + [Rooting Android](#rooting-android)


Rooting and Jailbreaking
---
- devices has restrictions
    - limit app installation
    - limited access priv to device
    - code signing
        - 1 of most impt security mechanisms
        - all binaries libs must be signed by trusted authority code signing app
            - assure users that it's from a known source and app not modified since its last signed
- this escapes the restrictions
    - gain unrestricted device access

### Rooting in Android
- equal to jailbreaking
- unlock os so can install unapproved apps, delete unwanted bloatware, update os, rpelace firmware and customise anything
- allow user to gain root user priv
    - no restrictions on system settings
- android allow sideloading w/o rooting by default
    - install app from non-android market


### Jailbreaking in IOS
- required modification on os settings
    - form of priv esc via hardware/software exploits
    - enable installation of 3rd pt apps
- phone will work with app store
    - can still call after jailbroken


### Motivation for End Users
- more app sources
- access unauth apps
    - pirated software
    - firefox in iphone
- remove vendor-installed SW (bloatware)
    - improve perf
    - inc avail memory
        - ram/rom (mmc)
- access restricted hardware res
    - eg. bluetooth on kindle fire
    - perform system tweaking

### Warnings before Rooting/Jailbreaking
- use 3rd pt tools to escape control
    - ensure tools are secure
- voiding of warranty
- error and perf issue
    - not tested
    - can cause unstability
- dont root or jailbreak everyday product devices
- check org's legal posture (security policy) on permitted activities with corporate devices
    - eg. EULA (end user license agreement) violation


### Jailbreaking iPhone
- use tools like
    - JailbreakMe
        - easiest way to free device
        - fully customisable, themeable
    - Redsn0w
    - Evasi0n
- vulns exploited usually fixed asap in next revision of ios by apple
    - new ver need new set of vulns to jailbreak device

### Rooting Android
- varies from device
    - diff in hardware
- rooting steps
    - flash recovery
        - enter recovery to backup device and load new os
    - flash boot (fastboot)
        - flash imgs like recoveries, bootloaders and kernels to device
    - local priv esc
    - ADB priv esc
        - android debug bridge (ADB) lets you communicate android device from pc using cmd line
- for some methods to work, u need
    - allow unsigned software
        - eg. sideloading
    - enable usb debugging
        - dev mode in android that allows newly programmed apps to be copied via usb to device for testing
- tools used
    - ADB
        - old sch
        - need drivers, scripts, SU apk
    - z4root
        - from android 2.3
    - SuperOneClick
        - need adb
    - flashing recovery and custom ROM
    - motochoppper
        - android 4.32
- once rooted, adb can yield rootshell when local privesc request (su) requested
    - `superuser.apk` will prompt you
    - once granted by user, rootshell is granted to the shell
- NOTE
    - keep in mind that if the phone is stolen, data can be extracted





###### tags: `DFI` `DISM` `School` `Notes`