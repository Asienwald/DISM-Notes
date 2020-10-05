---
title: 'Lecture 03 AES'
disqus: hackmd
---

:::info
ST2504 Applied Crypto
:::

Lecture 03 Advanced Encryption Standard (AES)
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


AES Requirements
---
- private key symmetric block cipher
- 128 bit data, 128/192/256 bit keys
- stronger & faster 
    - than triple-DES
- provide full specification & design details
- both C & Java implementations


AES Evaluation Criteria
---
- initial criteria
    - security - effort for practical cryptanalysis
    - cost - in terms of computational efficiency
    - algorithm & implementation characteristics
- final criteria
    - general security
    - ease of software & hardware implementation
    - implementation attacks, example
        - __timing analysis (TA)__ - execution time
        - __power analysis (PA)__ - power consumption
    - flexibility (in en/decrypt, keying, other factors)


AES Shortlist
---
- shortlisted in Aug-99 for further analysis & comment
    - MARS (IBM) 
        - complex
        - fast
        - high security margin
    - RC6 (USA)
        - very simple
        - very fast
        - low security margin
    - Rijindael (Belgium)
        - clean
        - fast
        - good security margin
    - Serpent (Euro)
        - slow
        - clean
        - very high security margin
    - Twofish (USA)
        - complex
        - very fast
        - high security margin
- contrast between algo
    - few complex rounds VS many simple rounds
    - refined existing ciphers VS new proposals
- best balance of attributes to meet criteria, in particular balance between speed, security & flexibility


AES Cipher - Rijndael
---
- designed by Rijmen-Daemen in Belgium
- design considerations
    - resistant against known attacks
    - speed & code compactness on many CPUs
    - design simplicity
- AES variants, key length & round
    - more key size = more rounds = more CPU time
- based on entire data block in every round
![](https://i.imgur.com/b3qZVuC.png)

### Rijndael Features
- block cipher processing 16 bytes at a time
- based on __iterative substitution permutation network__ cipher
- __state__ defined as intermediate cipher result of data block in AES
    - 4 x 4 bytes - table
- typical operations
    - key expansions
    - initial round
    - rounds
        - SubBytes, ShiftRows, MixColumns, AddRoundKey
    - final round consisted of
        - SubBytes, ShiftRows, AddRoundKey
- typical example of AES encryption process with 128 bits of key & 10 rounds of processing
![](https://i.imgur.com/6Mo82tN.png)


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


### AES Round
![](https://i.imgur.com/9l3HM9Q.png)


AES Key Expansion
---
- take 128bit (16 byte) key & expand into array of 44 (10 rounds) x 32bit words (W-in ea col)
- use round constants (RCON) to increase randomness

![](https://i.imgur.com/75fx9hH.png)

- typical operations
    - generate 1st word
        - RotBytes
        - SubBytes using S-box
        - XOR with W0 & RCON

![](https://i.imgur.com/32m7ZOC.png)

- W5-7 generated from prev word XOR with word in prev round (W1-3)
- W8 will have same treatment 
    - rotate bytes/s-box/XOR ops as W3
- process continues

![](https://i.imgur.com/HzUNBrF.png)

### Key Expansion Rationale
- designed to resist known atks
- additional design criteria
    - knwing part key not enough to find more
    - invertible transformation
        - if func f applied in input x gives result of y then applying inverse func g to y gives x, vice versa
    - fast on many CPUs
    - use round const (RCON) to break symmetry
    - diffuse key bits into round keys
    - enough non-linearity to hinder analysis
    - simplicity of description


AES Decryption
---
- decrypt = reverse encrypt
- inverse cipher with steps as for encryption
    - use inverse for ea step
    - with diff key schedule
- no lost of info
    - swap byte sub & shift rows
    - swap mix cols & add (tweaked) round key

![](https://i.imgur.com/X0LYKPM.png)


AES Implementation
---
- efficient on 8bit CPU
    - byte sub, smallest substation table needed only 256 entries for ea byte of data
    - shift rows is simple byte shift
    - add round key workd on byte XOR's
    - mix cols needs matrix multiplication
        - if sufficient memory, process can effectively be converted to table lookups
- very efficient on 32bit CPU
    - need to redefine steps to use 32bit words
    - can pre-compute 4 tables of 256-words
    - ea col in ea round can be computed using 4 table lookups + 4 XORs
    - cost, memory needed of pre-compute tables = 4Kb
- trade off between speed & storage needed



###### tags: `ACG` `DISM` `School` `Notes`