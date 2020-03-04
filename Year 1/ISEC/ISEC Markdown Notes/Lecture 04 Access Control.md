---
title: 'Lecture 04 Access Control'
disqus: hackmd
---

:::info
ST1004 Infocomm Security
:::

Lecture 04 Access Control
===

<style>
img{
/*     border: 2px solid red; */
    margin-left: auto;
    margin-right: auto;
    width: 90%;
    display: block;
}
</style>


## Table of Contents

[TOC]


Authentication Credentials
---
- types
    - where you are
    - what you have
    - what you are
    - what you know
    - what you do

What you know - Passwords
---
- most common type of auth
    - but weak
- weaknesses (6)
    - human's memory is limited
        - long complex passwords are most effective but difficult to memorise
    - must rmb passwd for many diff accs
    - ea password must be unique
    - security policies that mandate passwords must expire
        - users must repeatedly memorise passwords
    - users often take shortcuts
        - use weak password - common words, short, personal info etc
    - follow predictable patterns when creating stronger passwords
        - appending - using letters, nums, punctuation in pattern
        - replacing - replace in predictable patterns
- attacks on passwords
    - social engineering
        - phishing, shoulder surfing, dumpster diving
    - capturing
        - kelogger, protocol analyser
        - MIM & replay attacks
    - resetting
        - gains physical access to pc and resets pwd

### Offline attacks on passwords
- attackers steal file of password digests
    - compare with own digests they created
- __Brute Force__
    - every possible combi of letters, nums & chars used to create encrypted pwds & match against stolen file
    - slowest, most thorough method
    - __NTLM (New Tech LAN Manager) Hash__
        - attacker who steal digest of NLTM pwd don't have to break it
        - can simply pretend to be user & send the hash to remote system to be authenticated
        - AKA pass the hash attack
- __Mask Attack__
    - more targeted brute force atk that uses placeholders for chars in certain pos of pwd
    - params include
        - pwd length
        - char set
        - language
        - pattern
        - skips
- __Rule Attack__
        - conducts statistical analysis on stolen pwds used to create mask to break largest num of pwds

![](https://i.imgur.com/JTAb7wq.png)

- __Dictionary Attack__
    - attacker creates digest of common dictionary words
        - compare against stolen file
    - __pre-image attack__ - dict atk that uses set of dict words & compares with stolen digests
    - __birthday atk__ - search for any 2 digests that are same

- __Rainbow Tables__
    - creates large pregenerated data set of candidate digests
    - steps to create table
        - chain of plaintext pwds
        - encrypt intial pwd
        - feed into func that produces diff plaintext pwds
        - repeat for set num of rounds
    - steps to use table to crack pwd
        - run encrypted pwd through same procedure used to create initial table
        - results in initial chian pwd
        - repeat, starting with intial pwd until orig encryption found
        - pwd used at last iteration is cracked pwd
    - advantages
        - can be used repeatedly
        - faster than dict atks
        - less memory on attacking machine required
- __Password Collections__
    - in 2009, atker used SQL injection atk & more than 32m pwds in cleartext stolen
    - these pwds provided 2 key elements for pwd atks
        - large corpus of real-world pwds
        - provided atkers advanced insights into strategic thinking of how users create pwds

### Password Security
- depends on 
    - user - properly managing pwds
    - enterprise - protecting pwd digests
- managing pwds
    - length most critical
    - don't consist of dict words or phonetic words
    - don't repeat chars or use sequences
    - don't use bdays, fam names, pet names, personal info etc.
    - use non-keyboard chars
        - created by holding down ALT key while typing num on numeric keypad


- password managers
    - tech used for securing pwds
    - 3 basic types
        - pwd generators
        - online vaults
        - pwd management apps
- protecting pwd digests
    - use salts
        - random string used in hash algo
        - pwd protected by adding random string to user's cleartext pwd before hashed
        - make dict atks & brute force atks slower & limit impact of rainbow tables
    - key stretching
        - specialised pwd hash algo intentionally designed to be slower
        - 2 stretching algos
            - brypt
            - PBKDF2
    - recommendations for enterprise who use salting & key stretching
        - use strong random num generator to create salt of at least 128 bits
        - input salt & user's plaintext pwd into PBKDF2 algo that is using HMAC-SHA-256 as core hash
        - perform at least 30,000 iterations on PBKDF2
        - capture 1st 256 bits of output from PBKDF2 as pwd digest
        - store iteration count, salt & pwd digest in secure pwd database


What you have - Tokens, Cards and Phones
---
- multifactor authentication
    - use more than 1 authentication credential
- singlefactor authentication
    - just 1 type of auth

### Tokens
- used to create __one-time password (OTP)__
    - auth code used only once for limited period of time
- hardware security token
    - small device with window display
- software security token
    - stored on general-purpose device like laptop PC or smartphone
- 2 types of OTPs
    - time-based OTP (TOTP)
        - synched with auth server
        - code generated from algo
        - code changes every 30 to 60 seconds
    - HMAC-based OTP (HOTP)
        - event-driven & changes when specific event occurs
- advantages over pwds
    - token code changes frequently
        - atker have to crack code within time limit
    - user may not know if pwd is stolen
        - if token stolen, is obvious & steps can be taken to disable acc

![](https://i.imgur.com/nFRhrXv.png)


### Cards
- smart card contains integrated circuit chip that holds info & can be either
    - contact card - pad that allows electronic access to chip elements
    - contactless cards/proximity cards
        - need no phy access to card
    - common access card (CAC)
        - issued by US department of defense
        - bar code, magnetic chip & bearer's pic
- smart card standard covering all US gov employees is __Personal Identity Verification (PIV)__ standard

![](https://i.imgur.com/uH0gLUV.png)

### Cell Phones
- increasingly replacing tokens & cards
- code can be sent to user's phone through app
    - allow user to send request via phone to receive HOTP auth code


What you are - Biometrics
---
- biometrics involve
    - standard biometrics
    - cognitive biometrics

### Standard Biometrics
- uses person's unique phy characteristics for auth
    - face, hand or eye characteristics used to authenticate
- specialised biometric scanners
    - retinal scanner uses human retina as biometric identifier
        - maps unique patterns of retina by directing beam of low-energy infrared light (IR) into person's eye 
    - fingerprint scanner types
        - static fingerprint scanner - takes pic & compares with img on file
        - dynamic fingerprint scanner - uses small slit or opening
- standard input devices
    - voice recog use comp mic to identify users based on unique characteristics of voice
    - iris scanner use standard webcam to identify unique char of iris
    - facial recog use landmarks called __nodal pts__ on faces for authentication
- disadvantages
    - cost of hardware
    - readers have some error
        - reject authorised users
        - accept unauthorised users
    - can be tricked

### Cognitive Biometrics
- cognitive biometrics
    - relates to perception, thought process & understanding of user
    - easier for user to rmb as based on user's life experiences
    - difficult for attacker to imitate
- picture passwd
    - introduced by windows
    - select pic to use whr thr shld be at least 10 "pts of interests" that can serve as landmarks/places to touch
- other examples
    - identify faces
    - selects 1 of memorable events
- behavioral biometrics
    - authenticates by norm actions user performs
- keystroke dynamics
    - recognise user's typing pattern
        - all users type at diff pace
        - up to 98% acc
    - 2 unique typing variables
        - dwell time - time take to press & release key
        - flight time - time bwteen keystrokes
    - great potential
        - need no specialised hardware


Where you are - Geolocation
---
- geolocation
    - identification of location of person/object using tech
- used often to reject imposters instead of accepting authorised users
    - can indicate if atker trying to perform malicious action from location diff from norm location of user
    - many sites dont allow user to access acc if comp located in diff state
    - some sites may need 2nd type of auth
        - code sent as text msg to phone


Access Control
---
- access control - granting/denying approval to use specific resources
    - physical
        - fencing, hardware door locks, mantraps etc
    - technical
        - tech restrictions that limit users from accessing data
- standard access control models used to enforce access control

### Terminology
- identification
    - presenting credentials
- authentication
    - checking credentials
- authorisation
    - granting permission to take action
- accounting
    - record preserved of who accessed network, what resources accessed & when they disconnected

![](https://i.imgur.com/zS0QjSl.png)

- object
    - specific resource
- subject
    - user/process functioning on behalf of user
- operation
    - action taken by subj over an object

![](https://i.imgur.com/mk8mUhr.png)

### Access Control Models
- access control model
    - standards that provide predefined framework for hardware or software devs
    - use appropriate model to config necessary lvl of control
- 5 major access control models
    - discretionary access control (DAC)
    - mandatory access control (MAC)
    - role based access control (RBAC)
    - rule based access control
    - attribute based access control (ABAC)

#### Discretionary Access Control (DAC)
- least restrictive model
- every object has owner
- owners have total control over their objects
- owners can give permissions to other subjects over their objects
- used on OS like most UNIX & microsoft windows
- 2 significant weaknesses
    - relies on decision by end user to set proper lvl of security
    - subject's permissions inherited by any programs that subject executes

![](https://i.imgur.com/9ILmE5i.png)

#### Mandatory Access Control (MAC)
- most restrictive model
    - user has no freedom to set any controls/distribute access to other subjs
- typically found in military settings
- 2 elements
    - labels - every entity is an obj & assigned classification label that reps the relative importance of the obj
        - subjs assigned privilege label (clearance)
    - levels - hierarchy based on labels used
        - top secret has higher lvl than secret which has higher lvl than confidential
- MAC grants permissions by matching obj labels with subj labels
    - labels indicate lvl of privilege
- to determine if file opened
    - obj and subj labels compared
    - subj must have equal or greater lvl than obj to be granted access
- 2 major implementations of MAC
    - __Lattice Model__
        - subjs & objs assigned a "rung" on the lattice
        - multiple lattices can be placed beside ea other
    - __Bell-LaPadula BLP Model__
        - similar to lattice model
        - subjs may not create new obj or perform specific func on lower lvl objs
- Microsoft Windows uses MAC implementation called __Mandatory Integrity Control (MIC)__
    - security identifier (SID) issued to user, grp or session
    - ea time user logs in, SID retrieved from db
    - SID used to identify user with subsequent interactions with Windows
    - windows links SID to an integrity lvl
    - __User Access Control (UAC)__ - windows feature that controls user access to resources

#### Role-Based Access Control
- AKA non-discretionary access control
- access permission based on user's job func
- RBAC assigned permissions to particular roles in org
    - users assigned to roles

#### Rule-Based Access Control
- AKA rule-based role-based access control (RB-RBAC)
    - dynamically assigns roles to subjs based on set of rules defined by custodian
- ea res obj contains access properties based on rules
    - when user attempts access, system checks obj's rules to determine access permission
- often used for managing user access to 1 or more systems
    - business changes may trigger app of rules specifying access changes

#### Attribute-Based Access Control (ABAC)
- more flexible policies than rule-based AC
    - can combine attributes
- policies take advantage of attributes like
    - obj attributes
    - subj attributes
    - environment attributes
- ABAC rules can be formatted uses If-Then-Else structure

![](https://i.imgur.com/BKRlKJO.png)


### Best Practices
- establish best prac for limiting access can help secure systems & data
- Examples
    - separation of duties
    - job rotation
    - mandatory vacations
    - clean desk policy

#### Separation of Duties
- fraud can result from single user being trusted with complete control of process
    - need 2 or more people responsible for funcs related to handling money
    - system not vulnerable to actions of single person
- in relation to computer access control
    - requires that if fraudulent app of process could potentially result in breach of security, the process shld be divided between 2 or more indivs

#### Job Rotation
- indivs periodically moved between job responsibilities
    - employees can rotate within department/across departments
- advantages
    - limits amt of time indivs are in pos to manipulate security configs
    - helps expose potential avenues for fraud
        - indivs have diff perspectives & may uncover vulns
    - reduces employee "burnout"

#### Mandatory Vacations
- limits fraud as perpetrator must be present daily to hide fraudulent actions
- audit of imployee's activities usually scheduled during vacation for sensitive positions

#### Clean Desk Policy
- designed to ensure that all confidential/sensitive materials removed from user's workspace & secured when items not in use
    - paper form or electronic
- example
    - workstations must be locked when workspace unoccupied & turned off at end of day
    - confidential/sensitive info must be removed from desk & locked in drawer/safe when desk unoccupied/end of day
    - file cabinets must be kept closed & locked when not in use or not attended & keys may not be left at unattended desk
    - laptops must be locked with locking cable or locked in drawer or filing cabinet

Chapter Summary
---
![](https://i.imgur.com/vfEoDCP.png)
![](https://i.imgur.com/WP4IQP0.png)



###### tags: `ISEC SEM 2` `DISM SEM 2` `School` `Notes`