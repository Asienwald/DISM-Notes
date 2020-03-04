---
title: 'ACG Revision'
disqus: hackmd
---

ACG Revision
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

Overview
---
- 10 mcq
- 4 open ended qns


01 Classical Ciphers
---
- slide 15, 16, 20-23, 25-30

### Substitution VS Transposition Ciphers
- sub - letters replaced by other letters or characters
- trans - hide msg by rearranging the letter order without altering letters used
    - can be recognised since have same freq distribution as orig text

### One-time pad
- unbreakable as
    - ciphertext & plaintext has no r/s
    - for any ciphertext & plaintext there's a key mapping
- difficulties in generation & safe distro since key used once only
    - hence not widely used today
- preconditions
    - key as long as plaintext
    - key truly random
    - key used once

### Playfair Cipher
- 5x5 key matrix

![](https://i.imgur.com/ueZOQY8.png)

#### En/Decryption
![](https://i.imgur.com/loRArNW.png)

#### Security
- now 26x26 = 676 digraphs
    - need to analyse freq table of 676 entries VS 26 for monoalphabetic encryption
        - monoalphabetic - map ea letter to letter
    - hence need more ciphertext to analyse
- can be broken since still has much of plaintext structure


### Vigenere Cipher
![](https://i.imgur.com/lXWtLhd.png)
![](https://i.imgur.com/80mon45.png)

#### Security
![](https://i.imgur.com/2gUGiml.png)


### Rail Fence Cipher
![](https://i.imgur.com/tFc37wa.png)
- diagonal


### Row Transposition Cipher
![](https://i.imgur.com/sNSDHDG.png)



02 DES
---
- slide 7, 8
- tutorial qns
- encrypt 64bit data with 56bit key


### Feistel Scheme
- no need details
- construction of scheme

#### Construction
![](https://i.imgur.com/ThIA0AI.png)
![](https://i.imgur.com/ZmS9HXA.png)

#### Design Elements
![](https://i.imgur.com/3L2yVis.png)



03 AES
---
- slide 6, 8, 10
- rijndael


### Requirements
![](https://i.imgur.com/8qoFyhx.png)
![](https://i.imgur.com/w3YlK9r.png)


### How it Works
- key expanded and separate keys for each blk derived from orig key
![](https://i.imgur.com/n7ZpwJv.png)

#### Byte Substitution
- simple substitution of ea byte
    - substitution table of 16x16 bytes
    - all permutation of 8 bit values
- ea byte (of state) used as index of S-box, replaced by content from S-box
    - by row - left 4 bits
    - by column - right 4 bits
- in decryption, inverse S-box used
- Rijndael S-box constructed using defined transformation of values in Galois Field (2^8)

![](https://i.imgur.com/b9sN8xf.png)

#### Shift Rows
- since state processed by cols, this steps permutes bytes between the cols
- circular byte shift in ea row
    - ![](https://i.imgur.com/0vs6zi9.png)
- decrypt inverts using shifts to right

![](https://i.imgur.com/rNxeiV9.png)

#### Mix Columns
- ea col processed separately (S > S')
- mixcol func multiplies ea col (state) with 4x4 byte matrix

![](https://i.imgur.com/NY7z01e.png)

- ea byte replaced by value dependent on all 4 bytes in col
    - ![](https://i.imgur.com/z6u6mie.png)

![](https://i.imgur.com/t4YbAk6.png)

- improved efficiency using Galois Field GF(2^8)
- multiplication with matrix
    - needs SHIFT & XOR operations only (vs matrix multiplication)
- decryption needs use of inverse matrix

#### Add Round Key
- XOR state with 128bits of round key
- processed by col
    - effectively a series of byte operations
- decryption is identical
    - with reversed keys, will reverse effect of XOR during encryption
    - designed to be simple af

![](https://i.imgur.com/gMgnCKC.png)

![](https://i.imgur.com/aJ3AjFP.png)

- round keys operates on ea byte of state independently

### S-Box
- how to use




07 Digital Signature
---
- slide 1-6, 9-11
- msg auth through hash, MAC or encryption
    - does not address issues of lack of trust


### Definition
- Digital signature - an auth mechanism that enables the creator of a msg to attach a code that acts as a signature
- the signature is formed by taking the hash of the msg & encrypting it with the creator's private key
- the signature guarantees the source & integrity of the msg

### Objectives
- signature provides
    - auth of msg content
    - 3rd parties can verify (not just receiver)
        - author, date & time
    - non repudiation

### Requirements
- must be bit pattern that depend on msg signed
- must use info unique to sender
    - prevent forgery & denial
- easy to produce
- easy to recognise & verify
- computationally infeasible to forge
- practical to save digital sign in storage

#### Application
- sign docus, files & emails
    - Eg. PDF, Word, PGP email
- sign server's cert
- provide as online signing service 
    - Eg. Docusign

### Direct vs Arbitrated
#### Direct
- involve only sender & receiver
    - assumed
        - sender & receiver both have own key pairs
        - both have each other's pub keys
- sign 1st then encrypt msg & sign
    - sign made by sender's private key
        - sign entire msg
        - sign hash only - for efficiency of scheme
- encrypt using receiver's pub key
- validity based on sender's priv key
    - sender can deny msg 
        - priv key stolen
    - timestamp on msg not useful
        - msg backdated

#### Arbitrated
- invites 3rd party in process called __trusted arbiter__
- use
    - arbiter receive signed msg from sender
    - validate content & origin from subj, msg & sign
    - dated msg & indicate that msg verified
    - send to recipients
- note
    - arbiter may/may not see msg
    - suitable lvl of trust needed
    - implement with priv/pub key encryption
        - need
            - complete trust from sender & receiver that arbiter will time-stamp & forward doc & also not alter the data
            - prevent sender from disowning msg

08 RSA
---
- what does it ensure
- solve 2 issues
    - key distro - enable secure comms w/o needing to trust key distro centre with key
    - digital signs - enable verification of msg from claimed sender
- use 2 keys
    - pub key - known to anybody
        - used to encrypt & verify signs
    - priv key - known to recipient only
        - used to decrypt & create signs
- asymmetric - those who encrypt/verify signs cannot decrypt/create signs

### Formula
#### Generating the Keys
![](https://i.imgur.com/o7VFs3d.png)

#### En/Decryption
![](https://i.imgur.com/34XKROw.png)


### HBL Calculation
![](https://i.imgur.com/iDtO5yj.png)
![](https://i.imgur.com/0iFQvdX.png)

- choose relatively prime - no other common factor other than 1
    - she chose 7 - smol so easier to calculate

![](https://i.imgur.com/FFQdAfp.png)
![](https://i.imgur.com/VphZnVU.png)
![](https://i.imgur.com/Ig2i3Kw.jpg)

- we want to find y (the num in front of e) which is d
    - if y is negative, need to subtract from totient (weird n thing)
    - if +ve, just take the num


09 Key Distribution
---
- slide 14


### Diffie-Hellman Key Exchange
- 2 qns on calculations & xxx
- formula

![](https://i.imgur.com/VckVHaF.png)



10 PGP
---
- slide 18-22
- application qns (10 marks)

### Digital Signature
- 1st step in PGP
- process
    - sender creates msg
    - PGP uses SHA-1 to generate 160bit hash code of msg
    - sender specifies priv key used for the op & provides passphrase, enabling PGP to decrypt sender's priv key
    - PGP encrypts hash code with RSA using sender's priv key & result prepended to msg
    - receiver uses RSA with sender's pub key to decrypt & recover hash code
    - receiver generates new hash code
        - if 2 match, msg accepted as authentic
- combi of SHA-1 & RSA provides an effective scheme
- strength of RSA ensures not only possessor of matching priv key can generate signature

### Process
- confidentiality in PGP achieved by encrypting msgs transmitted/stored locally
- conventional encryption algo CAST-128 may be used
    - other algos (Eg. IDEA/3DES) can be used
    - 64bit cipher feedback (CFB) used
- must address key distribution prob
    - ea conventional key only used once in PGP
    - new key generated as random 128bit num for ea msg
        - AKA one-time key or session key
    - because key only used once, its bound to the msg & transmitted with it
    - to protect key, its encrypted with receiver's pub key
- steps to encrypt msg
    - sender generates msg & random 128bit num used as session key for the msg only
    - msg encrypted, using CAST-128 etc. with session key
    - session key encrypted with RSA using recipient's pub key
        - prepended to msg
    - receiver uses RSA with its priv key to decrypt & recover session key
    - session key used to decrypt msg

#### Encryption Process
![](https://i.imgur.com/SXPNhEn.png)

11 SET
---
- slide 5, 6
    - remaining slides for understanding

### Steps
![](https://i.imgur.com/9PlpJYK.png)

### Components
![](https://i.imgur.com/bfKcFcC.png)


### Dual Signature
- purpose to link 2 msgs intended for 2 diff recipients by same sender
    - neither pt need know details of other but must know they're linked
    - dual msg for OI for merchant and PI for bank

![](https://i.imgur.com/AUewbf3.png)
![](https://i.imgur.com/Frob3Ry.png)




###### tags: `ACG SEM 2` `DISM SEM 2` `School` `Notes`