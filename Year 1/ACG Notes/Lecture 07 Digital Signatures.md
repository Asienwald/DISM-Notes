---
title: 'Lecture 07 Digital Signatures'
disqus: hackmd
---

:::info
ST2504 Applied Cryptography
:::

Lecture 07 Digital Signatures
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

Digital Signature
---
- msg auth
    - through hash, MAC or encryption
    - doesn't address issues of lack of trust
- handwritten signature
    - useless on internet
    - bind signatory to msg
- signature provides
    - auth of msg content
    - 3rd parties not just receiver can verify
        - author, date & time of msg
    - non-repudiation

### Requirements
- must be bit pattern that depend on msg signed
- must use info unique to sender
    - prevent forgery & denial
- easy to produce
- easy to recognise & verify
- shld be computationally infeasible to forge
    - create new msg with existing digital signature
    - create fraudulent digital sign for given msg
- shld be practical to save digital sign in storage

### Application
- sign docs, files, emails
    - Eg. PDF, Word PGP email
- sign server's cert
- provide as online signing service
    - Eg. DocuSign

### How it Works
- digital sign - auth mechanism that enable creator of msg to attach code that acts as signature
- formed by taking hash of msg & encrypting msg with creator's private key
- guarantees src & integrity of msg

![](https://i.imgur.com/a9I7HgB.png)


Types of Digital Signatures
---
### Direct Digital Signatures
- involve only sender & receiver
    - assumed
        - sender & receiver have own key pairs - private & public
        - receiver has sender's pub key
        - sender has receiver's pub key
- sign 1st then encrypt msg & signature
    - digital sign made by sender's private key either
        - sign/encrypt entire msg
        - sign/encrypt hash only
            - for efficiency of scheme
- encrypt using receiver's pub key
    - validity of signature depends on sender's private key
        - sender may deny sending msg
            - private key stolen
        - timestamp on msg not useful
            - msg might be back dated

![](https://i.imgur.com/33eo7w9.png)

### Arbitrated Digital Signatures
- implementing arbitrated digital signature invites 3rd pt into process called __trusted arbiter__
- use of arbiter (trusted 3rd pt)
    - arbiter receive signed msgs from sender
    - validate content & origin from subj, msg & signature
    - arbiter dated msg & indicated that msg verified
    - sent to recipients
- arbiter may/may not see msg
- suitable lvl of trust in arbiter needed
- implemented with priv & pub key encryption
    - need
        - complete trust from both sender & receiver that arbiter wont only time-stamp & forward doc as instructed but also not alter data
        - prevent sender from disowning msg


Digital Signature Schemes
---
### Mechanism of Signature Schemes
- 3 algos
    - key gen algo
        - randomly select key pair
    - signature algo
        - msg + priv key = signature
    - signature verification algo
        - pub key + signature = true/false (validated/not validated)

### Digital Signature Standard (DSS)
- US gov pproved signature scheme
    - designed by NIST & NSA in early 90s
    - published as FIPS-186 in 1991
        - FIPS 186-2 (2000) inclludes alt RSA & elliptic curve signature variants
    - revised in 1993, 1996 & 2000
- uses SHA hash algo
- DSS is standard, DSA is algo

### Digital Signature Algorithm (DSA)
- based on asymmetric key algo
- digital signature scheme
    - 320bit signature (length of sign)
    - 512-1024 bit security key
- smaller & faster than RSA
- security > discrete logarithm (computationally hard prob)

![](https://i.imgur.com/7RfLVLr.png)


#### Key Generation
- by signing person

![](https://i.imgur.com/a6pK4Gf.png)

![](https://i.imgur.com/4ctIoHF.png)

#### Signing
![](https://i.imgur.com/fCUaOxQ.png)

#### Verification
![](https://i.imgur.com/BfJ64Kj.png)

![](https://i.imgur.com/cOVrW9w.png)


Summary
---
![](https://i.imgur.com/yk8db2y.png)





###### tags: `ACG SEM 2` `DISM SEM 2` `School` `Notes`