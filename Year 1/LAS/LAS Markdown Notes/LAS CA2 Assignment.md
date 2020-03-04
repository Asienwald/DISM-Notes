---
title: 'LAS CA2 Assignment'
disqus: hackmd
---

:::info
ST1412 Linux Administration & Security
:::

LAS CA2 Report
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


Overview
---
- design proof on concept (POC) system
- 2 main functions
    - enable public to browse through price list of products
    - enable authorised staff to upload/update price list content remotely

:::danger
__Due Date:__ 3rd Feb 2020 9pm
:::

### System Requirements
- price list system based on apache web server & Centos 7 system
- webpage is html based for simplicity & cost effectiveness
    - no need any db/app servers
- required to host 2 or 3 diff sample price list pages for POC purposes
- based on preference/design can use multiple (<=3) centos systems
- design & implement 5 security related features/measures to enhance system security


### Task
- report to describe & explain functional & security features 

![](https://i.imgur.com/X7CFKQg.png)

- individual reflection

![](https://i.imgur.com/SatYw0s.png)

- 15 minutes technical demo

![](https://i.imgur.com/li4gIPM.png)


### Marking Scheme
![](https://i.imgur.com/hoIA2Ws.png)



Our Report
---
### System Overview
- CentOS 7 virtual machine

#### Assumptions Made



### Network Design
![](https://i.imgur.com/ae7OgkA.png)


### List of required services & configurations

#### Services
- apache web server
- ssh for remote connection
- add more!

#### Configurations
- HTTPS
    - Use of TLS v1.2
    - /etc/httpd/conf.d/ssl.conf:
    - ![](https://i.imgur.com/aemWUE5.png)
    - Certificates + public and private keys
    - /etc/httpd/conf.d/ssl.conf:
    - ![](https://i.imgur.com/ITPfjiD.png)
    - If client attempts to connect via HTTP, they will be redirected to connect via HTTPS
    - /etc/httpd/conf.d/pancakes.conf:
    - ![](https://i.imgur.com/SOWxX0I.png)
    - https://www.digitalocean.com/community/tutorials/how-to-create-an-ssl-certificate-on-apache-for-centos-7
- Reverse proxy
    - domain name mapped to `www.reallygoodpancakes.com`
        - IP static to 172.16.108.45
    - Dummy computer used to port forward connections made via port 443 and 80 to the server at port 443 and 80 also
- Only main system services, firewalld, sshd and httpd are enabled on the server computer
- SSH
    - Cannot login as root
        - add line deny root into the sshd.conf 
    - Only can login as users in designer group
        - add line allow designer into the sshd.conf
    - /etc/ssh/sshd_config
    - ![](https://i.imgur.com/yNDHJdM.png)

- Firewall
    - Only allow system administrator (designer) to access the computer via ssh to edit the website
    - Only allow the reverse proxy computer to access the computer via https and http for it to send and receive information from the server to communicate to the clients
    - Block all other connections made to the server to prevent unauthorised access to the server
    - ![](https://i.imgur.com/nXOs55K.png)

    - Reverse proxy computer allows connection made via HTTP and HTTPS and forwards these connections via portforwarding to the server
    - ![](https://i.imgur.com/H49vDa3.png)


### Operation Procedures
- kw do

### List of security measures
- Use of https 
    - prevent hackers from intercepting the connection between the server and client
- Reverse proxy
    - By using a dummy computer to handle connections from clients instead of the actual server, it allows the server to stay hidden from the internet and hence reduces the ability of potential attackers gathering information of the actual server
- Firewall
    - Prevent unautorised computers from connecting to the server
- SSH
    - Allow system admins to edit the websites on the server remotely
- Shut down services that are not required
    - Reduce the number of vulnerabilities that attackers can use to attack the system
    


###### tags: `LAS SEM 2` `DISM SEM 2` `School` `Notes`