---
title: 'Lecture 02 System Security I'
disqus: hackmd
---

Lecture 02 System Security I
===

:::info
ST1004 Infocomm Security
:::

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


Malware
---
__Attacks using Malware__
- malicious software (malware)
    - enters pc system w/o owner's knowledge/consent
    - uses threat vector to deliver malicious "payload" that performs harmful function once invoked
- malware - general term for damaging/annoying software
    - can be classified using primary trait of malware
        - __circulation__ - spreading rapidly to other systems to impact large number of users
            - 2 types have this primary trait
                - viruses
                - worms
        - __infection__ - how it embeds itself into a system
        - __concealment__ - avoid detection by concealing presence from scanners
        - __payload capabilities__ - what actions malware performs

Circulation Malware
---

### Virus
- __computer virus__ - malicious computer code that reproduces itself on same computer
- __program virus__ - infects exe file
- __macro__ - series of instructions that can be grouped tgt as single command
    - common data file is __macro virus__ written in script known as macro
- virus infection method
    - __appender infection__ - virus appends itself to end of file
        - easily detected by virus scanners
    - ![](https://i.imgur.com/b1eEimI.png)
- __armored virus__ - go to great lengths to avoid detection
    - armored virus techniques
        - __swiss cheese infection__ - inject themselves into exe code 
            - virus code scrambled to make it more difficult to detect
            - ![](https://i.imgur.com/tl1FCup.png)
        - __split infection__ - virus splits into several parts
            - parts placed at random pos in host program
            - parts may contain unnecessary "garbage" to mask true purpose
            - ![](https://i.imgur.com/xVhNjIy.png)

        - __mutation__ - virus may mutate/change
            - __oligomorphic virus__ changes internal code to 1 of a set of number of predefined mutations whenever executed
                - based on some num they do sth
            - __polymorhic virus__ completely changes from original form when executed
            - __metamorphic virus__ can rewrite own code & appear diff ea time executed

__What do they do?__
- performs 2 actions
    - unloads payload to perform malicious action
    - reproduces itself by inserting code into another file on same computer
- Eg. of virus actions
    - cause computer to repeatedly crash
    - erase files from/reformat hard drive
    - turn of computer's security settings
- viruses cannot auto spread to another computer
    - relies on user action to spread
- attached to files
    - spread by transferring infected files


### Worms
- worm - malicious program that uses computer network to replicate
    - sends copies of itself to other network devices
- worms may
    - consume resources
    - leave behind payload to harm infected systems
- Eg. actions
    - deleting computer files
    - allowing remote control of computer by attacker

![](https://i.imgur.com/CpqUKT3.png)


Infection Malware
---
### Trojan
- trojan - exe program that does sth other than advertised
    - contain hidden code that launches attack
    - sometimes made to appear as data file
- Eg
    - user downloads "free calendar program"
    - program scans system for credit card numbers & passwords
    - transmit info to attacker through network
- special type of trojan
    - __Remote Access Trojan (RAT)__ - gives threat actor unauthorised remote access to victim's computer by specially configured comm protocols

### Ransomware
- ransomware - prevents user's device from properly operating until fee paid
    - highly profitable
- variation of ransomware displays a fictitious warning that software license expired or there's problem & users must purchase additional software online to fix problem

### Crypto-Malware
- crypto-malware - more malicious form of ransomware where threat actors encrypt all files on device so none can be opened
- once infected,
    - software connects to threat actors __command & control (C&C)__ server to receive instructed/updated data
    - locking key generated for encrypted files & key is encrypted with another key downloaded from the C&C
    - 2nd key sent to victims once they pay ransom



Concealment Malware
---
### Rootkits
- rootkit - software tools used by attacker to hide actions/presence of other types of malicious software
    - hide/remove traces of log-in records, log entries
- may alter/replace OS files with modified versions specifically designed to ignore malicious activity
- users can't trust computer that contains rootkit
    - rootkit in charge & hides what's occuring in computer
![](https://i.imgur.com/QnOocQA.png)


Payload Capabilities
---
- destructive power of malware found in its payload capabilities

### Collect Data
- collect important data from target
- type of malwares
    - __spyware__ - gathers info w/o user consent
        - uses pc resources for collecting & distributing personal/sensitive 
        - can be hardware device/software program
            - hardware device inserted into pc
            - software installed on pc & silently capture
                - advantage - don't need physical access to user's computer
                - often installed as trojan/virus, can send captured info back to attacker via internet
    - __keylogger__ - captures & stores ea keystroke user types on pc keyboard
        - attacker searches captured text for useful info (Eg. passwords, etc)
        - ![](https://i.imgur.com/xBD1DyW.png)
        - ![](https://i.imgur.com/cYJiJPQ.png)
    - __adware__ - program that delivers ad content unexpectedly & unwantedly
        - typically displays ad banners & pop-up ads
        - may open random new browser windows
        - disapproved as
            - can display objectionable content
            - frequent popup ads can interfere with productivity
            - popups can slow computer/cause crashes/loss of data
            - unwanted ads are nuisance

### Delete Data
- payload deletes data on pc
- types of malware
    - __logic bomb__ - program that lies dormant until triggered by specific logic event
        - difficult to detect before triggered
        - often embedded in large computer programs that's not routinely scanned

### Modify System Security
- __backdoor__ - give access to pc, program or service that circumvents normal security to give program access
    - when installed, they allow computer to return at later time & bypass security settings

### Launch Attacks
- __bot/zombie__ - infected computer under remote control of attacker
    - groups of zombie computers gathered into logical computer network called __botnet__ under control of attacker __(bot herder)__
    - infected zombie computers wait for instructions through __command & control (C&C)__ structure from bot herders
        - common C&C mechanism used today is HTTP - more difficult to detect & block
    - ![](https://i.imgur.com/XShmFRx.png)

Social Engineering Attacks
---
- social engineering - means of gathering info for attack by relying on weakness of individuals
    - can involve psychological approaches/physical procedures

### Psychological Approaches
- goal - persuade victim to provide info/take action
- attackers use variety of techniques to gain trust w/o moving quickly
    - provide reason
    - project confidence
    - use evasion & diversion
    - make them laugh
- often involve
    - impersonation, phishing, spam, hoaxes & watering hole attacks

__Impersonation__
- attacker pretends to be someone else
    - often impersonate person with authority as victims generally resist saying "no" to anyone in power

__Phishing__
- sending email claiming to be from legit source
    - tries to trick user into giving private info
    - emails & fake websites difficult to distinguish from those that are legit
- variations on phishing attacks
    - __spear phishing__ - targets specific users
    - __whaling__ - targets "big fish"
    - __vishing__ - use call instead of emails
- about 97% of all attacks start with phishing

__Spam__
- unsolicited email
    - primary vehicles for distribution of malwares
    - sending spam is a lucrative business
        - costs spammers very little to send millions of spam messages
- filters look for specific words & block email
- __image spam__ - use graphical images of text to circumvent text-based filters
    - often contains nonsense text so appears legit

__Hoaxes__
- false warninng, usually claiming to come from IT department
- attackers try to get victims to change config settings on their pc that will allow attacker to compromise system
- attackers may also provide telephone number for victim to call for help, which will put them in direct contact with attacker

__Watering Hole Attack__
- malicious attack directed towards small group of specific individuals who visit same website
- Eg.
    - major executives working for manufacturing company may visit common website, such as parts supplier to manufacturer

### Physical Procedures
__Dumpster Diving__
- digging through trash for useful info
- electronic variation - google search for documents & data online
    - called __google dorking__

__Tailgating__
- follow behind authorised individual through access door
    - employee could conspire with unauthorised person to allow him to walk in with him (called __piggybacking__)
    - watching authorised user enter security code on keypad - __shoulder surfing__


Chapter Summary
---
![](https://i.imgur.com/5ORGqqG.png)
![](https://i.imgur.com/aesAUVs.png)



###### tags: `ISEC` `DISM` `School` `Notes`