---
title: 'ACG CA2'
disqus: hackmd
---

:::info
ST2504 Applied Cryptography
:::

ACG CA2 Assignment 2
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
:::danger
__Due date (proposal):__ 9 Feb 2020 (Sun) 11pm
__Due date (code):__ 16 Feb 2020 11pm
:::

- write proposal (report)
- write implementation (code package)
- group interview

### Task
- developed SPAM2, SP set up more AP using public wifi around
    - tasked to enhance the design & impementation to provide needed security with enhancement features
- menu-of-the-day info only need integrity protection
    - day-closing info need confidentiality and non-repudiation protection
- tasked to
    - conduct security risk assessment
    - proposal to overcome security risks identified
    - implement solution
    - arrange demo

### Assessment Criteria
![](https://i.imgur.com/9Yg15Qj.png)


Deliverables
---
### Risk Assessment
- only for confidentiality, integrity and non-repudiation of data stored & exchanged with consideration on deployment of software
- considerations

![](https://i.imgur.com/Kevi8pM.png)

- risk matrix

![](https://i.imgur.com/6iT55wp.png)

- risk response techniques

![](https://i.imgur.com/l0VvEu1.png)


- complete the risk assessment form & attach as appendix of proposal
    - do tgt

- more info
    - https://www.synopsys.com/blogs/software-security/software-risk-analysis

### Proposal
- 10 pages including appendices
    - single line spacing
    - 12 pt focus
- proper report structure
    - cover page
        - module name & code
        - course & class
        - name of students
    - content page
    - introduction
    - background
    - appendices
- outline
    - illustrate current SPAM2 system & implementation
        - Eg. connected via wireless@sg
    - describe assumptions on implementation
    - describe various attack scenarios
        - propose countermeasures with justification
    - make reasonable assumptions on motivation & capability of attackers
    - make reasonable assumptions on potential impact
    - illustrate proposed system
    - highlight new features with their roles in data protection
- conclusion & additional considerations
- planned task allocation
- individual reflection
- references
    - quote ref
    - acknowledge source
- appendix
    - risk assessment form

### Individual Contributions
- indicate using comments in python code
- list work done by ea member in contributions.txt

### Submission Checklist
![](https://i.imgur.com/Xe9WYIq.png)


Task Allocation
---
### Security Implementations
- encrypt using TLS
    - jess
- RSA public-private key exchange
    - digital certificates
    - certificate authority and wtv
    - jess
- rate limiting
    - kw
- restricting payload
    - kw
- authentication
    - client
    - server
        - certificates
    - jess
- create standards for our data packets
    - kw
- GUI (least priority)
    - see first

### Proposal
- kw
    - risk assessment form
    - intro 
    - background
    - ![](https://i.imgur.com/NSzYmjh.png)

- jess
    - ![](https://i.imgur.com/jTUujpd.png)
    - ![](https://i.imgur.com/Rij86gl.png)
    - conclusion & additional considerations


### Code
- kw
- jess



Our Report
---
### Risks Found
- everything is transmitted in plaintext
    - server sent message `Menu\n---\n1 Sweet popcorn\n2 Salty popcorn` to client and it can be viewed from wireshark in plaintext

![](https://i.imgur.com/45HAm6z.png)
![](https://i.imgur.com/3ppFDPx.png)
![](https://i.imgur.com/vvtCzwf.png)

- no authentication required
    - anyone who connected to the websocket can receive the same data
- No way to authenticate whether the food menu is actually from the server or not
    - data sent to client might be malicious or wrong information

- see google docs


### Code to Implement
#### Security Measures
- authentication when connecting to websocket
    - or authenticate before even establishing websocket session
- tls
    - secure the connection between client and server so atkers cannot intercept
- rsa
    - encrypt data send between client and server
- signature
    - hmac/mac?????(if you dw do i do this part)
- refer to bible at the end 

#### Interfaces
- make the interfaces a lot better looking
- make nicer terminal
    - if have time do GUI for server & client


Resources
---
- [Our Bible](https://www.freecodecamp.org/news/how-to-secure-your-websocket-connections-d0be0996c556/)
- [Bible num 2](https://devcenter.heroku.com/articles/websocket-security)



###### tags: `ACG SEM 2` `DISM SEM 2` `School` `Notes`