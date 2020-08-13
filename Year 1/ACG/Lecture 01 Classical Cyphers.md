---
title: 'Lecture 01 Classical Cyphers'
disqus: hackmd
---

:::info
ST2504 Applied Cryptography
:::

Lecture 01 Classical Cyphers
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

Terminology
---
- plaintext - original message
- ciphertext - coded message
- cipher - algo for transforming plaintext to ciphertext
- key - info used in cipher, known only to sender/receiver
- encipher (encrypt) - convert plaintext to ciphertext
- decipher (decrypt) - recover plaintext from ciphertext
- cryptography - study of encryption principles/methods
- crypanalysis (codebreaking) - study of principles/methods of deciphering ciphertext w/o knowing key
- cryptology - field of both cryptography & crypanalysis

### Cryptography
- categorise cryptographic systems by
    - diff types of encryption operations used
        - substitution
        - transposition
        - product - multiple stages of substitution & transpositions
    - num of keys used
        - single key or secrete key/two-key or public key
    - way plaintext processed
        - block - blocks of elements
        - stream - 1 element at a time

### Caesar Cipher
- replace each letter of alphabet with letter 3 places down alphabet
- encryption operation: substitution
- strength: weak

Symmetric Encryption
---
__Simplified diagram of Symmetric Cipher__
![](https://i.imgur.com/jUZw4CR.png)

### Symmetric Encryption
- AKA single-key encryption
- sender & receiver share common key
![](https://i.imgur.com/MXWoTrC.png)
- all classical encryption algo are symmetric key algos
- most widely used

### Requirements
- 2 requirements for secure usage of symm encryption
    - strong encryption algo
    - secret key known only to sender & receiver
- usually encryption algo publicly known
    - ![](https://i.imgur.com/h1GC7LY.png)
- secure channel needed to distribute key

Cryptanalysis
---
- 2 general approaches
    - brute force attack
        - try all possible keys
    - cryptanalytic attack
        - based on nature of algo
        - general characteristic of plaintext
        - sample of plaintext-ciphertext pairs
- objective is to recover key in use than recover plaintext of single ciphertext

### Attacks Terminology
- __unconditional security__ (ideal)
    - regardless of computer power/time. cipher cannot be broken since it provides insufficient info to uniquely determine corresponding plaintext
- __computational security__ (realistic)
    - given limited computing resources (Eg. time needed > age of universe), cipher cannot be broken

### Cryptanalytic Attacks
- ciphertext only
    - only know algo & ciphertext
    - plaintext is statistical/can identify
    - hardest
- known plaintext
    - know/suspect plaintext & ciphertext
- chosen plaintext
    - select plaintext & obtain ciphertext
- chosen ciphertext
    - select ciphertext & obtain plaintext
- chosen text
    - select plaintext or ciphertext to en/decrypt

### Brute Force Search
- try every possible key
- most basic attack
    - proportional to key size
- assume either know/recognise plaintext
![](https://i.imgur.com/nguX9BH.png)
- [See also](http://tjscott.net/crypto/64bitcrack.htm)


### One-Time Pad
- ideal cipher
- unbreakable
    - ciphertext bears no statistical r/s to plaintext
    - for any plaintext & any ciphertext there exists a key mapping 1 to another
- practical difficulties in generation & safe distribution of key can be used __once__ only
    - hence not widely used today
- preconditions
    - key must as long as plaintext
    - key must be truly random
    - key must only be used once

### Steganography
- alternative to encryption
- hides existence of message
    - using only subset of letters/words in longer message marked in some way
    - using invisible ink
    - hiding info in LSB of graphic img/sound file
- drawbacks
    - high overhead to hide relatively few info bits


Classical Ciphers - Substitution Ciphers
---
- letters of plaintext replaced by other letters, numbers or symbols
    - if plaintext viewed as sequence of bits, substitution involves replacing plaintext bit patterns with ciphertext bit patterns

__Caesar Cipher__
- earliest known substitution cipher
- by Julius Caesar
- used in military
- replace ea letter by 3rd letter on
![](https://i.imgur.com/OwUtIVx.png)

### Monoalphabetic Cipher
- arbitrarily map ea plaintext letter to diff random ciphertext letter
- key 26 letters long
    - n! > 4 * 10^26
![](https://i.imgur.com/SOpUDf8.png)

### Playfair Cipher
- https://www.geeksforgeeks.org/playfair-cipher-with-examples/
- large num of keys in monoalphabetic cipher provides security
    - if crypanalyst knows nature of plaintext (Eg. non-compressed english text), can exploit regularities of the language
        - Eg. frequency distribution of particular letters in ciphertext
- 1 approach is to encrypt multiple letters
    - hence, Playfair Cipher
    - invented by Charles Wheatstone in 1854; named after friend Baron Playfair
- key matrix
    - 5 x 5 matrix of letters based on key
    - fill in key, remove dupes
        - use I and J interchangeably
    - fill matrix with remaining letters
        - Eg. use key MONARCHY
![](https://i.imgur.com/82cA3PG.png)

__Encrypting & Decrypting__
- plaintext encrypted 2 letters at a time
    - if pair is repeated letter, insert filler like 'X'
        - Eg. hello = helxlo
        - insert filler to make even length so can form pairs
    - if both letters fall in same row, replace ea with letter to right
        - wrap back to end
        - Eg. "AR" > "RM"
    - if both letters fall in same column, replace ea with letter below it
        - wrap to top from bottom
        - Eg. "MU" > "CM"
    - otherwise ea letter replaced by letter in same row & column of other letter of pair
        - Eg. "HS" > "BP" and "EA" > "IM" or "JM"
        - form square with the 2 letters and pick the other 2 corners
- __Note__
    - usually remove J as 25 boxes but 26 alphabets
    - if odd, add filler (Eg. "X")
    - if duplicate. split & add "X"

__Security of Playfair Cipher__
- security improved over monoalphabetic
    - 26 x 26 = 676 digraphs
    - need to analyse frequency table of 676 entries
        - VS 26 for monoalphabetic encryption
    - hence need more ciphertexts to analyse
- widely used for many years
    - Eg. US & British military in WW1 AND WW2
- can be broken, given few hundred letters since has must of plaintext structure

## Polyalphabetic Ciphers
- same plaintext ciphers can be replaced by diff ciphertext alphabets
    - Eg. BEE > FHG depending on key used
- makes cryptanalysis harder with more alphabets to guess & flatter frequency distribution
    - Eg. instead of BEE > FHH have BEE > FHG
- key selects which ciphertext alphabet used to substitute ea letter of message
- apply ea key alphabet in turn, repeat from start after end of the key is reached
    - if key short and we have large msg to decrypt, will still have frequency analysis


### Vignere Cipher
- simplest polyalphabetic substitution cypher
- align plaintext & key, repeat key letters to match plaintext length
    - Eg. using keyword "deceptive"
        - key: deceptivedeceptivedeceptive
        - plaintext: wearediscoveredsaveyourself
            - use crossword to solve
![](https://i.imgur.com/WwCIvoc.png)

__Security of Vignere Cipher__
- security improved with multiple ciphertext letters for ea plaintext letter
- letter frequencies obscured but __not toally lost__
    - start with letter freq analysis, check whether matches monoalphabetic cipher characteristics
        - Eg. % of "e" occurrence
    - if not if 2 identical sequences of plaintext letters occur at dist that is int multiple of keyword length, will generate identical ciphertext sequences
        - Eg. red > VTW
            - guess that key length 3 or 9

Classical Ciphers - Transposition Ciphers
---
- transposition or permutation ciphers
- hide msg by rearranging letter order w/o altering actual letters used
- can be recognised since have same frequency distribution as original text

### Rail Fence Cipher
- write msg letters out diagonally over number of rows
- read off ciphertext row by row
- Eg. ![](https://i.imgur.com/dJkpszL.png)
    - plaintext is "meetmeafterthetogaparty"

### Row Transposition Ciphers
- write letters of msg out in rows over specified num of columns
- reorder columns according to some key before reading off rows
    - ![](https://i.imgur.com/Wf6HfXH.png)

### Rotor Machines
- before modern ciphers were most common complex cipher
- widely used in WW2
    - Eg. German Enigma
    - implemented very complex, varying substitution cipher
- used series of cylinders, ea giving 1 substitution, which rotated & changed after ea letter encrypted
- with 3 cylinders have 26^3 = 17576 alphabets
- [Watch](https://www.youtube.com/watch?v=G2_Q9FoD-oQ)


### Product Ciphers
- using only substitutions or transpositions not secure due to language characteristics
    - 2 substitutions = more complex sub
    - 2 transposition = more complex tran
- substitution followed by transposition = new harder cipher
    - basis of modern cipher

![](https://i.imgur.com/FLozKZH.png)



###### tags: `ACG SEM 2` `DISM SEM 2` `School` `Notes`