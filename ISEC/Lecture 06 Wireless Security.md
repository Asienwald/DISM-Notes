

Lecture 06 Wireless Security
===



## Table of Contents

- [Lecture 06 Wireless Security](#lecture-06-wireless-security)
  * [Wireless Attacks](#wireless-attacks)
    + [Bluetooth Attacks](#bluetooth-attacks)
      - [Bluejacking](#bluejacking)
      - [Bluesnarfing](#bluesnarfing)
    + [Near Field Communication (NFC) Attacks](#near-field-communication--nfc--attacks)
      - [Example of NFC Applications](#example-of-nfc-applications)
      - [Types of Attacks](#types-of-attacks)
    + [Radio Frequency Identification (RFID) Attacks](#radio-frequency-identification--rfid--attacks)
      - [Types of Attacks](#types-of-attacks-1)
    + [Wireless Local Area Networks Attacks](#wireless-local-area-networks-attacks)
      - [IEEE WLANs](#ieee-wlans)
      - [WLAN Hardware](#wlan-hardware)
      - [Types of Attacks](#types-of-attacks-2)
  * [WLAN Enterprise Attacks](#wlan-enterprise-attacks)
    + [Rogue Access Point](#rogue-access-point)
    + [Evil Twin](#evil-twin)
    + [Intercepting Wireless Data](#intercepting-wireless-data)
    + [Wireless Replay Attack](#wireless-replay-attack)
    + [Wireless Denial of Service Attack](#wireless-denial-of-service-attack)
    + [Wireless Home Attacks](#wireless-home-attacks)
  * [Vulnerabilites of IEEE Wireless Security](#vulnerabilites-of-ieee-wireless-security)
    + [Wired Equivalent Privacy (WEP)](#wired-equivalent-privacy--wep-)
    + [Wired Protected Setup (WPS)](#wired-protected-setup--wps-)
    + [MAC Address Filtering](#mac-address-filtering)
    + [SSID Broadcasting](#ssid-broadcasting)
  * [Wireless Security Solutions](#wireless-security-solutions)
    + [Wifi Protected Access (WPA)](#wifi-protected-access--wpa-)
      - [Temporal Key Integrity Protocol (TKIP) Encryption](#temporal-key-integrity-protocol--tkip--encryption)
      - [Preshared Key (PSK) Authentication](#preshared-key--psk--authentication)
      - [WPA Vulnerabilities](#wpa-vulnerabilities)
    + [WPA2](#wpa2)
      - [AES-CCMP Encryption](#aes-ccmp-encryption)
    + [IEEE 802.1x Authentication](#ieee-8021x-authentication)
      - [Extensible Authentication Protocol (EAP)](#extensible-authentication-protocol--eap-)
  * [More Wireless Security Protections](#more-wireless-security-protections)
    + [Rogue AP System Detection](#rogue-ap-system-detection)
    + [AP Types](#ap-types)
      - [Fat vs Thin APs](#fat-vs-thin-aps)
      - [Standalone vs Controller APs](#standalone-vs-controller-aps)
      - [Captive Portal APs](#captive-portal-aps)
    + [AP Configuration & Device Options](#ap-configuration---device-options)
  * [Chapter Summary](#chapter-summary)


Wireless Attacks
---
- atks against wireless system
    - bluetooth atks
    - NFC atks
    - radio freq identification systems
    - wireless lan atks

### Bluetooth Attacks
- bluetooth - wireless tech that uses short-range radio freq (RF) transmissions
    - provide rapid device pairings
    - personal area network (PAN) tech
- piconet
    - established when 2 bluetooth devices within range of ea other
    - 1 master device control all wireless traffic
    - 1 slave device takes commands
        - active slaves send transmissions
        - parked slaves connected but not actively participating

![](https://i.imgur.com/SrDsxxx.png)

#### Bluejacking
- atk that sends unsolicited msgs to bluetooth devices
- more annoying than harmful
    - no data stolen

#### Bluesnarfing
- atk that accesses unauth info from wireless device through bluetooth conn
    - often between phones & laptop
- atker copies emails, contacts & other data by connecting to bluetooth device w/o user knowledge


### Near Field Communication (NFC) Attacks
- near field comm (NFC)
    - set of standards used to establish comm between devices in close proximity
    - devices brought within 4cm of ea other & tapped tgt
        - comm established
- devices using NFC can be active/passive
    - passive nfc device
        - contain info that other devices can read
        - dont read/receive any info
        - Eg. NFC tag
    - active nfc device
        - can read info & transmit data

![](https://i.imgur.com/Z4mfYsz.png)

#### Example of NFC Applications
- automobiles
- entertainment
- office
- retail stores
- transportation
- contactless payment systems
    - consumer pay for purchase by tapping payment terminal with smartphone

#### Types of Attacks
![](https://i.imgur.com/CH3Iyqr.png)


### Radio Frequency Identification (RFID) Attacks
- radio freq identification (RFID)
    - commonly used to transmit info between employee inventory badges/tags/book labels/paper-based tags that can be detected by proximity reader
- most RFID tags are passive
    - dont have own power supply
        - hence very small
- current ver of rfid standards is Generation 2
    - contain security enhancements over prev version

#### Types of Attacks
![](https://i.imgur.com/JtbNXfa.png)


### Wireless Local Area Networks Attacks
- wlan designed to replace/supplement wired lan
- impt to know
    - history & specs of IEEE wlans
    - hardware needed for wireless network
    - diff types of wlan atks directed at enterprise & home users

#### IEEE WLANs
- institute of electrical & electronics engineers (IEEE) wlans
    - most influential org for computer networking & wireless comms
    - 1884
    - began developing network arch standards in 1980s
- 1997 - release of IEEE 802.11
    - standard for wlans
    - higher speeds (5.5mbps & 11mbps) added in 1999 - IEEE 802.11b
- IEEE 802.11a
    - specifies max rated speed of 54mbps using 5ghz spectrum
- IEEE 802.11g
    - preserve stable & widely accepted features of 802.11b
    - increase data transfer rates similar to 802.11a
- IEEE 802.11n
    - ratified in 2009
    - improvements
        - speed
        - coverage area
        - resistance to interference
        - strong security
- IEEE 802.11ac
    - ratified in early 2014
    - data rates over 7gbps

![](https://i.imgur.com/VkKByqt.png)


#### WLAN Hardware
- wireless client network interface card adapter
    - same func as wired adapter
    - antenna send & receive signals through airwaves
- access point (AP) major parts
    - antenna & radio transmitter/receiver send & receive wireless signals
    - bridging software to interface wireless devices to other devices
    - wired network interface allow it to connect by cable to standard wired network
    - AP funcs
        - act as base station for wireless network
        - act as bridge between wireless & wired networks
            - can connect ot wired through cable

![](https://i.imgur.com/L8vYL5I.png)


- wlan using AP is operating in __infrastructure mode__
- network not using AP oprating in __ad hoc mode__
    - devices only comm between themselves
        - cannot conenct to other networks
    - wifi alliance created similar tech specification called __Wi-Fi Direct__
- residential wlan gateway
    - used by small offices/home users to connect to internet
    - features
        - AP
        - firewall
        - router
        - dynamic host config protocol (DHCP) server
        - others

#### Types of Attacks
- continued below


WLAN Enterprise Attacks
---
- __hard edge__ - well-defined boundary that protects data & res in network
    - intro of wlans in enterprises changed hard edges to __blurred edges__

![](https://i.imgur.com/fnn9XhJ.png)
![](https://i.imgur.com/ufiRVb6.png)


- types of wireless atks
    - rogue access pts
    - evil twins
    - intercepting wireless data
    - wireless replay atks
    - denial of service atks

### Rogue Access Point
- unauth access pt that allow atker to bypass network security configs
- usually set up by insider (employee)
- may set up behind firewall, opening network to atks

### Evil Twin
- ap set up by atker
- mimic authorised ap
- atkers capture transmission from user to evil twin ap

![](https://i.imgur.com/yAUpNEK.png)


### Intercepting Wireless Data
- atker pick up RF signal from open/misconfiged ap
- using wlan to read data can yield significant info to atker regarding wired enterprise network

### Wireless Replay Attack
- AKA hijacking
- atker captures transmitted wireless data, record it & send to orig recipient w/o atker ebing detected
- accomplished using evil twin ap
- AKA mitm atk

### Wireless Denial of Service Attack
- RF jamming
    - atkers use RF interference to flood rf spectrum with enough interference to prevent device from comm with ap
- spoofing
    - atker create fake frame that pretends to come from trusted client
- manipulating duration field values
    - atkers send frame with duration field set to high value
    - prevents other devices from transmitting for that period of time

### Wireless Home Attacks
- most home users fail to config security on home networks
- atkers can
    - steal data
    - read wireless transmissions
    - inject malware
    - download harmful content


Vulnerabilites of IEEE Wireless Security
---
- orig IEEE 802.11 committee recognised wireless transmission are vulnerable
    - implemented several wireless security protections in standard
    - left others to wlan vendor's discretion
    - protections vulnerable & led to multiple atks

### Wired Equivalent Privacy (WEP)
- IEEE 802.11 security protocol designed to ensure only authorised parties can view transmissions
    - encrypt plaintext into ciphertext
    - secret key shared between client & ap
- vulns
    - only use 64bit or 128bit key
        - __initialisation vector (IV)__ only 24 of those bits
        - short length = easy break
    - violates cardinal rule of cryptography - avoid detectable pattern
        - atkers can see dupes when IVs start repeating

### Wired Protected Setup (WPS)
- optional means of configuring security on wlans
- 2 common wps methods
    - __PIN method__
        - use PIN printed on sticker of wireless router/displayed through software wizard
        - user enter pin & security config auto occurs
    - __push-button method__
        - user push btn & security configs happen
- design & implementation flaws
    - no lockout limit for entering PINs
    - last pin char is only checksum
    - wireless router reports validity of 1st & 2nd halves of pin separately

### MAC Address Filtering
- method to control wlan access
    - limit device's access to ap
- media access control (MAC) address filtering
    - used by nearly all wireless ap vendors
    - permits/blks device based on mac
- vulns
    - addresses exchanged unencrypted
        - atker can see addr of approved device & sub with own
    - managing large num of addr challenging

![](https://i.imgur.com/69CqEc1.png)
![](https://i.imgur.com/fmfeCom.png)

### SSID Broadcasting
- service set identifer (SSID)
    - user-supplied network name of wireless network
    - broadcast so any device can see
        - broadcast can be restricted
- some wireless security sources encourage users to config their APSs to prevent broadcast of SSID
- not advertisiing SSID only provide weak degree of security
    - limitations
        - SSID can be discovered when transmitted in other frames
        - may prevent users from freely roaming from 1 AP coverage to other
        - not always possible to off SSID beaconing


Wireless Security Solutions
---
- unified approach to WLAN security needed
    - IEEE & wifi alliance began developing security solutions
- standards used today
    - IEEE 802.11i
    - WPA & WPA2

### Wifi Protected Access (WPA)
- introduced in 2003 by wifi alliance
- subset of IEEE 802.11i
- 2 modes
    - WPA personal
    - WPA enterprise
- WPA addresses both encryption & auth

#### Temporal Key Integrity Protocol (TKIP) Encryption
- TKIP encryption
    - used in WPA
    - uses longer 128bit key than WEP
    - dynamically generated for ea new packet
    - includes __message integrity check (MIC)__ designed to prevent MITM atks


#### Preshared Key (PSK) Authentication
- auth for WPA personal uses preshared key (PSK)
- after AP configed, client device must have same key value entered
    - key shared prior to comm
- use passphrase to generate encryption key
    - must be entered on ea AP & wireless device in advance
- devices with secret key auto auth by AP

#### WPA Vulnerabilities
- key management
    - key sharing done manually w/o security
    - keys must be changed regularly
    - key must be disclosed to guest users
- passphrases
    - PSK passphrases of fewer than 20 chars subj to cracking

### WPA2
- 2nd gen of WPA
    - introduced in 2004
    - based on final IEEE 802.11i standard
- 2 modes
    - WPA2 personal
    - WPA2 enterprise
- addresses major security areas of WLANs
    - encryption
    - auth

#### AES-CCMP Encryption
- advanced encryption standard (AES) blk cipher
- AES performs 3 steps on every blk (128bits) of plaintext
    - within 2nd step, multiple iterations performed
    - bytes substituted & rearranged
- __counter mode with cipher block chaining message authentication code protocol (CCMP)__ - encryption protocol used for WPA2
    - specifies use of CCM with AES
- __cipher blk chaining msg auth code (CBC-MAC)__ component of CCMP provides data integrity & auth
- both CCMP & TKIP use 128bit key for encryption
    - both use 64bit MIC value

### IEEE 802.1x Authentication
- orignally developed for wired networks
- higher degree of security by implmenting port-based auth
- blks all traffic on port-by-port basis until client authenticated

![](https://i.imgur.com/6jm47Ac.png)

#### Extensible Authentication Protocol (EAP)
- framework for transporting auth protocols
- defines msg format
- uses 4 types of packets
    - request
    - response
    - success
    - failure
- common EAP protocol is __protected EAP (PEAP)__
    - simplifies deployment of 802.1x using microsoft windows logins & passwords
    - creates encrypted channel between client & auth server

![](https://i.imgur.com/wCwqvSp.png)


More Wireless Security Protections
---
- other security steps
    - rogue AP system detection
    - using correct type of AP
    - AP config settings
    - wireless peripheral protection

### Rogue AP System Detection
- rogue AP discovery tools - 4 types of wireless probes can monitor airwaves for traffic
    - wireless device probe
    - desktop probe
    - access pt probe
    - dedicated probe
- one suspicious signal detected by wireless probe
    - info sent to centralised db whr WLAN management system software compares it to list of approved APs
    - any device not on list considered rogue AP

### AP Types
- devided into
    - fat vs thin
    - controller vs standalone
    - captive portal APs

#### Fat vs Thin APs
- autonomous APs have intelligence to manage wireless auth, encryption & other funcs for wireless devices they serve
    - __fat APs__
- lightweight APs dont contain all management & config funcs found in fat APs
    - __thin APs__

#### Standalone vs Controller APs
- controller APs managed through dedicated __wireless LAN controller (WLC)__
- WLC is single device that can be configed & settings automatically distributed to all controller APs
- other advantages of controller APs
    - handoff procedure eliminated as all auths performed in WLC
    - offer tools that provide for monitoring env & providing info regarding best locations for APs, wireless AP config settings & power settings

![](https://i.imgur.com/8cwrttH.png)

#### Captive Portal APs
- use standard web browser to provide info
- gives wireless user the opportunity to agree to policy/present valid login credentials


### AP Configuration & Device Options
- other AP config settings designed to limit spread of wireless RF signal
    - so that min amt of signal extends past phy boundaries of enterprise to be accessible to outsiders
- site surveys
    - in-depth examination & analysis of wireless LAN site
- signal strength settings
    - some APs alow adjustment of power lvl which LAN transmits
    - reducing power allows less signal to rch outsiders
- spectrum selection
    - some APs provide ability to adjust freq spectrum settings including
        - freq band
        - channel selection
        - channel width

- antennas
    - AP shld be located near center of coverage area
    - place high on wall to reduce signal obstructions & deter theft
    - possibly, AP & antenna shld be positioned so minimal amt of signal reaches beyond security perimeter of building
- wireless peripheral protection
    - vulns in wireless mice & keyboards common
    - 1 atk can let threat actor inject mouse movements/keystrokes from nearby antenna up to 100 yards away
    - protections include
        - updating/replacing any vuln devices
        - switching to more fully tested bluetooth mice & keyboards
        - substitute with wired mouse/keyboard


Chapter Summary
---
![](https://i.imgur.com/kyZxutk.png)
![](https://i.imgur.com/HeJtbt3.png)
![](https://i.imgur.com/47yUbXx.png)




###### tags: `ISEC` `DISM` `School` `Notes`