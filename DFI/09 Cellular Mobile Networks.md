

09 Cellular Mobile Networks
===



## Table of Contents

- [09 Cellular Mobile Networks](#09-cellular-mobile-networks)
  * [Table of Contents](#table-of-contents)
  * [How do Cellphones Work?](#how-do-cellphones-work-)
    + [Cellular Layout](#cellular-layout)
    + [Cellular Division](#cellular-division)
    + [Cell Antennas](#cell-antennas)
      - [Find Towers](#find-towers)
  * [Data Transmission in Mobile Networks](#data-transmission-in-mobile-networks)
    + [MTSO](#mtso)
      - [How Data is Transmitted](#how-data-is-transmitted)
    + [Wireless Frequency](#wireless-frequency)
    + [What Happens...](#what-happens)
    + [Cellular Hand off](#cellular-hand-off)
    + [Diff between Hard and Soft hand off](#diff-between-hard-and-soft-hand-off)
  * [Cellular Subsets](#cellular-subsets)
    + [Access Technologies](#access-technologies)
    + [TDMA](#tdma)
    + [iDen](#iden)
    + [CDMA](#cdma)
      - [CDMA Family](#cdma-family)
      - [BitPIM Software for CDMA](#bitpim-software-for-cdma)
      - [Qualcomm for CDMA](#qualcomm-for-cdma)
    + [GSM](#gsm)
  * [Cell Phone Identification Numbers](#cell-phone-identification-numbers)
    + [Mobile Identity Number (MIN)](#mobile-identity-number--min-)
    + [Electrical Serial Number (ESN)](#electrical-serial-number--esn-)
    + [Mobile Equipment ID (MEID)](#mobile-equipment-id--meid-)
    + [International Mobile Equipment Identity (IMEI)](#international-mobile-equipment-identity--imei-)
      - [IMEI Checksum Verification](#imei-checksum-verification)
    + [International Mobile Subscriber Identity (IMSI)](#international-mobile-subscriber-identity--imsi-)

How do Cellphones Work?
---
- mode of communication
    - full duplex
        - 2 channels
        - speak and listen at same time
        - cell phones essentially 2 way radio
            - radio transmitter
            - radio receiver
            - phone converts voice into electrical signal then transmit via radio waves to nearest cell tower
    - half duplex
        - cb radios (citizen band)
            - radio freq signal <-> electrical signal
        - only speak one at a time
        - eg. walkie talkie
- use radio waves to talk to cell tower that connects it to rest of phone network

### Cellular Layout
- phone network composed of **cell** or signal area
    - cells overlap or join to form large coverage area
    - users on network can cross into diff cells w/o losing conn
- phone networks allows for **freq reuse**
    - below, cell 1s on same freq but wont interfere due to phy separation
    - inteference called **crosstalk**

![](https://i.imgur.com/AuyomC7.png)

### Cellular Division
- cellular device can comm with another
- cells in hex shapes
    - preferred than square or circle as covers entire area w/o overlapping

![](https://i.imgur.com/V83sOAF.png)

### Cell Antennas
![](https://i.imgur.com/hbydZSD.jpg)
![](https://i.imgur.com/EQS8uO6.jpg)

#### Find Towers
![](https://i.imgur.com/ahEOUeq.png)
- http://www.cellreception.com/towers


Data Transmission in Mobile Networks
---
### MTSO
- mobile telephone switching office (mtso)
    - contains switching eq for routing mobile phone calls 
    - handles entire cell network
    - controls **handoff**
        - process of transferring ongoing call or data session from one channel (cell) to another channel (cell)
    - comm with PSTN (public switch telephone network)
        - landline network
    - brain of cell phone network
- mtso evaluates signal strength between device and network
    - tell device/network to make appropriate adjustments to transmission

![](https://i.imgur.com/4JokKd1.png)

#### How Data is Transmitted
![](https://i.imgur.com/f4k3Rkb.png)


### Wireless Frequency
- transmission of voice or data through use of electric waves set to specific freq
    - num waves per second = freq
    - freq measured in hz
    - 1 hz = 1 complete wave length per sec

![](https://i.imgur.com/inLnLny.png)

### What Happens...
- when phone turns on

![](https://i.imgur.com/dO7HPpi.png)

- when place call
![](https://i.imgur.com/aHuvZo4.png)


### Cellular Hand off
- if signal on channel from tower weakens during a call, another tower and handoff needed
    - if no other tower with stronger signal, call dropped

![](https://i.imgur.com/FEf32Jr.png)

### Diff between Hard and Soft hand off
![](https://i.imgur.com/RxUK5i1.png)


Cellular Subsets
---
### Access Technologies
- how phone talks to tower
    - AMPS advanced mobile phone system
        - fdma
        - 800 mhz
        - 1g
        - analog
    - TDMA time division multiple access
        - 2g
        - digital
    - iDen integrated digital multiple access
        - 2g
        - digital
    - CDMA code division multiple access
        - 2g/3g
        - digital
    - GSM global system mobile comm
        - 2g
        - digital
    - W-CDMA wideband CDMA
        - 3g
        - digital
    - OFDM orthogonal freq-div multiple access
        - 4g
        - digital

### TDMA
- time div multiple access
    - method of digitizing and compressing
    - num of equal timeslots configed for ea freq channel
    - divides convos by freq and time
    - outdated tech
- facilitates many users to share same freq w/o interference
    - divides signal into diff timeslots and inc data carrying capacity
- breaks up freq allocation by time
    - eg. 6.7ms
- 2 channels used
    - decoding
    - encoding

### iDen
- integrated digital enhanced network
    - based on tdma
- iden phones can support sms msgs, voice mail and data networking eg. vpn, internet and intranets
- allow users to take advantage of **PTT (push to talk)** walkie talkie tech
    - half duplex
    - used by
        - sprint
            - shutdown in 2013
        - at&t
        - verizon

### CDMA
- code div multiple access
- uses spread spectrum tech
    - spreads info contained in particular signal of interest over greater bandwidth than orig
- assigns code to ea piece of data passed across spectrum
- newer tech still uses orig tdma concept
    - deemed more superior to fdma and tdma
- cannot carry voice and data at same time
- every comm channel uses full avail spectrum
- 2 channels
    - encoding
    - decoding
- spread spectrum
    - channels spread across entire freq range instead of 1 dedicated one
        - 1850 mhz - 1990 mhz

![](https://i.imgur.com/FxQ9rBc.png)

#### CDMA Family
- cdmaOne (2g)
    - orig cdma system
- cdma2000
    - 3g
    - evolved from cdmaone
    - fam of tech for 3g cellular comm for transmission of voice, data and signals
    - 1xRTT (voice), 1xEV-DO (3g wireless standard data)
- W-CDMA
    - 3g
    - borrows ideas from cdma
    - use gsm tech and evolve into UMTS (universal mobile telecomms service)

#### BitPIM Software for CDMA
- is open src cross platform that allows u to view and manipulate data on many cdma phones
    - include phonebook, calendar, wallpapers, ringtones and filesystem
- analyse most qualcomm cdma chipset based phones
- PIM = personal info management

#### Qualcomm for CDMA
- founded in 1985 by multinational semiconductor and telecomms eq company
    - created CDMA and components in 1990s
    - orig built base stations, chipsets and phones
    - owns patent on CDMA chipset tech


### GSM
- based on TDMA
    - 70%-80% of phones
- digital cellular tech for transmitting mobile voice and data services
- established in 1987 as standard
    - avail in >212 countries
- global systems for mobile comm with freq 850-1900mhz
- uses SIM tech

![](https://i.imgur.com/A06ytH5.png)


Cell Phone Identification Numbers
---
### Mobile Identity Number (MIN)
- 10 digit
    - more with country code
    - assigned by carrier
    - used for phone identification
    - eg. (303)866-1010
- 2 parts
    - MIN 1
        - 24 bit number after area code
    - MIN 2
        - area/mobile subscriber code
- can be ported

### Electrical Serial Number (ESN)
- unique 32bit number assigned to ea TDMA or CDMA (non GSM) device
    - like mac addr
- uses 14 bit code for manufacturer code
    - since 8bit almost exhausted

![](https://i.imgur.com/uEe03md.png)

### Mobile Equipment ID (MEID)
- rpelace soon exhausted ESN for CDMA devices
- all fields are hex vals
    - RR
        - regional code
        - global administered
    - XXXXXX
        - 000000 - for small quantities of test/prototype mobiles
        - 000001 - FFFFFE
            - reserved for regional admin bodies or mobile manufacturers
            - subject to industry agreement
    - ZZZZZZ - manufacturer assigned to unique id device
    - C
        - check digit
        - not tramistted over air

![](https://i.imgur.com/TpDbzgs.png)


### International Mobile Equipment Identity (IMEI)
- unique 15 digit code to identify indiv GSM mobile to mobile network
- displayed on phones dy dialing code `*#06#`

![](https://i.imgur.com/YcYttBd.png)
![](https://i.imgur.com/YASPtMQ.png)


#### IMEI Checksum Verification
- 3 steps
    - starting from right, double every other digit
    - sum digits
        - note that 14 is 1 + 4 not +14
        - check if sum is divisible by 10

![](https://i.imgur.com/YMOsc4B.png)

![](https://i.imgur.com/FeWVvfn.png)


### International Mobile Subscriber Identity (IMSI)
- global unique identifier
- 56 bit
    - unique in every network
- allowed for auth of device to network
- 3 parts
    - MCC
        - mobile country code
        - 3 digits
        - all MCC is assigned by ITU internation telecomm union in recommendation E.212
            - internaitonal identification plan for public networks
    - MNC
        - mobile network code
        - 2 digits
    - MSIN
        - mobile station identification num
        - 10 digits

![](https://i.imgur.com/ja3PXES.png)
![](https://i.imgur.com/S1sUv1N.png)




###### tags: `DFI` `DISM` `School` `Notes`