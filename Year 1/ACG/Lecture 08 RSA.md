---
title: 'Lecture 08 RSA'
disqus: hackmd
---

:::info
ST2504 Applied Cryptography
:::

Lecture 08 RSA
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



Private-Key Crypto
---
- traditional private/secret/single key crypto uses 1 key
- key disclosed
    - confidentiality of comms compromised
    - repudiation of sender compromised
        - receiver may forge msg & claim its sent by sender

Public-Key Crypto
---
- uses 2 keys
    - public key
        - known by anybody
        - used to encrypt msgs
        - verify signatures
    - private key
        - known only to recipient
        - used to decrypt msgs
        - sign/create signatures
- asymmetric
    - both parties not using same key
    - those who encrypt msg/verify signatures cannot decrypt msgs/create signatures
- complements private key crypto
- uses num theoretic concepts
- why pub-key crypto?
    - solves 2 key issues
        - key distribution
            - enable secure comms w/o having to trust KFC with key
        - digital signatures
            - enable verification of msg from claimed sender
    - invented publicly by Whitfield Diffie & Martin Hellman at Stanford Uni in 1976
        - known earlier in classified community

![](https://i.imgur.com/msqZJFN.png)

### Characteristics
- pub key algo need
    - easy to en/decrypt msgs when relevant key known
        - using exponentiation/multiplication
    - hard tof ind decryption key when only algo & encryption key known
        - using logs, factoring
    - 2 related key can be switched for encryption/decryption
        - for some algos

### Cryptosystems
![](https://i.imgur.com/w7ARjkQ.png)

### Applications
- used for
    - en/decryption
        - provide secrecy
    - digital signatures
        - provide auth
    - key exchange of session keys
- not all algos suitable for 3 apps above
    - Eg. Diffie-Hellman used for key exchange, RSA for en/decryption, DSA for digital signature

### Security of Public Key Schemes
- brute force/exhaustive search atk theoretically possible
- hard enough to be impractical to break by using large keys
    - RSA claims
        - ![](https://i.imgur.com/q1jWisw.png)
- pub key crypto is slow compared to private key crypto
    - harder to brute


RSA
---
- invented by Rivest, Shamir & Adleman in 1977
- best known & most widely used pub key scheme
- en/decryption based on exponentiation (easy)
- security is at cost of factoring large numbers (hard)

### RSA Key Setup
- ea user generates pub/priv key pair by

![](https://i.imgur.com/1CrJWvs.png)

#### Example
![](https://i.imgur.com/0bmjoa5.png)


### RSA Encryption/Decryption
- to encrypt msg M

![](https://i.imgur.com/y97NwlD.png)

- to decrypt ciphertext C

![](https://i.imgur.com/h3x2UjJ.png)

- note - msg M must be smaller than modulus n
        - break M into blks if needed

#### En/decryption Example
![](https://i.imgur.com/wW6isf2.png)


### RSA Attacks
#### Factoring
- brute-force atk

![](https://i.imgur.com/0Plz9PV.png)

- mathematical atk (on factoring)
    - slow improvement over years
        - as of 9th Dec best is 232 decimal digits - 768bits
    - improvement in algos & Quantum Comps could potentially break RSA
    - currently recommended n >= 2048bits

#### Misuse
- use common modulus N
    - reusing same N with diff d & e is not safe to generate pub/priv keys
- using small pub/priv exponent
    - d & e are modular multiplicative inverse
        - select 1, compute other
    - short public exponent = faster to encrypt
        - extremem tiny public exponent (Eg. e = 3) is unsafe
        - typically 65535 is commonly used (good enough)
    - long private exponent > protect data
        - harder to brute force


#### Chosen Ciphertext Attacks
- RSA is deterministic encryption algo
    - ciphertext same if msg unchanged
- chosen ciphertext atk - atker send ciphertext & gets plaintext back
    - ![](https://i.imgur.com/9K15aTj.png)
- solution - use random pad on plaintext
    - ![](https://i.imgur.com/CTA8vIR.png)
- [Recommended Vid](https://www.youtube.com/watch?v=aH4DENMN_O4)

#### Implementation
- timing atk
    - based on time by device (Eg. smartcard) to decryption/signing
    - solution - use delays
- power cryptanalysis
    - based on power needed by device during signature generation > discover secret key


### RSA Key Generation Considerations
- select 2 sufficiently large primes to generate modulus
    - N shld be >2046bits in length
- p & q shld be prime nums
- e & N shld be co-prime
    - two integers a and b are said to be  coprime if the only positive integer (factor) that divides both of them is 1
    - Eg. 18 & 35 are co-prime as 1 is their only common factor
- msg must be smaller than N
- use bigger (priv & pub) exponents when possible
    - fermat prime (2^(2n) + 1) commonly used as public exponents
        - faster
- use padding 
    - Eg. OAEP



###### tags: `ACG SEM 2` `DISM SEM 2` `School` `Notes`