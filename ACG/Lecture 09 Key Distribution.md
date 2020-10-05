

Lecture 09 Key Distribution
===


## Table of Contents

- [Lecture 09 Key Distribution](#lecture-09-key-distribution)
  * [Distribution of Public Keys](#distribution-of-public-keys)
    + [Public Announcement](#public-announcement)
    + [Publicly Available Directory](#publicly-available-directory)
    + [Public-key Authority](#public-key-authority)
    + [Public-key Certificate](#public-key-certificate)
      - [Certificate](#certificate)
    + [Key Exchange](#key-exchange)
  * [Diffie-Hellman Key Exchange](#diffie-hellman-key-exchange)
    + [DH Setup](#dh-setup)
      - [Example](#example)
    + [Key Exchange Protocols](#key-exchange-protocols)

Distribution of Public Keys
---
### Public Announcement
- users distribute pub keys to recipients/boradcast to community
    - append PGP keys to emails & send across network
    - post PGP keys on news grps/email list
    - various site that support PGP keys as part of user profile
        - Eg. facebook
    - convenient & works well for small scale distro
- weakness - forgery
    - anyone can create key claiming to be someone else & broadcast
    - adversary can masquerade as claimed user

### Publicly Available Directory
- dir must be trusted with properties
    - contains {name, public-key} entries
    - participants register securely with dir
    - participants can replace key anytime
    - dir periodically published
        - can publish entire/just changes of dir
    - dir can be accessed electronically
    - dir must be trusted
- greater security compared to public announce but still vulnerable to tampering/forgery
    - pretend to be authorised dir
    - change records in dir

### Public-key Authority
- improved security - tighten control over distro of keys from dir
- central authority maintains dynamic dir of pub keys of everyone
- requirements
    - authority secured
    - all users know pub key of dir/authority
        - only authority know corr private key
    - real-time access to dir/authority when keys needed
        - AKA always on server
- issues
    - authority can be bottleneck
    - records maintained can be tampered

![](https://i.imgur.com/IAIzCNo.png)
__E: Encryption/signing msg (if from authority)
N: Some random val that's hard to predict__

- A & B know their key pair
    - pub/priv keys & so is authority
- A & B published their pub key to authority
- authority verify all pub keys correct
- A & B know pub key of authority
- msg 3, 6 & 7 are for A & B to cfm they talking to right pt


### Public-key Certificate
- to overcome bottleneck, can use pub key certs
    - allow key exchange w/o real-time access to pub-key authority
    - binds identity to pub key
        - with other info like period of validity, rights of use etc.
- pub key signed by trusted Certificate Authority (CA) can be verified by anyone
    - pub key of CA is publicly available

![](https://i.imgur.com/5v1VPPY.png)
![](https://i.imgur.com/ukR4jkU.png)

- when A & B want to comm, only msg sent is (1) and (2)
- M1 & M4 happen in advance way before msg (1) and (2)
    - this why performance improved greatly
    - only (1) and (2) needed for A & B to exchange msg
    - no msg goes to authority during comm
- certs exchnage between A & B issued by CA
- CA not involved in comm
- certs received verified using CA's pub key

#### Certificate
![](https://i.imgur.com/bfEajlw.png)


### Key Exchange
- sharing secret keys securely with aid of pub key
    - pub key encryption
        - need long key to be effective
            - AKA hard to break
        - hence slow/CPU intensive
    - use secure way to exchange secret/session key
        - encrypt msg based on secret/session key


Diffie-Hellman Key Exchange
---
- 1st pub-key scheme proposed
    - by diffie & hellman 1976
    - note
        - Williamson (UK CESG) secretly proposed the concept in 1970
- DH not for data secrecy/auth
- DH key exchange is practical method for public exchange of secret key/shared value

![](https://i.imgur.com/4S3HUrw.png)

- DH features
    - establish common key known only to the 2
        - val of key depends on participants & their priv & pub key info
    - properties
        - cannot be used to exchange arbitrary msg
        - shld be
            - computationally easy - forward processing
                - exponentials modulo a prime/polynomial
            - computationally hard - reverse processing
                - discrete logarithms

### DH Setup
- all agree on global params
    - p is large prime int
    - g is primitive root modulo of p
- ea user generates his/her key
    - chooses secret key
        - ![](https://i.imgur.com/NCjx3C6.png)
- ea user makes pub key
    - alice's pub key
        - ![](https://i.imgur.com/d9nOOnI.png)
    - bob's pub key
        - ![](https://i.imgur.com/llA9QVP.png)
- shared session key for users

![](https://i.imgur.com/KOaW1Qo.png)

- K(ab) is session key in priv key encryption scheme between Alice & Bob
- subsequent comms between Alice & Bob will have same key as before
    - unless they change their pub keys
- atker must solve discrete log to get Xa r Xb

#### Example
![](https://i.imgur.com/LG2ha9M.png)


### Key Exchange Protocols
- if pub key properly secured in central dir AKA with PKI
    - other users can query pub key, compute secret key, communicate
    - auth of user possible because of PKI
- DH key exchange atks
    - replay atks with/without PKI
    - MITM atks (w/o PKI)



###### tags: `ACG` `DISM` `School` `Notes`