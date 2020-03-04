---
title: 'Lecture 01 Intro to Security'
disqus: hackmd
---

Lecture 01 Intro to Security & Challenges
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

Attacks
---
### Examples of recent attacks
- USB flash drive malware/USB killer
- WINVote voting machine tampering
- Vtech security breach
- stolen data from European Space Agency
- IRS fraud
- Hyatt Hotels Corporation hacked
- etc.

### Reasons for successful attacks
- widespread vulnerabilities
- configuration issues
- poorly designed software
- hardware limitations
- enterprice-based issues

### Difficulties in defending against attacks
![](https://i.imgur.com/LmZW1Jf.png)

Defining Information Security
---
### Information Security
- tasks of securing info in digital format
    - manipulated by microprocessor
    - preserved on storage device
    - transmitted over network
- goal: to ensure that protective measures properly implemented to ward off attacks & prevent total collapse of system when attacked
- as security &#8593;, convenience &#8595;

### 3 types of info protection (CIA)
- confidentiality: only approved individuals may access info
- integrity: info is correct & unaltered
- availability: info accessible to authorised users

### Info security layers
![](https://i.imgur.com/QYfEBZc.png)
- products layer
    - form security around data
    - Eg. door locks, net sec eq, etc
- people layer
    - those who implement & use sec products to protect data
- policies & procedures layer
    - plans & policies etablished by enterprise to ensure that people crrectly use the products

### Terminologies
- asset: item with value
- threat: action that may cause harm
- threat actor: person/element who can cause threat
- vulnerability
    - flaw/weakness that allows threat agent to bypass security
- threat vector
    - means which attack can occur
- risk
    - situation that involves exposure to some danger
    - risk response techniques
        - accept: risk acknowledged but no steps taken to address yet
        - transfer: transfer risk to 3rd party
        - avoid: identify risk but make decision not to engage in activity
        - mitigate: address risk by making risk less serious
- Identity Theft
    - stealing another person's personal info, usually for financial gain
    - Eg.
        - steal person's SSN
        - create new credit card acc to charge purchases & leave unpaid
        - file fradulent tax returns

### Understanding the Importance of InfoSec
- Infosec can be helpful in
    - preventing data theft
    - thwarting identity theft
    - avoiding legal consequences of not securing info
    - maintaining productivity
    - foiling cyberterrorism

During Attacks
---
### Avoiding Legal Consequences
- laws protecting electronic data privacy
    - Health Insurance Portability & Accountability Act of 1996 (HIPAA)
    - Sarbanes-Oxley Act of 2002 (Sarbox)
    - Gramm-Leach-Billey Act (GLBA)
    - Payment Card Industry Data Security Standard (PCI DSS)
    - state notification & security laws
        - California's Database Security Breach Notification Act (2003)
- Singapore laws
    - data privacy - personal data protection act 2012
    - cybersecurity - cybersecurity act 2018
    - cybercrime - computer misuse act (Cap. 50A)

### Maintaining Productivity
- post-attack clean up diverts resources away from normal activities
    - time, money etc
- cost of attacks
![](https://i.imgur.com/VcrF2GA.png)

Cyberterrorism
---
### Foiling Cyberterrorism
- cyberterrorism
    - any premeditated, politically motivated attack aginst info, pc systems, programs & data
- designed to
    - cause panic
    - provoke violence
    - result in financial catastrophe
- may be directed at targets
    - Eg. banking industry, military installations, power plants, air traffic control centers & water systems

Types of Attackers
---
### Threat Actors
- threat actor - individuals who launch attacks against other users & their pcs
    - mostly for financial gain
- financial cybercrime - divided into 2 categories
    - 1st category focuses on individuals as victims
    - 2nd category focuses on enterprises & gov
- diff threat actors varies widely, based on
    - attributes
    - funding & resources
    - whether internal/external to enterprise/org
    - intent & motivation

### Script Kiddies
- individuals who want to attack computers yet lack the knowledge of computers & network needed to do so
    - download automated hacking software (scripts) from websites
    - > 40% of attacks require low/no skills

### Hactivists
- attackers who attack for idealogical reasons generally not as well-defined as cyberterrorist's motivation
- Eg.
    - breaking into website & changing contents on site to make political statement
    - disabling website belonging to bank as bank stopped accepting payments deposited into accounts belonging to hactivists

### Nation State Actor
- attacker commisioned by govs to attack enemies' info systems
    - may target foreign govs/citizens of gov considered hostile/threatening
    - known for being well-resourced & highly trained

### Advanced Persistent Threat
- multiyear intrusion campaign that targets highly sensitive economic, proprietary or national security info

### Insiders
- employees, contractors & business partners
- over 58% of breaches attributed to insiders
- Eg. attacks
    - healthcare workers publicise celebrities' health records
        - disgruntled over upcoming job terminations
    - stock trader conceal losses through fake transactions
    - employees bribed/coerced into stealing data before moving to new job

### Others
![](https://i.imgur.com/bqR8Loh.png)

Defending Against Attacks
---
### Layering
- info sec created in layers
    - single def mechanism easy to circumvent
    - hence unlikely that attacker can break through all def layers
- layered sec approach (AKA def-in-depth)
    - useful in resisting variety of attacks
    - provides most comprehensive protection

### Limiting
- limiting access to info
    - reduce threat aginst it
- only those who use data be granted access
    - limited to only what they need
- methods of limiting access
    - tech-based
        - Eg. file permissions
    - procedural
        - Eg. prohibiting document removal from premises

### Diversity
- closely related to layering
    - layers must be diff (diverse)
- if attackers penetrate 1 layer
    - same technques will be unsuccessful in breaking through other layers
- breaching 1 sec layer does not compromise whole system
- Eg. diversity
    - using sec products from diff manufacturers
    - grps responsible for regulating access (control diversity) are diff

### Obscurity
- obscuring inside details to outsiders
- Eg. not revealing details
    - type of computer
    - OS version
    - brand of software used
- difficult for attacker to devise attack if system details unknown

### Simplicity
- nature of info sec complex
- complex sec systems
    - difficult to understand & troubleshoot
    - often compromised for ease of use by trusted users
- secure system should be simple from the inside
    - but complex from outside


Frameworks & Reference Architectures
---
- industry-standard frameworks & ref architectures
    - provide resources of how to create secure IT env
    - give overall program structure & sec management guidance to implement & maintain effective sec program
- various frameworks/arhictectures specific to particular sector (industry-specific frameworks)
    - Eg. financial industry
- some frameworks/arch domestic
    - others worldwide

Summary
---
![](https://i.imgur.com/MOGWgRZ.png)
![](https://i.imgur.com/Hri60iH.png)



###### tags: `ISEC SEM 2` `DISM SEM 2` `School` `Notes`
