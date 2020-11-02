

Lecture 03 Footprinting
===




## Table of Contents

- [Lecture 03 Footprinting](#lecture-03-footprinting)
  * [Table of Contents](#table-of-contents)
  * [Penetration Testing](#penetration-testing)
      - [Stages](#stages)
    + [Footprinting](#footprinting)
      - [Info to Find](#info-to-find)
  * [Web Tools](#web-tools)
    + [Advanced Web Searches](#advanced-web-searches)
    + [Whois](#whois)
    + [Using Email](#using-email)
    + [Analyse Company's Website](#analyse-company-s-website)
    + [Find Info about Connected Devices](#find-info-about-connected-devices)
    + [Use Domain Name Service (DNS)](#use-domain-name-service--dns-)
      - [Other DNS Whois Tools](#other-dns-whois-tools)
    + [Traceroute](#traceroute)
    + [Analyse Company's Website](#analyse-company-s-website-1)
      - [Paros](#paros)
    + [Copy Whole Websites](#copy-whole-websites)
  * [Using HTTP Basics](#using-http-basics)
    + [HTTP Headers](#http-headers)
    + [Detecting Cookies & Web Bugs](#detecting-cookies---web-bugs)
  * [Social Engineering](#social-engineering)
    + [Techniques](#techniques)
    + [Shoulder Surf](#shoulder-surf)
    + [Dumpster Diving](#dumpster-diving)
    + [Piggybacking](#piggybacking)
    + [Phishing](#phishing)
  * [View Email Headers](#view-email-headers)
    + [Info to look out for](#info-to-look-out-for)
  * [Summary](#summary)



Penetration Testing
---
#### Stages
![](https://i.imgur.com/KXAdMLa.png)

### Footprinting
- footprinting
    - discover info abt org/network
    - usually avail on internet
    - info gathered can be used to conduct security test
        - or determine attack vectors
    - example info
        - size of network
        - OS used
- info gathering
    - many res to find info legally
    - identify methods to find info abt orgs
    - companies can try to limit the amt of info avail publicly

#### Info to Find
- domains
    - how many registered domains
- principle service
    - what main internet services provided
        - test for port 21, 22, 25, 80, 443
- IP addr discovered
    - dig up all systems & scope
- gateway routers
    - who ISP
    - whr hosting DMZ in-house
        - how big
- visible systems
    - estimate based on what we can see is alive
- primary OS by IP
- firewalls
    - scan tcp 135-139
- IDS/IPS
    - can teack us?
    - will kill our conns?
- web techs
    - slow past of testing
- ISPs
    - name, addr, website, info on hosting
- test conditions
    - hops
    - restrictions
        - Eg. internet weather

Web Tools
---
![](https://i.imgur.com/gEQrByr.png)

### Advanced Web Searches
- Eg.
    - find certain word/file on website
        - `site:www.example.com keyword`
    - find file types with keywords
        - `filetype:type site:www.example.com keyword`
    - find webpages with certain string in URL
        - `inurl:string site:www.example.com`
    - find webpages with certain string anywhr in txt
        - `intext:string site:www.example.com`
- http://www.googleguide.com/advanced_operators_reference.html

### Whois
- domain names registered with network info centre (NIC)
- regional internet registries handle IP allocation
    - american registry for internet nums (ARIN)
    - asia-pacific network info centre (APNIC)
- whois db allow queries on who owns domains, contact info, IP range etc.

### Using Email
- find email format
    - guess other employee email accs
- bounce email using non-existent acc
    - read mail header
    - get info abt servers
- tool to find corporate employee info
    - Groups.google.com

### Analyse Company's Website
- webpages have a lot of info
    - preferred web tehc, type of OS, webserver etc.
- simplest tool is browser
- view source
    - sometimes useful info can be found in comments

![](https://i.imgur.com/XJ59hd1.png)

### Find Info about Connected Devices
- shodan
    - www.shodan.io
    - search engine for online devices

![](https://i.imgur.com/2EywjEr.png)


### Use Domain Name Service (DNS)
- dns
    - resolve hostnames to IP
    - people prefer URL to IP
    - can be vuln
- dns query tools
    - nslookip
    - dig
    - host
    - whois
- determine company's primary DNS server
    - look for __start of authority (SOA)__ record
    - show zones/IP
- __zone transfer__
    - enable you to see all hosts on network
    - gives you org's network diagram

#### Other DNS Whois Tools
- www.whois.net
- greenwich
- wikto
- smartwhois
- activewhois
- spiderfoot
- www.dnsstuff.come
- www.mxtoolbox.com

### Traceroute
- why traceroute?
    - can use to discover alt ISPs use for disaster recovery
    - use ICMP (windows) or UDP (linux)
    - TTL vals used to trace route
    - perform traceroute from diff countries
        - use online traceroute tool

### Analyse Company's Website
- other advanced tools (proxy)
    - paros
    - webscarab
    - burpsuite
- dev tools on browser
    - press f12

#### Paros
- search for website
    - tools > spider
    - enter website's url
    - check results

![](https://i.imgur.com/BB06OkM.png)
![](https://i.imgur.com/fsSCvV0.png)

- get structure of website
    - tree > scan all
    - report includes
        - vulns & risk lvls
        - web server ver
    - gathering info takes time

![](https://i.imgur.com/XAqKWJA.png)


### Copy Whole Websites
- pages of website inspected & analysed offline
    - HTTrack Website Copier
        - www.httrack.com


Using HTTP Basics
---
- port 80
- use HTTP lang to pull info from web server
- basic understanding of HTTP beneficial for security testers
- return codes
    - reveal info abt system

![](https://i.imgur.com/GPtb4Xa.png)

- HTTP methods
    - `GET / HTTP/1.1` is most basic method
    - can determine info abt server OS from server's generated output

![](https://i.imgur.com/7C7BBAe.png)
![](https://i.imgur.com/455Mnan.png)
![](https://i.imgur.com/1bC9Qp3.png)

### HTTP Headers
- every HTTP packet (resp/req) contains set of header fields
- may contain info on
    - browser of client
    - OS of client
    - web server turning response
    - cookies
- other methods of gathering info
    - cookies
    - web bugs


### Detecting Cookies & Web Bugs
- cookie
    - txt file generated by web server
    - stored on user's browser
    - info sent back to web server when user returns
    - used to customise webpages
    - some cookies store personal info
        - security issue
- web bug
    - 1 px x 1px img file
    - referenced in IMG tag
    - usually works with cookie
    - purpose similar to spyware & adware
    - comes from 3rd pt companies specialising in data collection



Social Engineering
---
- use human nature to get info
- biggest security threat to networks
- most difficult to protect against

### Techniques
- urgency
- help with probs
- everyone else doing it
- kindness & charm
- authority

### Shoulder Surf
- stand behind people and see info entered
    - use camera phones to take vids

### Dumpster Diving
- lots of valuable info in trash
    - discarded windows XP manuals - company just upgraded windows OS
    - company organisational charts
    - printouts of emails
    - discarded hard disks, USB drives
        - deleted data can be retrieved
- docs shld be shredded
- use disk-cleaning software to wipe all data on discarded disks

### Piggybacking
- trailing authorised staff closely to enter restricted areas
- may rely on kindness of people to hold door for them while wearing fake staff card
    - or carrying big boxes

### Phishing
- urgent emails that seem to be from legit companies asking you to click on link to provide/update details
    - link leads to atker's website
- spear phishing
    - sent to specific people in org

- not limited to emails, can occur in mobile msgs too
    - phishing sms



View Email Headers
---
- learn to find email headers
    - after opening email headers, copy paste into txt doc to read them from txt editor
- headers contain valuable info abt sender
    - unique identifying numbers, IP addr of sending server & sending time
- [Learn more abt email headers](https://www.arclab.com/en/kb/email/how-to-read-and-analyze-the-email-header-fields-spf-dkim.html)

### Info to look out for
- info to look out for
    - return path
    - recipient email addr
    - type of email sending service
    - ip addr of sending server
    - name of email server
    - unique msging num
    - date & time email sent
    - attachment files info
- use who is or other db to find true source of email


Summary
---
![](https://i.imgur.com/KMtH4Y9.png)





###### tags: `EHD` `DISM` `School` `Notes`