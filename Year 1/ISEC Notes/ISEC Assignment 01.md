---
title: 'ISEC Assignment 01'
disqus: hackmd
---

:::info
ST1004 Infocomm Security
:::

ISEC Assignment 01 WannaCry
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

Overview
---
- set of powerpoint slides on WannaCry + presentation in week 15
    - presentation 10mins including QnA
- deliverables
    - what security breach it was
        - what kind of malware attack
        - what kind of hacking done
    - what damage it cost to org/party being attacked
    - what was done to repair the damage
    - lesson learnt & what could have been done to prevent it in the 1st place
    - other interesting facts

### Slides
> slide theme
> https://docs.google.com/presentation/d/1EUmhKBCuppzeu5THbH_zcp5qyPMXQlXet5X_3mOIwj0/edit?usp=sharing

Report
---
### What security breach it was
- wannacry is a ransomware worm that encrypts user files before demanding a fee of $300 or $600 worth of bitcoins
- consists of multiple components
    - __dropper__ - contains encryptor as an embedded resource
        - self-contained program that extracts the other components embedded within itself
    - __encryptor__ - contains decryption app ("Wana Decrypt0r 2.0"), password-protected zip containing a copy of Tor, and other files with config info & keys
    - __decryptor__
- once launched, wannacry tries to access a hard-coded URL (AKA kill switch)
    - if can't, it searches & encrypts files of important formats
        - Eg. Office to MP3s
    - it then displays a ransom notice demanding $300 in bitcoin


#### How does it infect PCs?
- exploits Server Message Block (SMB) protocol
    - SMB helps various nodes on a network communicate & was used to spread the worm by executing arbitrary code
    - this vuln thrives in Windows XP or earlier OSes
        - Microsoft ended official support for XP in 2014
    - US National Security Agency discovered this vulnerability and rather than reportig it to the infosec community, they developed code to exploit it called __EternalBlue__
        - exploit stolen by hacking group __Shadow Brokers__ who realised it in a post on April 8 2017
        - Microsoft discovered the vuln a month later & released a patch
- once pc infected, wannacry first tries to access an unregistered domain - AKA the kill switch
    - if it can't connect, it infects
    - if connects, it stops the attack
    - a security researcher who goes by the name __MalwareTech__ activated the kill switch by registering the domain & posting a page on it
        - helped stop the spread of the ransomware
    - why did they do it?
        - security researchers run malware in sandbox environment - any URL or address will appear reachable
            - hoped to ensure malware won't activate for researchers to watch (?)
            - in many malware sandboxes, any Internet request, whether to a registered domain or not, will give a response, thus indicating to the malware that it is being analysed.

### What damage it cost to parties involved
- The number of infected system had grown from 45,000 to 200,000 over the weekend acrosss 150 countries. 
    - It varies from National Health Service in Uk to Automobile factories in Spain as well as Telecommunications Company in Spain and Russia's second Mobile Operator.
- It locked out 16 NHS Hospitals' computer systems

    - Ambulances were reportedly reruoted, leaving people in critical need
    - It also restricted the delivery of many services in the UK
    - 19,000 appointments were canceled due to the attack.
    - up to 70,000 devices were also affected (MRI scanners, Blood-Storage Refridgerator)


- Perpetrators demanded $300 bitcoins and subsequently increasing to $600 worth of bitcoins.
    - even if ransom has been made the attackers had no way of identifying the payment with a specific victim’s computer.


-  The impact is considered relatively low as compared to other potential attacks of the identical type
    -  It could have been disastrous if the kill switch was not discovered
    -  it could have specifically targeted highly sensitive infrastructure, nuclear power plants, railway systems

### What was done to repair the damages
- Microsoft released out-of-band security updates for obsolete products such as Windows Server 2003 and Window XP .
    - it saved many aging systems from Wannacry infection  
-   Kill switch was discovered to prevent infection from spreading
    -   MalwareTech reversed engineered samples of Wannacry
    -   He discovered that he could activate the kill switch by registering the domain 
    -   Seeing the domain was unregistered and inactive, the query has no effect on Wannacry's spread
    - However, once the ransomware checked the url and found it active, it shut down.
### Lesson learnt & what could have been done to prevent it
- one reason why WannaCry spread so quickly was because despite finding out about a new 0-day vuln, the US NSA did not report it and instead created an exploit that WannaCry used to exploit PCs and launch the attacks
- WannaCry exploited a vuln in outdated Windows XP or earlier which Microsoft ended support for in 2014
    - patch to prevent WannaCry actually available before the attack began
        - Microsoft Bulletin MS17-010 released on March 14th 2017
    - However, despite flagging as critical, many systems were still unpatched as of May 2017 when Wannacry hit

#### Lesson Learnt
- it is important to keep your workstations up to date and patch it whenever a new patch is out to receive the latest security updates
- never ever use an outdated OS
- always report a vuln to the relevant officials immediately so a patch can be released for it as soon as possible

#### What could have been done
- regularly patch computers and update your OS to receive latest security updates
    - also configure your firewalls to block unnecessary traffic
    - disable unused ports or services on workstations
- release a patch for the 0-day vuln as soon as it was found before releasing it to the public and not create an exploit for it instead

### Interesting facts
- hackers only made $50,000 even though it spread to over 200000 PCs in 150 countries and caused worldwide panic
- Britain's National Health System was among the biggest victims as many of it's computers still run Windows XP
- New versions of Wannacry appeared after the kill switch code was removed
    - caused a second wave

Script
---
Hello I’m Kar wei and this is Yu Ran and today we’ll be talking about the infamous ransomware attack, Wannacry.


In May 2017, a worldwide ransomware attack that specifically targeted Windows systems was launched.

This attack was called the Wannacry Ransomware attack and it cost many organisations millions of dollars worth in damages.


So, what exactly is Wannacry?

Wannacry is a ransomware worm that spreads between victims, encrypting their files and data before demanding a fee of around $300 to $600 worth of bitcoins.

Wanncry consists of 3 main components,
The encryptor & decryptor, to encrypt or decrypt files once the ransom has been paid,
Files containing encryption keys
And a copy of Tor to access a domain which will be covered later.


So, how does it affect computers?

Firstly, wannacry infects computers through a vulnerability in the Server Message Block protocol in Windows systems.

The SMB protocol is known as a network communication protocol for providing shared access to files, printers, and serial ports between nodes on a network.

It was exploited and used to spread the worm by allowing users to execute arbitrary code through the vulnerability.

This vulnerability was only found in Windows XP or earlier versions, with official support for XP ending in 2014.


Next, Wannacry then tries to access an unregistered domain, which is also known as the Kill Switch.

If it connects to the domain, wanancry stops all actions and remains dormant.
If it can’t connect to the domain, wannacry continues on with its infection.

The reason why it’s called a kill switch is that it allowed a security researcher known a MalwareTech to activate the kill switch by registering the domain wannacry connects to hence deactivating any future attempts to infect computers and stopping the spread of the ransomware worm.

There are many speculations as to why this kill switch was implemented, but it is believed to be an indicator if its being analysed by security researchers or not.

This is because in many malware sandboxes, any Internet request, whether to a registered domain or not, will give a response, thus indicating to the malware that it is being analysed and stop all further actions


Finally if the domain doesn’t connect, Wannacry continues on with its infection and searches & encrypts any important files found on the victim’s computer like documents or music MP3s.

After this is done, the computer has been successfully infected and displays a ransomware notice demanding $300 to $600 in bitcoins from its victim.
Once paid, it decrypts all encrypted data and returns the data to its victims.


Now I'll pass on to Yu Ran who will elaborate more on the damages and post attack repairs


(Yu Ran talks)


Now we'll explain the cause of wannacry.


The vulnerability was actually initially discovered by the US National Security Agency but rather than reporting the vulnerability to Microsoft, they developed an exploit for it called EternalBlue.

On 8th April 2017, a group called Shadow Brokers stole this exploit and released it publicly, and was later used in Wannacry and caused its swift spread.


Furthermore, 
A patch for the vulnerability was actually released on March 14th 2017, about a month before the Wannacry attack but many users did not patch their computers and remained vulnerable to the attack

Many users also continued using Windows XP even though Microsoft had ended official support for it 3 years before the attack, one such example is NHS which suffered huge damages because of it as XP was the sole target of Wannacry

After the 1st wave, a second wave was launched with a different kill switch.
However, the domain in connected to was registered around 10 hours later hence halting the attack but nevertheless more computers were still infected.


So, what could have been done to prevent this disastrous attack?

Firstly, do not use outdated OSs like Windows XP for your workstations.
Use the latest ones like Windows 10 that receives regular updates.

Secondly, always configure your computer’s security settings like setting up your firewall, disabling unused ports, unnecessary user accounts etc.
If possible, get experienced security personnel to do it for you.

Thirdly, do not click any malicious links or run unknown softwares, especially in phishing attacks as visiting these links might result in a virus getting downloaded into your computer unknowingly.

Lastly, if you ever find a vulnerability, always document it and report it as fast as possible to the relevant authorities so it can be patched asap and DO NOT create an exploit for it or publicise the vulnerability!


In conclusion, 

1. Report vulnerabilities asap
2. Always keep your computer systems up-to-date
3. Install any patches released asap



Resources
---
- https://www.csoonline.com/article/3227906/what-is-wannacry-ransomware-how-does-it-infect-and-who-was-responsible.html
- https://www.siliconrepublic.com/enterprise/wannacry-impact-organisations-attack
- https://help4it.co.uk/done-prevent-wannacry-ransomware-attack-nhs/
- https://utgsolutions.com/15-important-facts-about-wannacry-ransomware-virus-infographic/
- https://logrhythm.com/blog/a-technical-analysis-of-wannacry-ransomware/
- https://www.kaspersky.com/resource-center/threats/ransomware-wannacry

### Slides Themes
- https://slidesgo.com/recent


###### tags: `ISEC SEM 2` `DISM SEM 2` `School` `Notes`