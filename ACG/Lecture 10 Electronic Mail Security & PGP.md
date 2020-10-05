---
title: 'Lecture 10 Electronic Mail Security & PGP'
disqus: hackmd
---

:::info
ST2504 Applied Crypto
:::

Lecture 10 Electronic Mail Security & PGP
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

Electronic Mail Security
---
- objectives
    - privacy/encryption
    - msg integrity
    - auth
    - non-repudiation


Pretty Good Privacy (PGP)
---
- program to secure email to ensure __privacy__ & __authenticity__
- capable of resisting even most sophisticated forms of analysis
- can be used to apply digital signature & en/decrypt msg
- written by Phil R Zimmermann


### Reason for Popularity
- PGP/OpenPGP is available free worldwide
    - OpenPGP is branch of PGP
        - use no algo with licensing difficulties
- available on many platforms
    - Windows/unix/macintosh
- based on algos that survived extensive public review & considered extremely secure
- has wide range of applicability
- not developed by/controlled by any gov or standards org


### Features
- combi of algo in set of utility software for
    - encryption os msgs, digests & keys
    - msg digest used for digital signature
    - key generation for priv session key
    - key generation for users' pub/priv key pairs
    - key management & certification cyclic redundancy check (CRC)

### Public Keys
- ea user has priv key & copy of pub key of ea potential correspondent
- PGP maintains list of pub keys that user obtained by any means
    - Eg. through email
- ea item on pub key includes many parts
    - pub key itself
    - user ID of owner of pub key
    - key ID
        - unique identifier for key
    - other info about trustworthiness of key & owner


### Private Keys
- ea PGP must have priv key
- priv key handled with more care
- stored on user's priv key ring
    - recommended to store on secure USB disk for security reason
- to access key, passphrase needed
- PGP uses passphrase to generate symmetric key
    - Eg. 128bit IDEA (International Data Encryption Algo)
- encrypts priv key using chosen algo & passphrase-based key
- for ea priv key, need these info
    - priv key, encrypted using passphrase-based key
    - owner's used ID
    - copy of matching pub key


Operation of PGP
---
- op of PGP for sending/receiving msgs consist of 5 services

![](https://i.imgur.com/Kx3ax6G.png)
![](https://i.imgur.com/Vek3Uab.png)

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

#### Sample
![](https://i.imgur.com/JEeaBBb.png)


### Message Encryption
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

#### Sample
- sample of msg encryption using PGP software

![](https://i.imgur.com/txQAy7m.png)

#### Digital Signature & Message Encryption
- can be used tgt
    - provide auth & confidentiality
- digital sign generated 1st for plaintext msg & prepended to msg
- plaintext msg + sign encrypted using CAST-128
- session key encrypted using RSA


### Compression
- by default PGP compresses msg after applying signature but before encryption
- compression saves transmission time & disk space
- also strengthens cryptographic security
    - reduces redeundacy hence enhancing resistance to crptanalysis
- takes extra time to compress plaintext but from security pt of view its worth it
- PGP uses commonly used compression technique called __zip__
    - is freeware package
- operation of zip
    - looks for repeating string of chars in input & replaces with compact codes
    - dest system performs same func & replaces code with orig text
    - more redundancy, more effective the zip algo
    - typical txt files compress abt 50% of orig length

### Radix-64 Conversion
- when PGP used, at least part of blk transmitted is encrypted
- signature services - msg digest encrypted with sender's priv key
- confidentiality - both msg & signature encrypted with one-time symmetric key
- hence, part of all resulting blks consists of stream of arbitrary 8bit bytes
- many email systems only allow msgs of ASCII text
    - 8bit raw binary data not supported/readable
- PGP supports ASCII radix-64 format for ciphertext msgs
    - special format represents binary data by using only printable ASCII chars
    - useful for transmitting encrypted data as norm email text
    - acts as transport armor - protect against corruption on internet
- PGP also depends on CRC (cyclic redundancy check) to detect transmission errors
- Radix-64 format converts plaintext by expanding blk of 24bits into 4 printable ASCII chars (32bits)
    - file grows abt 33%, consdering that file was prob compressed more than that before encryption

### Segmentation & Reassembly
- email facilities often restricted to max msg length
    - long msg must be broken into smaller segments & mailed separately
- PGP auto subdivides msg that's too large into segments small enough to send via email
    - done after all other processing including raidx-64
- session key component & signature component appear only once at beginning of 1st segment
    - at receiving end, PGP must strip off all email headers & reassemble entire orig blk
    - this is before performing any steps to verify/decrypt msg


Summary PGP
---
### Order of Operations
![](https://i.imgur.com/OpLPRrK.png)

### Summary
![](https://i.imgur.com/cx1zNoQ.png)




###### tags: `ACG` `DISM` `School` `Notes`