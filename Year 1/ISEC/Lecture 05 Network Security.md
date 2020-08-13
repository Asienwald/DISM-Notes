---
title: 'Lecture 05 Network Security'
disqus: hackmd
---

:::info
ST1004 Infocomm Security
:::

Lecture 05 Network Security
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

Networking-Based Attacks
---
- relies on network
- grped into
    - interception
    - poisoning

Interception Attacks
---
- designed to intercept net comms

### Man-in-the-Middle (MITM)
- MITM atk
    - interception of legit comm & forging fictitious resp to sender
    - 2 comps sending & receiving data with comp between
- can occur between 2 users
    - however many mitm atks between user & server

![](https://i.imgur.com/l8pAoy0.png)

### Man-in-the-Browser (MITB)
- intercepts comm between parties to steal/manipulate data
    - occur between browser & comp
- usually begins with trojan infecting comp & installing extension into browser config
    - browser launched and ext activated
    - ext waits for specific webpage whr user enters private info 
    - when user clicks submit, ext captures all data from form fields
        - some can even modify data
- advantages
    - distributed through trojan browser ext - difficult to recognise that malicious code installed
    - infected MITB browser might remain dormant for months until triggered by user visiting targeted site
    - MITB software resides exclusively in browser hence difficult for standard anti-malware to detect

### Replay
- atker makes copy of transmission before sending to orig recipient
    - uses copy later
    - Eg. capture login credentials
- methods to prevent
    - both sides nego & create random key that's valid for limited time for specific process
    - use timestamps in all msgs & reject any msg that fall outside of norm window of time


Poisoning Attacks
---
- introducing substance that harms/destroys

### ARP Poisoning
- Address resolution protocol (arp)
    - if IP of device known but MAC not, sending comp send ARP packet to determine MAC
    - MAC stored in ARP cache for future ref
    - all comps that "hear" ARP reply also cache the data
- ARP poisoning
    - relises on MAC spoofing - imitating another comp by changing MAC

![](https://i.imgur.com/PRcsx7u.png)

### DNS Poisoning
- domain name system is current basis for name resolution to IP
    - DNS poisoning substitutes DNS addresses to redirect comp to another
- 2 locations
    - local host table
    - external DNS server

![](https://i.imgur.com/EvMCZ7Q.png)

### Privilege Escalation
- access rights
    - privileges to access hardware & software resources granted to users
- privilege escalation
    - exploiting software vuln to gain access to resources user normally would be restricted from accessing
- 2 types
    - vertical privilege esc - lower privilege user accesses funcs restricted to higher privilege users
    - horizontal privilege esc - user with restricted privilege accesses diff restricted funcs of similar user

Server Attacks
---
- compromised server can provide threat actors with its privileged contents/provide opening to atk ant device that accesses server

### Denial of Service (DoS)
- denial of service (dos)
    - deliberate attempt to prevent authorised users from accessing system by overwhelming it with requests
- most dos are __distributed denial of service__
    - use hundred/thousands of devices flooding server with requests

#### Smurf Attack
- atker broadcasts net requests to all comps on network but changes address whr req came from
    - AKA __IP Spoofing_-
- appears as if victim pc askinf for resp 
- all comps send resp to victim so its overwhelmed

#### DNS amplification atk
- flood victim by redirecting valid resp to it
- use publicly accessible & open DNS servers to flood system with DNS resp traffic

#### SYS flood atk
- take advantage of procedures for initiating session
- in syn flood against server
    - atker send SYN segments in IP packets to server
    - atker modifies src address of ea packet to comp addresses that don't exist/cannot be reached

![](https://i.imgur.com/7gtqOS3.png)


### Web Server Application Attacks
- securing web apps more difficult than protecting systems


#### Zero-day Attack
- atk that exploits previously unknown vulns, victims dont have time to prepare/defend against atk
- traditional network security devices can block trad net atks but cannot always block web app atks
    - many networks sec devices ignore content of HTTP traffic
- several diff web app atks target input from users & grped into 2 cats
    - cross-site atks
    - injection atks

#### Cross-site scripting (XSS) Attack
- threat actor takes advantage of web apps that accepts user input w/o validating before presenting to user
- when victims visit injected website
    - malicious instruction sent to victim's browser
- some XSS atks designed to steal info
    - retained by browser when visiting specific sites
- XSS atk requires website to meet 2 criteria
    - accepts user input w/o validating 
    - uses input in resp

#### Cross-site request forgery (XSRF)
- uses browser settings to impersonate user
- if user currently authenticated on site & tricked into loading another webpage
    - new page inherits identity & privileges of victim to perform undesired func on atker's behalf

#### Injection Attack
- introduce new input to exploit vuln
- 1 of most common injection atks called __SQL injection__ inserts statement to manipulate database server
- SQL (structred query language)
    - used to view & manipulate data stored in relational database
- forgotten password example
    - atker enters ficitious email address that included single quotation mark as part of data
    - resp lets atker know whether input is validated
    - atker resends email field in SQL statement
    - statement processed by database
    - example statement
        - SELECT fieldlist FROM table WHERE field = 'whatever' or 'a'='a'
    - result - all user email addresses displayed

![](https://i.imgur.com/f4X0wPM.png)

### Hijacking Attacks
- several server atks are result of threat actors "commandeering" tech then using it for atk
#### Session hijacking
- atker attempts to impersonate user by stealing/guessing session token
- session token - random string assigned to an interaction between user & web app
- atker can attempt to obtain session token
    - by using XSS or other atks to steal session token cookie from victim's comp
    - eavesdropping on transmission
    - guessing session token

#### URL hijacking
- AKA __typo squatting__
- users directed to fake look-alike site filled with ads whr atker receives money for traffic generated to site
    - atkers purchase the domain names of sites spelled similarly to actual sites
- threats actors also registering domain names that are one bit diff
    - __bitsquatting__

#### Domain hijacking
- domain pointer that links domain name to specific web server changed by threat actor
- when domain hijacked,
    - threat actor gains access to domain control panel & redirects registered domain to diff phy web server

#### Clickjacking
- hijacking mouse click
    - user tricked to click link that's not what it appears to be
- relies upon threat actors who craft zero-pixel IFrame
    - iframe (AKa inline frame) is HTML element that allows embedding another HTML doc inside main doc
    - 0-pixel ifrma eis virtual invisible to naked eye

### Overflow Attacks
- designed to "overflow" areas of memory with instructions from atker

#### Buffer overflow
- process attempts to store data in RAM beyond boundaries of fixed-length storage buffer
    - extra data overflows into adjacent memory locations
- atker can overflow buffer with new address pointing to atker's malware code

![](https://i.imgur.com/8jkUu4O.png)

#### Integer overflow
- condition that occurs when result of arithmetic operation exceeds max size of int type used to store it
- in an int overflow atk
    - atker changes value of var to sth outside range programmer had intended using int overflow
- can be used when
    - atker can use int overflow to create buffer overflow situation
    - program that calculates total cost of items purchased will use num sold times cost per unit
        - if int overflow introduced, can result in negative value & resulting negative total cost
    - large positive value in bank transfer can be wrapped around by int overflow atk to become negative value
        - can reverse flow of money

### Advertising Attacks
- several attempts to use ads/manipulate advertising system

#### Malvertising
- threat actors use 3rd pt advertising networks to distribute malware to unsuspecting users who visit well-known site
    - AKA malvertising or __poisoned ad attack__
- ad that contains malware redirects trojans & ransomware onto user's comp
- preventing malvertising difficult
    - website operators unaware of types of ads being displayed
    - users have false sense of security going to mainstream site
    - turning off ads that supports plugins (Eg. adobe flash) often disrupts web experience
#### Ad fraud
- threat actors manipulate pre-roll ads to earn ad revenue directed to them
- create "robo-browser" called __Methbot__
    - spoofs all necessary interacted needed to initiate, carry out & complete ad auctions

### Browser Vulnerabilities
- browser additions introduced vulns in browsers that access servers

#### Scripting code
- adding dynamic content
    - web server downloads "script"/series of instructions in form of comp code that commands browser to perform specific action
- JS most popular scripting code
    - JS embedded inside HTML
- there are diff def mechanisms intended to prevent JS programs from causing harm
- however, security concerns
    - malicious JS program can capture & remotely trasmit user info w/o user's knowledge/authorisation

#### Extensions
- expand normal capabilities of browser
- most written in JS
    - so browser can support dynamic actions
- browser dependent
    - ext that works on chrome cannot func in edge

#### Plug-ins
- adds new functionality to browser so users can play music, view vids or display special graphical images
- single plugin can be used on diff browsers
- 1 common plugin supports Java
    - java can be used to create separate program called __Java applet__
- most widely used plugins for browsers
    - java, adobe flash player, apple quicktime & adobe acrobat reader

![](https://i.imgur.com/BBAQpTr.png)

#### Add-ons
- add greater degree of func to browser
- can do
    - create more browser toolbars
    - change browser menus
    - be aware of tabs open in same browser
    - process content of every webpage loaded
- due to risks
    - effort made to minimise
    - some browsers block plugins
    - HTML5 standardises sound & vid formats so plugins not needed

![](https://i.imgur.com/YzrukDa.png)

Chapter Summary
---
![](https://i.imgur.com/Ra6FWse.png)
![](https://i.imgur.com/VOoBSr6.png)




###### tags: `ISEC SEM 2` `DISM SEM 2` `School` `Notes`