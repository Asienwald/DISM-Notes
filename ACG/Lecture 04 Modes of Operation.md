
Lecture 04 Modes of Operation
===



## Table of Contents

- [Lecture 04 Modes of Operation](#lecture-04-modes-of-operation)
  * [The Problem](#the-problem)
    + [Modes of Operation](#modes-of-operation)
    + [Message Padding](#message-padding)
  * [Block Cipher - Modes of Operation](#block-cipher---modes-of-operation)
    + [Electronic Code Book (ECB)](#electronic-code-book--ecb-)
      - [Limitations](#limitations)
    + [Cipher Block Chaining (CBC)](#cipher-block-chaining--cbc-)
      - [Features](#features)
  * [Stream Ciphers](#stream-ciphers)
    + [Structure](#structure)
    + [Properties](#properties)
    + [Cipher Feedback (CFB) Mode](#cipher-feedback--cfb--mode)
      - [Advantages & Limitations](#advantages---limitations)
    + [Output Feedback (OFB)](#output-feedback--ofb-)
      - [Advantages & Limitations](#advantages---limitations-1)
    + [OFB vs CFB](#ofb-vs-cfb)
    + [Counter (CTR)](#counter--ctr-)
      - [Advantages & Limitations](#advantages---limitations-2)
  * [Summary](#summary)


The Problem
---
- ciphers are deterministic
    - same msg + same key = same ciphertext

### Modes of Operation
- block ciphers - encrypt fixed size block of data
    - DES encrypts 64bit blks with 56bit key
    - AES encrypts 128biit blks with 128/192/256bit key
- modes of op
    - used to handle arbitrary amts of data to improve security
    - describes how repeatedly aplying cipher's single-blk op securely to transform amts of data larger than a block
    - 5 modes defined for AES & DES
- applicable for block & stream modes

### Message Padding
- 1 issue with blk cipher is how to handle last blk
    - blk size - fixed
    - msg size (input) - not fixed
- possible implementation
    - pad with extra bits at last blk
        - pad with known non-data value
            - Eg. nulls
        - pad with bits + count of pad size
            - Eg. 3 data bytes then 5 bytes pad + count
            - Eg. b1 b2 b3 0 0 0 0 5
    - overheads
        - need to recognise padding at receiving end
        - must know count of padding


Block Cipher - Modes of Operation
---
### Electronic Code Book (ECB)
- simplest mode of op
- msg split into independent blks
- ea blk encrypted independently with same key
    - ea blk sub with another value (like codebook, hence name ECB)
    - ![](https://i.imgur.com/3tPO3H0.png)
- used in secure transmission of single blk f info needed to be sent
    - Eg. session key encrypted using master key

![](https://i.imgur.com/9xfYJk4.png)

#### Limitations
- deterministic - not appropriate of any quantity of data
    - data block 1...n use same key, encrypted twice will get same ciphertext with same plain text
    - when msgs known to have subtle changes only - can be used for analysis
- msg repetitions show in ciphertext
    - obvioous in certain types of data (Eg. graphics)
    - weakness due to encrypted msg blks being independent
- limitations - for sending few blks of data

### Cipher Block Chaining (CBC)
- msg split into blks
- cipher blks linked tgt
    - ea cipher blks chained with current plaintext blk (hence called cipher blk chaining)
    - initialisation vector (IV) used to start process
        - IV - most modes need __unique binary sequence__ AKA IV for ea encryption operation
            - IV usually random or non-repeating
        - IV ensures diff ciphertext blks will be generated even if same plaintext blks appear multiple times in msg
    - ![](https://i.imgur.com/ybkWQib.png)
- used in bulk data encryption, auth

![](https://i.imgur.com/zLpzE3X.png)

#### Features
- ciphertext blk depends on all blks before it (not just key)
    - any change to blk affects all following ciphertext blks
    - chaining provides avalanche effect
- common IV between sender & receiver
    - IV dont need to be secret as its purpose is to ensure same plaintext encrypt to diff ciphertexts
    - IV need to be random so unlikely for IV to coincide with 1st plaintext blk by accident
    - IV need to be random to avoid atkers to base on known IV value to check/verify their guesses (brute force)
    - IV can be sent encrypted as 1st blk (effectively ECB mode) before rest of msg



Stream Ciphers
---
- process msg bit by bit as stream
    - use pseeudo random keystream
        - deterministic yet will pass randomness tests
    - combined (XOR) with plaintext bit by bit
- randomness of stream key completely destroys statistically properties in msg
    - ![](https://i.imgur.com/GjjxfIe.png)
- nvr reuse stream key else can recover msgs
- common stream ciphers
    - RC4
    - Salsa20

### Structure
![](https://i.imgur.com/6FW43z1.png)

### Properties
- design considerations
    - no repetitions over long period
    - statistically random
    - depends on large enough key (avoid brute force)
- as secure as blk cipher (with same key) if properly designed
- simpler (use less code)
- faster



### Cipher Feedback (CFB) Mode
- msg stream in bits added to output of blk cipher
    - ea ciphertext blk get feedback in encryption process to encrypt next plaintext blk
- allows num of bit (1, 8, 64 or 128 etc) to be feedbacked
    - denoted CFB-1, CFB-8, CFB-64, CFB-128 etc.
- most officient when all bits in blk (64 or 128) used
    - ![](https://i.imgur.com/Q6QThpj.png)
- used in stream data encryption, auth

![](https://i.imgur.com/vBwtbaW.png)

#### Advantages & Limitations
- most appropriate when data arrives in bits/bytes (stream mode)
- limitations
    - will stall during blk encryption after every n-bits if cant keep up with input data
        - blk cipher used in encryption mode at both ends
    - errors propagate for several blks
        - if network transmitting data is noisy

### Output Feedback (OFB)
- use unique IV to generate sequence of output blks that are XOR with plaintext
- output of cipher added to msg stream
- output then feedback to next cycle independent of msg
- can be computed in advance
    - ![](https://i.imgur.com/1Dtst2L.png)
- used in stream encryption on noisy channels

![](https://i.imgur.com/4cbuo1G.png)

#### Advantages & Limitations
- bit errors dont propagate
    - single bit error in cipher text C1 only affect 1 bit in plaintext P1
    - easy for recovery
- nvr reuse same key + IV
    - if reuse, portion of output stream can be recovered
- based on research, more optimum to use __full block feedback__ (ie OFB-64 or OFB-128)

### OFB vs CFB
![](https://i.imgur.com/fA2ojL4.png)
- OFB carried before plaintext added, CFB after plaintext added??

### Counter (CTR)
- similar to OFB but encrypt counter value instead of  feedback value
- "new" mode
- need diff key/diff counter value for every plaintext blk
    - nvr reused
    - ![](https://i.imgur.com/bouPij6.png)
- used in high speed network like ATM (asynchronous transfer mode) encryptions

![](https://i.imgur.com/bHvh4ix.png)

#### Advantages & Limitations
- efficiency
    - can do parallel encryptions
    - blk cipher ops can preprocess in advance
    - good for bursty high speed links
- provable security
- breakable if reuse key/counter values
    - similar to OFB


Summary
---
![](https://i.imgur.com/CCsBxsd.png)
![](https://i.imgur.com/WUhuLhN.png)



###### tags: `ACG` `DISM` `School` `Notes`