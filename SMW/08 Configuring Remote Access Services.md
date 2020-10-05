---
title: '08 Configuring Remote Access Services'
disqus: hackmd
---

:::info
ST2612 Secure Microsoft Windows
:::

08 Configuring Microsoft Windows
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

Introduction to Remote Access
---
- remote access service (RAS) role
    - enables remote access through 3 means
        - virtual priv networking
        - directaccess
        - web app proxy
- virtual priv network (VPN)
    - like tunnel through larger network that's restricted to designated member clients only
- related topics
    - directaccess
        - established 2 tunnels for connecting to direct access server used in remote access
        - transparent to users & always on
    - web app proxy
        - publishing apps so users external to org can access these apps on org's servers
- NOTE
    - many vendors providing vpn implementations
        - most production sites use firewalls/routers based vpn
            - Eg. SP using cisco anyconnect vpn; SoC using PaloAlto global protect vpn
    - microsoft servers provides few build-in vpn protocols via remote access services (RA) role

### Using Remote Access Protocols
- remote access protocols carries network packets over wan link
    - encapsulates packets like ip datagram so can be transmitted from 2 pts in wan
    - IP is most commonly used transport protocol
- many remote access protocols used by winserver2016 & its remote clients
    - early basic remote access protocol in use is PPP
- __point-to-point protocol (PPP)__
    - used in legacy remote comms involving modems
    - enables auth of conns & encryptions for network comms, but not considered as secure as modern options
    - can auto negotiate comms with several network comm layers at once
- when implementing winserver2016 vpn server, can choose 3/4 remote access tunneling protocols (4 built-in vpn protocol you can use to implement remote access in winserver)
    - pt to pt tunneling protocol
    - layer 2 tunneling protocol
    - secure socket tunneling protocol
    - ike v2 protocol
        - ipsec, tunnel mode, ikev2
        - ike v2 is newer ver of ipsec with more options in config
- NOTE
    - lan and wan uses diff medium, hardware devices, bandwidth and topologies so run on diff set of network protocols
    - remote access protocol needs to cater for lan to wan protocol conversions
        - to allow 2 remote parties to comm seamlessly as if both on same lan

#### Point-to-Point Tunneling Protocol (PPTP)
- offers PPP based auth techniques
- encryptes data carried by pptp through __Microsoft Pt to Pt Encryption (MPPE)__
- NOTE
    - PPTP is easiest to setup protocol, most network devices support it
        - but not good for setting up vpn channel that needs long/near permenant session

#### Layer 2 Tunnneling Protocol (L2TP)
- similar to PPTP
- use layer 2 forwarding that enables forwarding on basis of mac addressing
- uses ipsec for extra auth & data encryption
    - ipsec is set of ip based secure comms & encryption standards created through IETF

#### Secure Socket Tunneling Protocol (SSTP)
- employs PPP auth techniques
- encapsulates data packet in http through web comms
- uses ssl channel for secure comms
    - ssl is data encryption technique employed between server & client
    - ssl now evolved into transport layer security (TLS)
- more secure than PPTP or L2TP
- uses port 443 only to operate
    - hence most firewall friendly vpn protocol

#### Internet Key Exchange Version 2 Protocol (IKE v2)
- employs ipsec in tunnel mode protocol over udp port 500 & 4500
    - encapsulates datagrams using ipsec ESP or AH headers for transmission over network
- encryption
    - AES 256, 192, 128 & 3DES encryption algo
        - 3des not recommended
- pros
    - faster & extremely secured protocol
    - support mobility conns (Eg. MOBIKE)
        - Eg. remote clients are constantly moving
        - is the only built-in vpn protocol that supports this
    - more resilient to changing network connectivity
        - switch between access pts/wired to wireless conn
- cons
    - proprietary like sstp
        - but there's open source implementation
        - support by some network devices vendor

![](https://i.imgur.com/MusKGnV.png)
- these built-in vpn protocols can be implemented in RAS server concurrently
    - can config ras server to support remote client using any of the 4 vpn protocols to your site



Implementing Virtual Private Network
---
- vpns can use internet conn/internal network conn as transport medium to establish conn with vpn server
- vpn uses lan protocols and tunneling protocols
    - to encapsulate data as its sent across pub network like internet
- benefits of vpn
    - users can connect to local ISP & connect through ISP to local network
- vpn used to ensure any data sent across pub network like internet is secure
    - vpn creates encrypted tunnel between client & RAS server
- vpn server uses 2 or more NICs for comm
    - 1 nic used to connect to priv network inside org that uses priv ip addressing
    - other NIC connects to external pub network
- to create this tunnel, client 1st connects to internet by establishing conn using remote access protocol
    - once connected to internet, client establishes 2nd conn with vpn server
    - client & vpn server agree on how data encapsulated & encrypted across virtual tunnel
- limitations
    - dont use dc as vpn server
    - vpn server is pub facing so shld be in dmw segment
- NOTE
    - typical vpn use cases
        - ensure secured comm between 2 sites
        - ensure secured comm between site with remote clients
            - to allow remote client to access res offered by site
        - provide secured internet conn to remote client
            - remote client establishes vpn conn to site then use gateway of site to access internet
            - network security between remote client & internet cared for by security measure implemented on site
    - typical config
        - use windows server with 2 NIC to implement vpn server
            - AKA multi-homed dual NIC deployment
    - vpn may or may not be part of domain
        - if windows server part of domain, can directly use active dir for client auth

#### Examples
![](https://i.imgur.com/p2WAKqi.png)
- this diagram shows 3 diff remote clients to site vpn implementations
    - top - firewall based vpn for remote client access to office network
    - middle - router based firewall
    - bottom - microsoft RAS based vpn (use basic router)
- NOTE
    - smw covers microsoft ras based vpn only

![](https://i.imgur.com/A7Sfq1l.png)
- this diagram shows how remote client connects to site (Eg. staff remote access to office network via vpn)
- effect after vpn established:
    - remote client assigned with set of local IP settings (IP addr, gateway, dns)
    - remote client can access to all services offered by site as if connected to lan directly
    - by default, outgoing traffic from remote client will 1st go to vpn server via internet


### Configuring a VPN Server
- general steps
    - install network policy & access services role
    - config winserver2016 as vpn server
        - includes configuring right protocols to provide vpn access to clients
    - config vpn server as __dhcp relay agent__ for tcp/ip comms
    - config vpn server properties
    - config remote access policy for security

![](https://i.imgur.com/f32pHVP.png)
- simulated vpn setup
    - 4 vms
        - 3 windows
        - 1 linux (virtual router)

### Configuring Server's Firewall
- vpn server must send comms through network
    - early config step is to make sure comms can go through firewall setup at server
- if using windows firewall on server
    - tcp & udp ports used by vpn are unblocked by default when configuring a vpn server
        - though impt to make sure they unblocked
- NOTE
    - for simple vpn setup, server firewall configs may all be completed by installation wizard
    - in production system, extra protections usually in place with firewall devices
        - hence need understand config requirement for various types of vpn protocols

### Configuring VPN Properties
- RAS demo 2
    - https://web.microsoftstream.com/video/3d1a4030-6bc9-41e5-8557-b7f68747d984
- after vpn server setup
    - config wizard invoked to guide through config
    - RAS demo 3 - https://web.microsoftstream.com/video/c3d88644-ebdd-4618-b8e6-a29a6a1a3f82
- after initial setup, can further config from routing and remote access tool
    - right click vpn server in tree and click properties


### Configuring DHCP Relay Agent
- dhcp relay agent
    - broadcasts ip config info between dhcp server on network and client acquiring address
    - can config vpn server as dhcp relay agent using routing & remote access tool
- basic terms
    - client contacts vpn server to make conn
    - vpn server as dhcp relay agent contacts dhcp server for ip addr for client
    - dhcp server notifies vpn server of ip addr
    - vpn server relays this ip assignment to client

### Configuring VPN Security
- can setup vpn secrity through __remote access policy__
    - greatly reduces admin overhead
    - more flexibility & control for authorising conn attempts
- elements of remote access policy
    - access perm
    - conditions
    - constraints
    - settings
- 1st step to evaluating access is determine if access perms enabled at vpn server
    - default perm for this policy set to deny access
    - change default perm to grant access in default remote access policy
- conditions of remote access policy - set of attributes that are compared with attributes of conn attempt
    - if conn attempt matches conditions of remote access policy, constraints are evaluated
    - settings in remote access policy are then examined
        - settings include ip filters, encryption, ip settings etc.
- NOTE
    - remote access policy can be setup to allow/deny access requests
        - by default, remote access policy set to deny all
            - hence even ras services up and running, remote clients wont be able to connect until remote access policy configed correctly

#### Establishing Remote Access Policy
- use __routing and remote access tool__ to create & config remote access policy
- to create new remote access policy, click to activate then right click remote access logging & policies folder in tree under vpn server
    - click launch nps to launch network policy server tool

![](https://i.imgur.com/Yo9047H.png)


### Monitoring VPN Users
- after configuring vpn server & placed in production,
    - shld periodically monitor users connected
- use routing and remote access tool to monitor connected users
- with tool open,
    - expand elements under server name in left panel
    - click remote access clients in left pane
    - right pane shows users connected
        - right click and select disconnect to disconnect user

### Troubleshooting VPN Installations
- troubleshooting vpn comms prob can be divided into hardware & software tips

#### Hardware Solutions
- use device manager to make sure network adapters and wan adapters working 
    - also make sure adapter has no res conflicts
- for external DSL adapter or combined DSL adapter and router
    - make sure device properly configured and connected
    - check monitor lights for probs
- call ISP to determine if probs present on ISP's wan

#### Software Solutions
- use services tool or server manager to make sure following services started
    - ip helper, remote access conn manager, IKE and authIP ipsec keying modules, routing and remote access, netlogon, remote access management service, basic filtering engine, windows firewall & secure socket tunneling protocol service
- ensure windows firewall setup to allow remote access
- make sure vpn server enabled
- check remote access policy and make sure access perm granted
- make sure vpn server started
- in routing and remote access tool, check network interface
- make sure ip params correct to provide address pool for either vpn server
- check remote access policy consistent with users' access needs
- open remote access management console & click dashboard in left pane
- if only certain clients but not all having conn probs, try these
    - ensure clients using same comms protocol as server
    - if manage access to vpn server using security grps, make sure ea user acc or comp acc that needs access is in correct grp
- NOTE
    - basically re-check overall hardware conns & system configs
    - checking needs thorough understanding of network infrastructure, vpn protocols, windows and/or active dir operations


Remote Desktop Services
---
### Connecting through Remote Desktop Services
- __remote desktop services (RDS) server__
    - enables clients to run session-based desktops, virtual desktops and software apps on winserver2016 instead of client
- using session-based desktops
    - client accesses rds server to run apps during conn session
- virtual desktops
    - used with accessing virtual machines on virtual server through hyper-v
    - multiple virtual desktops can be in pool of desktops for diff purposes
- 4 main components that enable remote desktop server connectivity
    - winserver2016 multiuser remote desktop services
    - remote desktop services client
    - remote desktop protocol (rdp)
    - remote desktop services admin tools
- when installing rds, can install diff role services
    - remote desktop session host
    - remote deskto web access
    - remote desktop virtualisation host
    - remote desktop licensing
    - remote desktop gateway
    - remote desktop conn broker

- NOTE
    - rds is viable options to offer remote access services to remote clients
        - unique func - remote desktop session created and run on remote desktop server
            - remote client act as viewer to allow user to observe & operate desktop session that runs on remote desktop server
        - this way of remote access offers 2 extra features that vpn doesnt support
            - allow thin client conns
            - enables server admins to know details of remote clients activities


#### RemoteApp
- RDS server employs __RemoteApp__
    - feature that enables client to run app w/o loading remote desktop on client
    - programs appears to be just another program in windows running on local comp
- remoteapp program started by clients through
    - icon on client's desktop
    - client's start menu
    - link on website via remote desktop web access
    - as .rdp (remote desktop protocol) file

![](https://i.imgur.com/pe3AghM.png)

### Uses & Purposes
- used for 3 purposes
    - run apps on server instead of client
    - support thin clients
    - centralise program access
- __thin clients__
    - downsized PCs with minimal windows based OS that access winserver2016 so most CPU-intensive operations performed on server
    - generally used to save money & reduce training & support requirements
    - also used for portable field/handheld remote devices
- centralise control of how programs used
    - highly classified/sensitive documents can be stored & modified only on server
    - server can be configed to provide high lvl of security
- RDS not only support thin clients, but also other OSes
    - win10
    - winserver2016
    - unix/unix based X-terminals
    - linux
    - mac os
    - table os


### Installing Remote Desktop Services
- when installing the remote desktop services role, also need install RDS licensing role service
    - to manage num of terminal server user licenses obtained from microsoft
- rds licensing role server can be installed when u install remote desktop services role
    - licenses can be purchased per user acc or by client device
- when installing rds role, implement __network level auth (NLA)__
    - enables auth before rds conn established
    - designed to eliminate mitm atks
- another element to consider before installing rds role is who will be allowed to access rds server
    - create grps of user accs in advance so can add these grps during installation
- if operating in active dir env
    - consider creating domain local grp (Eg. RDS Users)
    - next create diff global grps of users
        - like global grp for ea department that will access rds server
    - add appropriate user accs for ea department's global grp
    - finally add global grps to single domain local grp

![](https://i.imgur.com/YJVSsPv.png)
- all these features are high on res demands

### Configuring Remote Desktop Services
- after installing rds role & associated role services
    - use server manager to complete basic config in activity 9-9 (prac)

### Build-In Remote Desktop Services
- installation of full scale remote desktop services may be highly demanding of system resources
    - remote desktop role and features
- for all windows servers & some win10 editions, there's build-in remote desktop services
    - limited num of conns
    - simplified config options
    - runs on same remote desktop protocol

### Accessing RDS Server from Client
- rds client comps can signin using __remote desktop connection (RDC)__ client
    - rdc client installed in win vista-10 & winserver2016
- steps to start rdc client
    - start > accessories folder
    - click remote desktop conn
    - enter comp name to access & click connect
    - provide username & password. click ok

Summary
---
![](https://i.imgur.com/BWpIUN4.png)
![](https://i.imgur.com/vNQICdb.png)




###### tags: `SMW` `DISM` `School` `Notes`