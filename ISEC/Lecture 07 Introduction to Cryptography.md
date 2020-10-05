---
title: 'Lecture 07 Introduction to Cryptography'
disqus: hackmd
---

:::info
ST1004 Infocomm Security
:::

Lecture 07 Introduction to Cryptography
===

<style>
img{
/*     border: 2px solid red; */
    margin-left: auto;
    margin-right: auto;
    width: 80%;
    display: block;
}
</style>


## Table of Contents

[TOC]

Cryptography
---
- defining cryptography involves
    - what it is
    - what it can do
    - how it can be used as secrity tool to protect data

### What is Cryptography?
- cryptography
    - scrambling info so cannot read
    - transform info into secure form so unauth persons cannot access
- steganography
    - hides existence of data
    - img/audio/video file can contain hidden msgs embedded in file
    - achieved by dividing data & hiding in unused portions of file
    - may hide data in file header fields that describe file, between sections of __metadata__
        - metadata - data used to describe content or structure of actual data

![](https://i.imgur.com/rethauw.png)

#### Definitions
- encryption
    - changing orig txt into secret msg using crypto
- decryption
    - changing secret msg back to orig form
- plaintxt
    - unencrypted data to be encrypted/output of decryption
- ciphertext
    - scrambled & unreadable output of encryption
- cleartxt data
    - data stored/transmitted w/o encryption
- plaintxt input into __cryptographic algorithm__ (AKA cipher)
    - consist of procedures based on mathematical formula used to en/decrypt data
- key
    - mathematical value entered into algo to produce ciphertxt
    - reverse process uses key to decrypt msg
- substitution cipher
    - subs 1 char for another
    - 1 type of ROT13 whr entire alphabet rotated 13 steps
- XOR cipher
    - based on bin operation eXclusive OR that compares 2 bits

![](https://i.imgur.com/BRO9sXL.png)
![](https://i.imgur.com/afvvbiu.png)

- modern crypto algos rely upon underlying mathematical formulas
    - depend on quality of random nums (no identifiable pattern/sequence)
- software relies on __pseudorandom number generator (PRNG)__
    - algo for creating seq of nums whose properties approximate those of random num
- 2 factors that can thwart threat actors from discovering underlying key to crptographic algos
    - __diffusion__ - if single char of plaintext is changed then shld result in multiple chars of ciphertxt changing
    - __confusion__ - key dont relate in simple way to ciphertxt


### Cryptography & Security
- crypto can provide 5 basic protections
    - confidentiality
        - only auth parties can view
    - integrity
        - ensure info correct & unaltered
    - auth
        - ensure sender can be verified through crypto
    - non-repudiation
        - proves user performed an action
    - obfuscation
        - making sth obscure or unclear
        - security through obscurity
            - virtually any system can be made secure as long as outsiders unaware of it/how it works

![](https://i.imgur.com/DmZQQTP.png)

- crypto can provide protection to data as data resides in any of 3 states
    - data in-use
        - data actions performed by endpoint devices
    - data in-transit
        - actions that transmit the data across network
    - data at-rest
        - data stored on electronic media


### Cryptography Constraints
- num of small electronic devices (low-power devices) grown significantly
    - need to be protected from threat actors
- apps that need extremely fast response times also face crypto limitations
- __resource vs security constraint__
    - limitation providing strong crypto due to tug-of-war between avail res (time & energy) & security provided by crypto
- impt that thr be __high resiliency__ in crypto
    - ability to recover quickly from these res vs security constraints

![](https://i.imgur.com/kZthdl0.png)


Cryptographic Algorithms
---
- diff in crypto algos is amt of data processed at a time
    - __stream cipher__
        - take 1 char & replace with another
    - __blk cipher__
        - manipulate entire blk of plaintext at once
    - __sponge func__
        - take as input string of any length & return string of any requested variable length

- 3 categories
    - hash algos
    - symmetric crypto algos
    - asymmetric crypto algos

### Hash Algorithms
- __hashing__ - create unique digital fingerprint of set of data
    - this fingeprint called __digest__
        - AKA message digest/hash
        - represents content 
    - contents cannot be used to reveal orig dataset
        - primarily used for comparison purposes
    - hashing intended to be 1 way 
        - digest cannot be reversed to reveal orig data

- secure hashing algo characteristics
    - fixed size
        - short & long data sets have same size hash
    - unique
        - 2 diff datasets cannot produce same hash
    - original
        - dataset cannot be created to have predefined hash
    - secure
        - resulting hash cannot be reversed to determine orig plaintxt

- hashing also often used to verify that orig contents of item not changed

![](https://i.imgur.com/Yaq1AUZ.png)

#### Example of Hashing - ATMs
- bank customer have PIN of 93542
- num hashed & result stored on card's magnetic strip
- user insert card in ATM & enter PIN
- ATM hashes pin using same algo used to store PIN on card
- if 2 vals match, user can access ATM

#### Types of Hash Algorithms
- message digest 5 (MD5)
    - most well known of MD hash algos
    - msg length padded to 512 bits
    - weakness in compression func can lead to collisions
    - experts recommend use more secure algo
- secure hash algorithm (SHA)
    - more secure than MD
    - SHA2 considered secure
    - SHA3 announced as new standard in 2015
        - suitable for low-power devices
- race integrity primitives evaluation msg digest (RIPEMD)
    - pri design feature is 2 diff & independent parallel chains of computation
    - results combined at end of process
    - several vers of RIPEMD
        - RIPEMD-128, RIPEMD-256, RIPEMD-320
- hashed msg auth code (HMAC)
    - hash variation providing improved security
    - uses shared secret key possessed by sender & receiver
    - receiver uses key to decrypt hash


### Symmetric Cryptographic Algorithms
- symmetric crypto algos
    - use same single key to en/decrypt document
        - orig crypto algos are symmetric
        - AKA __private key cryptography__
            - key kept private between sender & receiver

![](https://i.imgur.com/XWzL8uS.png)


- common algos
    - data encryption standard
    - triple DES
    - advanced encryption standard
    - other algos

#### Algorithms
- data encryption standard (DES)
    - based on product designed in early 1970s
    - 56bit key
    - blk cipher
- triple DES (3DES)
    - designed to replace DES
    - 3 rounds of encryption
    - ciphertxt 1st round becomes input for 2nd iteration
    - most secure vers use diff keys for ea round

![](https://i.imgur.com/Rhur1Sk.png)

- advanced encryption standard (AES)
    - symmetric cipher approved by NIST in 2000 as replacement for DES
    - 3 steps on every blk (128bits) of plaintxt
    - designed to be secure well into future
- other algos
    - rivest cipher (RC)
        - family of cipher algos designed by ron rivest
    - blowfish
        - blk cipher operating on 64bit blks with key length from 32-448bits
        - no significant weaknesses identified
    - international data encryption algo (IDEA)
        - used in european nations
        - blk cipher processing 64bits with 128bit key with 8 rounds


### Asymmetric Cryptographic Algorithms
- weakness of symmetric algo
    - distributing & maintaining secure single key among multiple users distributed geographically
- asymmetric crypto algos
    - AKA __public key cryptography__
    - use 2 mathematically related keys
    - pub key avail to everyone
        - freely distributed
    - private key known only to indiv

![](https://i.imgur.com/ucWmhux.png)

- impt principles
    - key pairs
    - pub key
    - private key
    - both directions
        - key work in both dirs
- common asymmetric crypto algos
    - RSA
    - elliptic curve crypto
    - digital signature algo
    - those relating to key exchange

#### Asymmetric Algorithms
- RSA
    - published 1977
        - patented by MIT in 1983
    - most common asymmetric crypto algo
    - uses 2 large prime nums
- elliptic curve crypto (ECC)
    - users share 1 elliptic curve & 1 pt on curve
    - use less computing power than prime-based assymetric crypto
        - key sizes smaller
    - considered alt for prime-based asymmetric crypto for mobile & wireless devices

![](https://i.imgur.com/wI37bKu.png)

- digital signature algo (DSA)
    - digital signature - electronic verification
    - verifies sender
    - prevent sender from disowning msg
    - prove msg integrity

![](https://i.imgur.com/wEOgGwV.png)

![](https://i.imgur.com/YdI3ly4.png)

- key exchange
    - diff solutions for key exchange
        - diffie hellman (DH)
        - diffie hellman ephemeral (DHE)
        - elliptic curve diffie hellman (ECDH)
        - perfect forward secrecy


Cryptographic Attacks
---
- common crypto attacks
    - target algo weaknesses
    - exploit collisions

### Algorithm Attacks
- methods atkers focus on circumventing strong algos
    - known ciphertxt atks
    - downgrade atks
    - using deprecated algos
    - taking advantage of improperly implemented algos

#### Known Ciphertext Attack
- statistical tools used to discover patterns in ciphertext to reveal the plaintext or key

![](https://i.imgur.com/rb1pHNm.png)

#### Downgrade Attack
- threat actor forces system to abandon current higher security mode of operation & instead fall back to implementing older & less secure mode

#### Using Deprecated Algorithms
- use crypto algo that shldnt be used due to known vulns

#### Improper Implementation
- AKA misconfiged implementation
- many crypto algos have several config options
- unless careful consideration given to these options, crypto may be improperly implemented


### Collision Attacks
- __collision__ - when 2 files have same hash
- collision atk - attempt to find 2 input strings of hash func that produce same hash result
- birthday atk - based on __birthday paradox__
    - says that for there to be 50% chance that someone in given room shares your bday, 253 people need to be in the room


Using Cryptography
---
- cryptography shld be used to secure
    - data in transit
    - data at rest
    - data in use
- includes 
    - indiv files
    - databases
    - removable media
    - data on phones
- crypto applied through
    - software
    - hardware

### Software Encryption 
- file & file system crypto
    - encryption software used to en/decrypt files 1 by 1
- pretty good privacy (PGP)
    - widely used asymmetric crypto system
    - used for files & emails on Windows
    - __GNU privacy guard (GNuPG)__
        - open source product that runs on windows, unix & linux OS
    - openPGP is another open source alt based on PGP
- OS system encryption
    - microsoft windows encrypting file system (EFS)
        - crypto system for windows
        - uses NTFS file system
        - tightly integrated with file system
        - en/decryption transparent to user
- full disk encryption (FDE)
    - protect all data on hard drive
    - Eg. bitlocker drive encryption software included in microsoft windows
        - bitlocker encrypts entire system volume
            - including windows registry
        - prevents atkers from accessing data by booting from another OS or placing hard drive in another comp


### Hardware Encryption
- software encryptionn subject to atks to exploit its vulns
- crypto can be embedded in hardware
    - higher degree of security
    - applied to USB devices & standard hard drives
- hardware encryption options include
    - trusted platform module
    - hardware security model

#### USB Device Encryption
- encrypted hardware-based flash drive used
    - wont connect to comp until correct password provided
    - all data copied to drive auto encrypted
    - tamper-resistant external cases
    - admins can remotely control & track activity on devices
    - stolen devices remotely disabled

#### Self-Encrypting Drives (SEDs)
- self encrypting hard drives protect all files stored on them
- drive & host device perform auth process during initial power up
- if auth fails, drive can be configed to deny access or delete encryption keys so all data permenantly unreadable

#### Trusted Platform Module (TPM)
- chip on comp's motherboard that provides crypto services
- include true random num generator
- entirely done in hardware so cannot be subject to software atk
- prevents comp from booting if files/data altered
- prompt for passwd if hard drive moved to new comp

#### Hardware Security Module (HSM)
- secure crypto processor
- includes onboard key generator & key storage facility
- performs accelerated symmetric & asymmetric encryption
- can provide services to multiple devices over LAN

Chapter Summary
---
![](https://i.imgur.com/bISYsCJ.png)
![](https://i.imgur.com/IKMoGAM.png)




###### tags: `ISEC` `DISM` `School` `Notes`