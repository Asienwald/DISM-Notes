---
title: 'ACG Assignment Outline'
disqus: hackmd
---

:::info
ST2504 Applied Crypto
:::

ACG Assignment 1 Week 4 Outline
===

> https://www.voicery.com/
> For natural, realistic voices

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

Presentation Flow
---
### Introduction - 5 min
- in form of video
> https://www.bbc.com/news/technology-46746592
> [name=Pewdiepie]
> https://www.secplicity.org/2018/04/27/the-fish-tank-casino-heist-daily-security-byte/
> [name=Fish Tank]

- introduction of IoT
    - what is IoT
    - where isit used today?
    - why is IoT security important?

### Act 1 - 2 min
- router suddenly says that the email has been succesfully sent
    - everyone confused, nobody sent any email
    - claims alexa ordered the email to be sent
- someone had intercepted the network and sent an email
    - due to unencrypted data transferring protocols used and sending login credentials such as username and password in plaintext
- go into educating about secure protocols and strong hashed passwords

[Slides 1] - 10 min

### Act 2 - 2 min
- go into more security related topics
    - custom firmware and signatures

[Slides 2] - 10 min

### Act 3 Conclude the skit - 1 min
- Alexa boi has learnt many thing and will make sure they never get attacked again
- Alexa gives a very convienent summary on what we covered
    - TLS/Encrypted Tunnels
    - Data/Origin Verification
    - Hashing Passwords
    - Password Security
    - Firmware verification

### Kahoot Quiz - 5 min

### QnA - 5 min

Total = 40min
---


Characters
---
- __Alexa__
    - small boy, dumb
- __smart tv (Sony)__
    - mum of group
- Jess
- Jia Wei
- Yu Ran
- Class
    - everyone else


Script
---
### Introduction
- [x] __Kar Wei__: (introduce the characters and overall gist of the skit)
- [x] __shows news report on Fishtank device attack on casino__
- [x] __Sony__: that's horrible, I sure hope I don't fall victim to that ever!
- [x] __Jess__: That's what you get for not securing your IoT devices!
- [x] __Alexa, dumbly__: Jess, what are IoT devices? 
- [x] __Jess__: That's a good question, class do you know?
    - class answers
- [x] __Jia Wei (slide 4)__: That's right! IoT devices are very useful forms of technology that help to make our lives easier and more convienent! They are essentially a piece of hardware with a sensor, like a microphone or camera, that transmits captured data from one place to another over the Internet, to process or to log data. Due to being **so** useful, they have since rapidly spread around the world and some of you might not realise that they're around you!  From smart home devices like Google Home, Alexa (That's you!), Thermostats and Philips Hue lightbulbs, to security devices such as NEST Home security cameras and door locks.
- [x] __Yu Ran (slide 5)__: (explain the background of IoT now)
    - The Internet of Things consists of any devices with a switch connected to the internet. The IoT comprise of an extensive network of internet connected to the things and devices. Also, it provides businesses and people better insight into and control over the 99% of objects and environments that remain beyond the reach of the internet. Hence, IoT allows them to be more connected to the word around them improving your ways of working. Such as Smart City[Smart Lighting, Smart Parking, Smart Mobility ]
    - how widespread IoT is in today's society?
- [x] __Sony__: So what does this have to do with us?
- [x] __Jess (slide 6)__: (explain the possible impacts of compromised IoT security)
    - If the security of IoT is compromised, attackers will have access to sensitive data stored inside the device such as email accounts,passwords,credit card credentials and more! Also, attackers can also inject malicious commands into the device to do things such as record the surroundings, pay stuff for them etc.
- [x] __Alexa and Sony__: Oh No! I sure wouldn't want to be the victim of that!
- [x] __Sony__: How do we protect ourselves against these attacks?
- [x] __Jia Wei__: Don't worry, we'll teach you all you need to know on IoT security!
- __Start Act 1__

### Act 1
- [x] __Alexa__: Cool, so when do we start? By the way, I sent the email you told me to, Yu Ran
- [x] __Yu Ran__: Huh, what email?
- [x] __Alexa__: didn't you ask me to send an email regarding the project you guys are working on? 
- [x] __Jia Wei__: Huh, what project? There's no such thing!
- [x] __Sony__: If none of you asked to send it, then who did?
- [x] __Jess__: Someone must have intercepted our network traffic and sent that phony email! Alexa, do you encrypt the data you transmit?
- [x] __Alexa__: What are you talking about?
- [x] __Jess (slide 7)__: When you transmit data, you have to send data through encrypted protocols such as HTTPS to ensure hackers can't just intercept the network traffic and get the data you are sending. Also, ensure that you authenticate the data transmitted to you via TLS where you check the digital certificate sent by the server to ensure the server is legitamate and not a unknown server which is likely by a hacker with malicious intentions. 
- [x] __Jia wei (slide 8)__: Another way IoT devices are commonly hacked are when people do not change their default password, so potential hackers can just do a Google search and gain access to the device, such as a IP camera or a router. Hence, you should change the default password and hash it using algorithms such as SHA-512 Using a hashed password means that if hackers somehow get the file containing the password, they cannot just read the password off the file and gain access. 
- [x] __Yuran (slide 9)__: Lastly, ensure your password is both long and complex so hackers cannot use dictionary attacks or rainbow tables to break through the encryption. 
- [x] __Jia Wei__: What are some bad password examples you can think of?
    - class answers
- [x] __Yuran__: Those are all valid examples! Simple passwords such as password123 or qwerty are really bad passwords The best passwords are easy to remember and hard for hackers to crack.
- [x] __Jia Wei__: The 3 essential rules to follow when creating a password is that they must have at least 12 characters, include numbers, symbols, capital and lowercase letters, and isn't a combination of dictionary words.
- [x] __Jia Wei__: Earlier Yuran mentioned about dictionary attacks and and rainbow tables, and i would like to briefly explain what they are.
    - [x] A dictionary attack is a straightforward example of a brute force attack, that has a computer generate a random combination of words from a dictionary, hashes it, then compares it to the hashed password you want to crack.if they match, then the password is cracked. This form of attack is very resource intensive as the computer has to generate the password, hash and compare it.
    - [x] A rainbow table however, is a more efficient way to crack passwords. A rainbow table is a precomputed table of passwords and their hashes. It is a practical example of a time-memory trade off, as the passwords and their hashes are already compiled and computed convienently for you. A rainbow table attack also uses a neat thing called a hash chain and reduction algorithm (which i won't explain because its too complicated haha) to save space and make the process more efficient.
    - [x] So you might be thinking: "Oh no! All my passwords are now not secure!" But do not worry: there is a way to counter rainbow table attacks, which is salting. Salting is the process of generating a random salt value every time a password is needed to be stored. Then this salt value is added to the end of the password, and the password + salt is hashed. The hashed password and the salt value is then stored in the database. This ensures that even the same plaintext password will generate a different hash value.
    - [x] When the system needs to authenticate the user again, they take the user's password and adds the salt stored in the database, hashes and compares it.
    - [x] This effectively makes rainbow tables and dictionary attacks impractical as they would require a significatly larger table and hugely more computing time.
    - [x] However, this does not protect against simple passwords. So good password practices must still be followed. 
- [x] __Alexa__ (really dumbly): WOAHHHHHHH thats so cool!


### Act 2
- [xx] __Sony__: That was really educational! I feel so much secure now that I know how to defend myself! I shall go do that right now!
- [x] __Alexa__: Are there any other things we should take note of?
- [x] __Yu Ran (slide 10-11)__: Besides encrypted tunnels, the authentication and integrity of the firmware plays an important role in securing the IoT devices. Basically ensuring that the device operates only on authorised firmware. In order to certify both the integrity and authenticity of the information, [ensures that data is reliable and not modified] the signature of the firmware will be checked when the device boots up. This digital signature is computed by a cryptographic algorithm [Elliptic Curve Digital Signature Algorithm] to prevent hackers from copying it. So why is it important? Imagine if the signature can be easily spoofed, attackers can load firmwares onto the device and gain unauthorised access.
- [x] __Kar Wei (slide 12-16)__: (Explanation of RSA and Diffie-Hellman)


### Ending
- [x] __Sony__: Wow, thank you guys for teaching us this! This is such an eye opener! 
- [x] __Alexa__: Yeah! From the various attacks that hackers use, like packet sniffing and brute forcing, to using TLS to encrypt data while in transit over the network, using hashing functions like SHA-512 to hash passwords, password security, Data and Firmware Verification, I've learned many things today! I'll make sure to take your advice to heart and make sure that we never fall victim to such attacks again!
- [x] __Jia Wei__: We're glad that you all have learned something today! If you ever get the chance, you should share this information to other devices that you meet, so that they can also defend themselves from such attacks!
- [x] __Sony__: We will make sure to do that!

### Q&A
- Go Jek and class ask questions

### Kahoot
- ~15 minutes





###### tags: `ACG SEM 2` `DISM SEM 2` `School` `Notes`

