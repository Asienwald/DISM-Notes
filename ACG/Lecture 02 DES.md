

Lecture 02 Data Encryption Standard (DES)
===



## Table of Contents

- [Lecture 02 Data Encryption Standard (DES)](#lecture-02-data-encryption-standard--des-)
  * [Block & Stream Ciphers](#block---stream-ciphers)
    + [Block Cipher Principles](#block-cipher-principles)
    + [Substitution-Permutation Networks](#substitution-permutation-networks)
    + [Feistel Scheme](#feistel-scheme)
  * [Data Encryption Standard (DES)](#data-encryption-standard--des-)
    + [DES Design Controversy](#des-design-controversy)
    + [Types of Permutation](#types-of-permutation)
    + [Encryption Steps](#encryption-steps)
    + [DES - Round Structure](#des---round-structure)
    + [Substitution Boxes S](#substitution-boxes-s)
    + [DES - Decryption](#des---decryption)
    + [DES - Key Schedule](#des---key-schedule)
    + [Avalanche Effect](#avalanche-effect)
    + [DES - Considerations](#des---considerations)

Block & Stream Ciphers
---
- __stream__ ciphers process msgs bit/byte at a time when en/decrypting
    - Eg. video stream
- __block__ ciphers process msgs in blocks
    - typical block size is 64/128 bits
    - most current ciphers are block ciphers
        - broader range fo apps (nature of data)
        - allow more complex design (more secure if implemented correctly)

### Block Cipher Principles
- based on following
    - __substitution-permutation networks__
    - __Feistel Scheme__
    - generalised feistel sceheme (variants of feistel scheme)
    - lai-messy scheme (not tested)
- block ciphers > large substitution tool
    - choice of block size does not directly affect strength of encryption scheme
        - strength depends on key length
    - implemented from smaller building blocks
    - typically is product cipher

### Substitution-Permutation Networks
- proposed by Claude Shannon 1949
- basis of modern ciphers
    - introduced idea of sub-perm networks (S-P nets)
    - based on 2 primitive crypto operations
        - substitution (S-box of cipher)
        - permutation (P-box of cipher)
- provide __confusion__ and __diffusion__ of msg & key
- AES standard use iterated sub-perm networks for encryption/decryption
- cipher should completely obscure statistical properties of original msg
- Shannon suggested combining sub & perm elements to obtain
    - diffusion
        - seeks to make stat r/s between plaintext & ciphertext complex af to prevent attempts to deduce key
        - use perm or transposition
    - confusion
        - makes r/s between ciphertext & key complex af to prevent attempts to discover key
        - use substitution

### Feistel Scheme
__Background__
- widely used to illustrate block cipher design principles
- variants based on "classical" feistel scheme
    - unbalanced feistel networks
        - with expanding & contracting rounds
    - alternating feistel networks
        - with steps alternate in expanding & contracting rounds
    - oothers
- used in DES
- once most widely used crypto algo
- proven secrecy

__Construction__
1. split block data (in bits) into half
2. using data from right half, apply substitution + subkey to encrypt
3. using data from left half, apply XOR with left and right to get resultant left half
    - for XOR, if bits same = 0, bits diff = 1
4. swap the 2 halves for next cycle
5. repeat for 16 rounds
![](https://i.imgur.com/h2pGlHC.png)
- continued
    - ![](https://i.imgur.com/cxKnkhS.png)
    - [F] - round func perform the S-box and P-box
    - after 2 rounds = all data will be encrypted once
        - left & right halves

__Design Elements__
- considerations
    - block size
    - key size
    - number of rounds
    - subkey (K1, K2, K3, ... Kn) generation algo
    - round function
- __Note__: greater complexity can make analysis harder but slows cipher
    - trade off

__Decryption__
- essentially same as encryption
- encryption - 16 subkeys generated from key
- decryption
    - reverse subkeys applied Eg. Kn in 1st round, Kn-1 2nd & K1 in last
- implementation
    - only 1 set of instructions needed
- recall R0 = L1
    - using [F] + subkey + L1, to generate same output as encryption
    - XOR with R1 to get R0

Data Encryption Standard (DES)
---
- widely used  widely used block cipher specified & adopted by US gov
    - adopted by National Bureau of Standards (NBS, now NIST) in 1977 as Federal Info Processing Standard (FIPS) PUB 46
- encrypts 64bit data using 56bit key

__History__
- IBM developed by Lucifer cipher
    - team led by Fesitel in late 60s
    - used 64bit data blocks with 128bit key
- redeveloped as commercial cipher with input from National Security Agency (NSA) & others
- National Bureau of Standards (NBS) issued request for proposals for national cipher standard (in 1973)
- IBM submitted their revised Lucifer cipher, later accepted as DES

### DES Design Controversy
- DES standard public but considered controversy over its design
    - 56-bit key (VS Lucifer 128-bit) though DES designed to accept 64-bit key
    - S-boxes used designed under classified conditions & led people to think iits a "trapdoor" for NSA
- Broken due to its 56-bit key
- heavily used in legacy apps especially in financial apps


### Types of Permutation
- __Normal Permutation__
    - bits change places
    - Eg. 4 bits in, 4 bits out
- __Expansion Permutation__
    - bits might be expanded into more bits
    - will have table to explain how to expand
    - Eg. 4 bits in, 6 bits out
- __Compression Permuation__
    - some bits supressed
    - Eg. 6 bits in, 4 bits out


### Encryption Steps
- initial permutation (IP)
- 16 key dependent round functions
- final permutation
- __1st & last step__: initial & inverse initial permutation
    - initial & final permutations are straight permutation boxes (P-boxes) that are inverses of each other
__Initial Permutation (1st step)__
![](https://i.imgur.com/W6BDpMM.png)
__Inverse Initial Permutation (Last Step)__
![](https://i.imgur.com/my11v6C.png)

### DES - Round Structure
- Round function
    - expands R from 32 --> 48 bit using Expansion P-box functiion
    - XOR with 48-bits subkey K
    - passes through 8 S-boxes to get 32 bit result
    - Permutes using 32 bit [P] function
![](https://i.imgur.com/s5gpRMu.png)
![](https://i.imgur.com/DSFUxp8.png)

### Substitution Boxes S
- 8 different S-boxes working in parallel
- Maps 6 to 4 bits
- Value in the selected cell is returned after the process
    - bits 1 & 6 
        - row bits
    - bits 2-5
        - col bits or inner bits

![](https://i.imgur.com/hrNfjNg.png)

### DES - Decryption
- Must unwind steps of data comptation
- With Feistel design, do encryption steps again using subkeys in reverse order(SK<sub>16</sub> --> SK<sub>1</sub>)
    - Initial permutation undoes final permutation step of encryption
    - 1st round with SK<sub>16</sub> undoes 16th encrypt round until the 16th round, which undoes 1st encryption round
    - final permutation undoes initial permutation, recovering original data

### DES - Key Schedule
- Generate 16 subkeys from secret key
- Use PC-1 for initial permuation
- 56 bits used
    - 8,16,24,32,40,48,56,64 considered parity bits
- resultant 56 bits intermediate subkey split into 2 x 28 bits halves 
- All bits in each half will be shifted to the left
    - first bit goes to the end of the block
- Refinement of 16 subkeys
    - Left rotate each halve separately
        - 1-2 places based on key rotation schedule
    - Use PC-2 for permutation & select 48 bits from 56 bits
![](https://i.imgur.com/hcNF7gm.png)

### Avalanche Effect
- Desirable property of encryption
- Eg: DES
    - 1 bit change of input/key --> ard half output bits changed

### DES - Considerations
- 56 bit keys have 2<sup>56</sup> values
- Brute force used to be hard
    - 1997 --> few months on Internet
    - 1998 --> few days (on dedicated hardware)
    - 1999 --> 22h (Internet + dedicated hardware)
- Must be able to recognize plaintext
- Must consider alternatives to DES


###### tags: `ACG` `DISM` `School` `Notes`