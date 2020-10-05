

Lecture 05 Cryptographic Hash
===



## Table of Contents

- [Lecture 05 Cryptographic Hash](#lecture-05-cryptographic-hash)
  * [Security != Encryption](#security----encryption)
    + [Possible Attacks](#possible-attacks)
    + [Requirements of Message Security](#requirements-of-message-security)
    + [Encryption](#encryption)
    + [Tools for Msg Auth](#tools-for-msg-auth)
  * [Hash](#hash)
    + [Hash Algo Requirements](#hash-algo-requirements)
    + [Merkle-Damgard Construction](#merkle-damgard-construction)
    + [Known Hash Algos](#known-hash-algos)
    + [Simple Hash Functions](#simple-hash-functions)
    + [Applications of Hash Algos](#applications-of-hash-algos)
      - [Requirements](#requirements)
  * [Secure Hash Algo (SHA)](#secure-hash-algo--sha-)
    + [Revised SHA (SHA-2)](#revised-sha--sha-2-)
    + [SHA-512](#sha-512)
      - [Processing](#processing)
      - [Round Function](#round-function)
      - [Message Expansion](#message-expansion)
    + [Comparison of SHA Functions](#comparison-of-sha-functions)
  * [Attacks](#attacks)
    + [Problem Statement](#problem-statement)
      - [Birthday Attacks](#birthday-attacks)
      - [Birthday Paradox](#birthday-paradox)

Security != Encryption
---
### Possible Attacks
- msg confidentiality
    - disclosure
    - traffic analysis
- msg auth
    - masquerade
    - content modification
    - sequence modification
    - timing modification
    - source repudiation
    - destination repudiation

### Requirements of Message Security
- msg confidentiality
    - adversary cannot understand/decrypt msg
- msg auth concerned with
    - integrity of msg
    - validating identity of originator
        - ascertain sender
    - non-repudiation of origin (dispute resolution)
        - recipient passes msg + proof to 3rd pt
        - 3rd pt confident that msg originated from sender

### Encryption
- strong encryption provides confidentiality
- provides some auth
    - using symmetric key encryption
        - receiver assum sender created msg
            - since only sender & receiver know key
        - receiver assume msg content not altered
            - encrypted + alter msg = corrupted msg
            - if msg has suitable structure like redundancy/checksum

- using public key encryption
    - encryption provides no info of sender
    - in public key system, sender can sign msg using private key then encrypt with recipient's public key
    - provide both secrecy & auth
    - note - 2 pairs of public-private keys used

![](https://i.imgur.com/q2mkZRf.png)

### Tools for Msg Auth
- hash
- msg auth code (MAC)
- digital signature

Hash
---
![](https://i.imgur.com/vUhplvU.png)

### Hash Algo Requirements
![](https://i.imgur.com/dYlu98j.png)


### Merkle-Damgard Construction
- like chained blk cipher
- append padding & length to msg
- break input into equal-sized blks
    - 1024 or 512 bits
- apply compression func f iteratively
    - saves state from 1 iter to next
    - hash as strong as compression func

![](https://i.imgur.com/2K2QSh6.png)

- merkle-damgard construction for handling big var input msg is proven collision resistant __if hash func f is collision resistant__

![](https://i.imgur.com/THABckR.png)
- hashing algo (Eg. MD5, SHA1, SHA2) ue diff hash func but based on same Merkle-Damgard construction concept

### Known Hash Algos
![](https://i.imgur.com/tNJkWjK.png)

### Simple Hash Functions
- based on XOR of msg blks + rotate bits
- insecure > predictable effect on digest by manipulating msg > non collision resistant
- if msg not encrypted, easy to modify msg & append  blk that will set hash code as needed

### Applications of Hash Algos
- public key algos
    - password logins
    - encryption key management
    - digital signatures
- integrity checking
    - virus & malware scanning
- auth
    - secure web connections
    - PGP, SSL, SSH, S/MIME

#### Requirements
![](https://i.imgur.com/c13DDHg.png)



Secure Hash Algo (SHA)
---
- originally designed by NIST & NSA in 1993
    - revised in 1995 as SHA-1
- US standard for use with DSA signature scheme
    - standard is FIPS 180-1 1995, also Internet RFC3174
    - note
        - algo = SHA, standard = SHS
- based on design of hash func MD4 with key diff
    - produces 160bit hash values
    - in 2005 SHA-1 raised concerns on use in future appps

### Revised SHA (SHA-2)
- NIST issued revision FIPS 180-2 in 2002
    - FIPS PUB 180-4 in 2012
- total 6 vers of SHA2
    - SHA-224, SHA-256, SHA-384, SHA-512
    - SHA-512/224, SHA-512/256 
        - added in FIPS PUB 180-4
    - with digests (hash vals) that are 224, 384 or 512 bits
- designed for compatibility + increased security
    - structure & detail similar to SHA-1
    - analysis shld be similar
    - higher security

### SHA-512
![](https://i.imgur.com/mt5ouTY.png)

#### Processing
1. append padding bits
2. append length of msg
3. initialise hash buffers (words)
4. process msg in 1024bit blks (the f func in the overview)
5. output final state val as resulting hash

![](https://i.imgur.com/81cztjk.png)

#### Round Function
![](https://i.imgur.com/B1AdWH0.png)

#### Message Expansion
- 1024bit msg fed multiple times into f func as W
- ![](https://i.imgur.com/TimEwsQ.png)

![](https://i.imgur.com/VzxejFn.png)

- msg size limitations
    - corr to num of reserved bitsa in pad length blk, diff hash funcs have diff max msg size limitations

![](https://i.imgur.com/pojGpeF.png)

### Comparison of SHA Functions
![](https://i.imgur.com/bfZIpj6.png)


Attacks
---
- preimage resistance
    - easy to generate code given a msg but virtually impossible to generate msg (or part of it) given a code
    - given y, difficult to find an x such that `h(x) = y`
    - hash is 1 way
- 2nd preimage resistance
    - computationally infeasible to find pair of msgs with same hash val
    - given x, difficult to find 2nd preimage `x' != x` such that `h(x) = h(x')`
    - no collisions

![](https://i.imgur.com/aXrZr22.png)
- birthday atk
    - general purpose atk on hash funcs
    - higher likelihood of collisions found between random atk attempts & fixed degree of permutations

### Problem Statement
- what's probability that any 2 students in class have same bday when there's 23 students?
    - 50
- wtf is this

#### Birthday Attacks
![](https://i.imgur.com/nStWx4E.png)

#### Birthday Paradox
![](https://i.imgur.com/wu73bhp.png)










###### tags: `ACG` `DISM` `School` `Notes`