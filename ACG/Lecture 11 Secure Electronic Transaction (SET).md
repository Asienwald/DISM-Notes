---
title: 'Lecture 11 Secure Electronic Transaction (SET)'
disqus: hackmd
---

:::info
ST2504 Applied Cryptography
:::

Lecture 11 Secure Electronic Transaction (SET)
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

Impt for EST
---
- what is RSA
    - what does it ensure
    - the HBL calculation

### Lecture 01 Classical Ciphers
- what is one-time pad
- playfair cipher
    - L1 slide 22, 23
- vigenere cipher
    - slide 25, 26
- what is diff between substitution & transposition cipher?
    - slide 28
- rail fence cipher
    - slide 29
- row transposition cipher
    - slide 30

### Lecture 02 DES
- feistel scheme
    - dont need detail
    - need aware that DES is using what scheme
    - construction of the scheme
    - slide 7, 8
- 

### Lecture 03 AES
- requirements, how it works
    - slide 6, 8
- s-box
    - when asked abt AES, will be asked abt s-box
    - during exam given s-box, need to know how to use it
    - slide 8, 10

### Lecture 07 Digital Signatures
- how digital sign etc works
    - slide 1-6
- direct vs arbitrated
    - slide 9, 10, 11

### Lecture 09
- diffie-hellman key exchange
    - slide 14

### Lecture 10 PGP
- PGP one qns (application qns)
    - slide 18, 19, 20, 22

### Lecture 11 SET
- slide 5, 6
- remaining slide used for understanding



Review Questions
---
### Blind Signature
- blind signature is form of digital signature whr content of msg disguised/blinded before signed
    - resulting blind signature can be publicly verified against orig like regular digital signature
- how it works
    - alice obtain signatures on her letter
    - bob is signer in possession of his secret key
    - alice send letter in envelope to bob
    - bob signs over letter w/o seeing contents
    - in the end, alice obtains sign on letter w/o bob knowing msg


Secure Electronic Transations (SET)
---
- open encryption & security specification
    - to protect internet credit card transactions
- developed in 1996 by Mastercard, Visa etc.
- not payment system
- set of security protocols & format
    - secure comms amongst parties
    - trust from use of X.509v3 certs
    - privacy restricted info to those who need it

### SET Components
![](https://i.imgur.com/xgQ2Cq4.png)

### SET Transaction
- customer opens acc
- customer receives cert
- merchants have own certs
- customer places order
- merchant verified
- order & payment sent
- merchant requests payment authorisation
- merchant cfms order
- merchant provides goods or service
- merchant requests payment


### Dual Signature
- purpose to link 2 msgs intended for 2 diff recipients by same sender
- process
    - customer creates dual msgs
        - __order info (OI)__ for merchant
        - __payment info (PI)__ for bank
    - neither pt needs details of other
        - but must know they linked
    - use dual signature
        - signed concatenated hashes of OI & PI
        - ![](https://i.imgur.com/g3ATcEq.png)

#### How it works
- when customer wants to send order info (OI) to merchant & payment info (PI) to bank
- 2 items must be linked in way that can be used to resolve disputes if needed
- prevents merchant from fabricating OI & claims that as orig OI
    - linkage prevents this
- link needed so customer can prove payment intended for this order
- customer takes hash (using SHA-1) of PI & hash of OI and concatenates them
    - then hash result
- finally customer encrypts final hash with his priv key, creating dual signature
- merchant dont need to know customer's credit card num & bank dont need to know details of customer's order
- summarised as:

![](https://i.imgur.com/nch5Dox.png)


### SET Purchase Request
- consists of 4 msgs
    - initiate request - get certs
    - initiate response - signed response
    - purchase request - of OI & PI
    - purchase response - ack order

#### Purchase Request - Merchant
- verify cardholder cert using CA sigs
- verify dual sign using customer's public key to ensure order not tampered with in transit & signed using cardholder's priv key
- process order & forwards payment info to payment gateway for authorisation
    - described ltr
- send purchase resp to cardholder

![](https://i.imgur.com/Q9VpSrd.png)


#### Purchase Request - Customer
![](https://i.imgur.com/xtoQ0ER.png)


### Payment Gateway Authorisation
- verify all certs
- decrypts digital envelope of authorisation blk to obtain symmetric key then decrypt authorisation blk
- verify merchant's signature on authorisation blk
- decrypts digital envelope of payment blk to obtain symmetric key then decrypt payment blk
- verify dual sign on payment blk
- verify transaction ID from merchant matches in PI received from customer
- requests & receives authorisation from issuer
- sends authorisation resp to merchant

### Payment Capture
- merchant sends payment gateway & payment capture request
- gateway checks request
    - cause funds to be transferred to merchant's acc
- notifies merchant using capture response


Summary
---
![](https://i.imgur.com/E9Z46Ga.png)



###### tags: `ACG` `DISM` `School` `Notes`