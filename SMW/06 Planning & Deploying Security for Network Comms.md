---
title: '06 Planning & Deploying Security for Network Comms'
disqus: hackmd
---

:::info
ST2612 Secure Microsoft Windows
:::

06 Planning & Deploying Security for Network Comms
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

IPSec Concepts
---
- history
    - published in 1995
    - many extra exts added to enhance/replace earlier ver of protocol
    - IKE defined in 1998
    - IKE2 added to protocol in 2005
        - abbrv of IP Security standardised to IPSec since then
- IPSec - set of protocols used to ensure private, secure comms over IP networks by using cryptographic security services based on
    - protecting contents of IP packets
    - packet filtering
    - enforced trusting comms
    - encryption of info travelling through network
    - mosty used as option for IPv4 implementations
- NOTE
    - starting from winserver 2008r2, IKE2 has been default built-in VPN protocols for their Remote Access Services

### IP Security Issues
- orig tcp/ip network protocols not designed with security in mind
    - source spoofing
    - replay packets
    - no data integrity/confidentiality
- subject to
    - DOS atks
    - replay atks
    - spying
    - etc.
- NOTE
    - IPSec is optional feature that network admins can use to protect tcp/ip network traffic
    - protection mainly based on combination of various encryption & hashing schemes

### IPSec Control Elements
- uses 3 main security control elements
    - __Internet Key Exchange (IKE)__
        - protocol for exchanging encryption keys
    - __Authentication Header (AH)__
        - provides authenticity guarantee for packets
    - __Encapsulating Security Payload (ESP)__
        - provides confidentiality through encryption
    - also uses __IP compression (IPComp)__ which is used to compress raw IP data
- NOTE
    - ike is 1st used when 2 parties comm
        - if IKE operation (host to host auth) fails, no further comm possible
    - once IKE cleared, 2 parties may use AH &/or ESP to protect subsequent data traffic

#### IKE Module
- internet key exchange module
    - responsible for 
        - initial security negotiation (phase 1)
            - based on auth methods defined in ipsec rule
            - need to establish 1st to support phase 2 operations
        - determine secret keying material (phase 2)
            - to secured network comm
            - related to filter action setting of associate ipsec rule
- NOTE
    - the 2 phases uses diff security & encryption schemes
        - not elaborating for smw
    - the 2 phases are using diffie hellman (key exchange method) asymmetric key encryptions to exchange data between the 2 parties

### IP Security Implementation
- winserver2016 supports implementation of ipsec
- when ipsec comm begins between 2 comps,
    - comps 1st negotiate using IKE module & auth between receiver & sender using __Microsoft AuthIP extension__
    - extra hasing scheme (optional) helps ensure data integrity at packet header
    - data encrypted with integrity check (optional) at NIC of sending comp as its formatted into IP packet
- ipsec can provide security for all tcp/ip based apps & comm protocols
    - ipsec security policies can be established through grp policy in active dir
        - configed through ip security policies management MMC snap-in
- NOTE
    - auth header (AH) ensures data integrity of packet
        - encapsulating security payload (ESP) - provide encryption & integrity check to protect data packets
        - packet sniffing tools (Eg. wireshark) shows diff of effect of these 2 protocols
    - admins use ipsec security policies to define ipsec configs 
        - policies have to be deployed to take effect
        - ipsec security policy is dependent to grp policy
        - can define ipsec policy at indiv system locally

### IPSec Trade-Offs
- deploying ipsec can affect network perf & compatibility with other services/apps
    - dont deploy ipsec if security it provides not required

#### Impacts
- time needed to establish ipsec conn
    - IKE very complex
- time needed to filter & encrypt packets
    - causes overhead (excess res used)
    - extra packet header needed too
- increased packet size
- network inspection tech used in routers, firewalls, IDS may not work on ipsec packets
- app compatibility with other platforms
- effect on active dir & domain controller conns
- NOTE
    - adding in ipsec might upset some existing security measures
        - popular IKE auth scheme for active dir based env is Kerberos
        - complicated if ipsec is involving DCs as kerberos is hosted by the DCs


Planning an IPSec Deployment
---
- config of ipsec based on
    - the way you use it
    - types of client OS in network
        - diff OS/network devices have diff ways for ipsec implementation
    - types of network devices in network
- not recommended for
    - securing comms between domain members & dc
        - reduce network perf
        - config ofipsec policy complicated
    - secure all traffic in network
        - reduced network perf (again)
        - ipsec cant support multicast & broadcast traffic
        - network tools that need to inspect packet headers may not work
    - NOTE
        - if all traffic in network protected, may help adversaries (enemies) carry out data exfiltration operations undetected
            - hence, ipsec might decrease degree of network security
- use cases of ipsec
![](https://i.imgur.com/fsXsXQW.png)

- proper use of ipsec
    - packet filtering like ipsec with routing & remote access service to permit/block inbound/outbound traffic
    - secure host-to-host traffic on specific paths
        - suitable for LAN
    - secure traffic to servers
        - suitable for LAN
    - combining L2TP & ipsec (l2tp/ipsec) for securing vpn scenarios
    - incorporating site-to-site or gateway-to-gateway tunnelling

### Implementing IPSec Policies
- in simple network structure, single ipsec policy can be designed to contain multiple rules
    - 1 policy for all
    - in large env, many diff ipsec policies can be designed
- factors that inc num of policies required
    - computer roles
    - sensitivity of data travelling
    - comp OS
    - domain r/s & memberships
    - num of apps require ipsec
- NOTE
    - ea system can only be deployed with at most 1 ipsec policy
        - hence, system need to host/cater for diff apps with ipsec protections
        - policy must have multiple rules
            - ea rule cater to 1 type of app

### 5 Elements that make up a Rule
- ea policy can include many rules
- ea rule has 5 configurable elements
    - connection type
        - lan, remote, all
    - mode
        - transport or tunnel
    - filter list
    - host to host auth method
        - used by IKE in phase 1
    - filter action
        - includes choice of AH/ESP
        - negotiated in IKE phase 2 & carried out agreed scheme in actual traffic

#### Connection Type
- only applies for particular types of conns
    - lan
    - remote
        - commonly seen if implemented remote access services in internet facing servers
        - usually installed with at least 2 NICs 
            - Eg. 1 connects to LAN, other to internet via routing device
    - all

#### Deciding which Mode to Use
- has 2 modes
    - transport mode
        - used to secure comms within network
        - can be server to server or server to client
        - provides end to end security
    - tunnel mode
        - secure comms between networks
            - Eg. between 2 gateways
        - primarily used for interoperability with gateways/end systems that dont support L2TP/IPSec or PPTP VPN site to site connns
- in simplest case, ipsec protection caters to system within lan
    - hence use transport mode
- when conns involving wan, use tunnel
- NOTE
    - in smw we focus on transport mode
    - commonly, routers & firewall takes care of site to site traffic security
        - many based on ipsec tunnel mode
        - windows systems may use this security channel w/o ipsec configs
    - tunnel mode only protects data traffic between 2 endpt devices
        - traffic between host to corr endpt not protected by AH/ESP protocols

##### Example
![](https://i.imgur.com/HBJclo3.png)
- ipsec securing traffic between alice & hr server in remote office
- case A
    - ipsec tunnel configed between router & firewall of company
    - alice & hr server involved in ipsec config
- case B
    - ipsec tunnel configed between alice & router 
    - both alice & hr involved in ipsec config
    - diff between A
        - all traffic from/to alice pc protected by ipsec
- case C
    - router & server configed as tunnel endpt
    - both alice & hr involved
- case D
    - vpn channel on alice pc and office network
        - hence, alice can use ipsec in transport mode to protect data between pc and hr
    - however, since vpn alr securing conn, ipsec protection redundant

#### IPSec Filters
- ipsec filter is specification in ipsec rule used to match ip packets
    - filters grped tgt in system wide filter list
    - in ipsec properties setting
        - system wide filter list avail for choice of filter
- packets which match filter applied with associated filter actions like
    - permit
    - block
    - negotiate security
- limitations
    - system configed with ipsec may not apply with expected security scheme if filter set wrongly
    - when network traffic dont match ipsec, it wont be blocked but just pass through
- filter list identifies traffic based on its src, dest & protocol
    - Eg. win2k3, win2k8
    - all icmp/ip traffic
- filter action set for ea type of traffic as identified by filter list
    - only triggered if traffic matches filter
    - actions
        - permit
        - request security/negotiate security
            - carried out at phase 2 of IKE
        - require security/block
    - admins may construct/customise specific actions
- can be managed in 1 of 2 ways
    - create new policy & define set of rules for policy, adding filter lists & actions as needed
    - 1st create set of filter lists & actions then create policies & add rules that combine with filter lists & actions
    - basically create policy 1st or create filter list 1st
- NOTE
    - unlike firewall filters, no action taken against unmatched traffic in ipsec filter
        - in firewall filter unmatched traffic default blocked

![](https://i.imgur.com/FTnm2KS.png)


#### Planning Auth Methods for IPSec
- ipsec auth
    - specifies how comps will prove their identities to ea other when establishing SA (security association)
- if conn matches filter IKE phase 1 will be invoked for initial auth
- avail auth methods
    - kerberos v5
        - default auth method for win2000 server or later
        - based on mutual auth
        - use when all clients can auth using kerberosv5
        - requires least administrative effort
    - certificates
        - requires PKI (pub key infrastructure)
        - method for granting access to users based on unique identification
        - used in situations when access to corporate res, external business partner comms or comps that dont run kerberosv5
    - pre-shared key
        - used when other methods not avail
        - shared secret key
- auth process done using DH asymmetric key encryption for data exchange
- choosing ipsec auth method
    - more than 1 can be selected with designated priority lvl
    - IKE phase 1 will sort out if 2 parties share common auth method
        - if dont match cannot establish ipsec channel
- NOTE
    - IKE v2 released 2005 added EAP (extensible auth protocol) auth as extra choice
    - windows systems adopted IKEv2 as built-in vpn protocol
    - pre-shared key used for testing, short term ad-hoc solution
        - cuz difficult to maintain & secure
    - kerberos best for domain based systems
        - certs ideal for non-domain based/mixed systems

![](https://i.imgur.com/MyJnUkG.png)


### Encryption Levels
- 2 basic categories
    - symmetric key encryption
    - pub key encryption
- lifetime settings determine when new key generated
- NOTE
    - in ike phase 2 both parties nego for commonly avail encryption scheme
        - filter action bases on it to encrypt data packets

![](https://i.imgur.com/SQnitcn.png)
- this screenshot shows 4 possible encryption methods

#### Methods of Hashing
- secure hash algo (sha)
    - use 160bit encryption key
    - very high security method
- message digest 5 (md5)
    - use 128bit key
    - lower perf than sha
- hashing method used to support AH traffic

#### Methods of Encryption
- data encryption standard (des)
    - use 56bit key
    - not reco for high security
- triple des (3des)
    - 168bit key
    - medium & high security networks
- encryption method used to support ESP traffic
- NOTE
    - hashing & enc methods here a bit old. new systems hash more choices

### IPSec Protocols
![](https://i.imgur.com/oRoqdsd.png)

- AH transport mode
![](https://i.imgur.com/b8nliNz.png)

- ESP transport mode
![](https://i.imgur.com/1mPMxYD.png)

- tunnel mode uses double encapsulation, suitable for protecting traffic between network systems (Eg. untrusted internet)
    - ah tunnel mode - encapsulates ip packet by placing ah header between internal & external ip header
    - esp tunnel mode - ip packet first encapsulated with esp header, then result encapsulated with extra ip header

![](https://i.imgur.com/V8a3xiH.png)
![](https://i.imgur.com/jlGAlVe.png)


How IPSec Works
---
![](https://i.imgur.com/oBpQCKP.png)
- security association (sa)
    - may include attributes like
        - crypto algo & mode
        - traffic encryption key
        - params for network data to be passed over conn


Deploying IPSec Policies
---
- can be deployed using
    - local policy objs
        - a way to enable ipsec for comps that aint members of domain
    - grp policy objs
        - ipsec policy propagated to any comp accs that affected by gpo
    - cli tools
        - netsh ipsec cmd in winserver 2003/2008

### Using Local Policy Objects
![](https://i.imgur.com/7Cd9U9S.png)

### Using Group Policy Objects
- factors to consider when selecting gpos for ipsec policy assignment
    - assignment precedence of ipsec policies
        - lowest to highest
            - local, site, domain and ou
    - persistent ipsec policy has highest precedence of all even tho stored on local comp
        - effective even other policies cannot be applied
    - ipsec policies from diff OUs nvr merged
    - for domain-based policy, limit num of rules to 10 or less
    - create & apply ipsec policy at domain lvl to provide baseline of ipsec protection
    - use export & import policies commands in ip security policy management console to backup & restore ipsec policy objs
    - adequately test impact of new ipsec policies before assigning them in domain

### Understanding Default IPSec Policies
- client (respond only)
    - secure comm only if other comp requests it
- server (request security)
    - accepts initial incoming comm that's unsecured
    - requests for comm to be secured
    - carry on with unsecured conn if client dont support
- secure server (require security)
    - accepts initial inbound comm that's unsecured
    - requires all conn to be secured

### Understanding IPSec Policy Precedence
- possible to config ipsec for multiple containers that will affect comp
    - only 1 ipsec policy can be assigned to comp at a time
    - if there's multiple ipsec policies assigned at diff lvls, last one takes effect
- precedence sequence
    - local gpo, site, domain, ou
- default order can be overriden using enforced, block policy inheritance
- when troubleshooting ipsec policies & precedence, rmb
    - only single ipsec policy can be assigned at specific lvl in active dir
    - ipsec policy assigned to OU takes precedence over domain-lvl for member in OU
    - ipsec policies from diff OUs are nvr merged
    - OU inherits policy of its parent OU unless policy inheritance explicitly blocked or separate policy explicitly assigned to OU
    - before assigning ipsec policy to gpo, verify the grp policy settings that's required for the policy
    - use enforced & blk policy inheritance features carefully
- procedure for deleting policy objs
    - unassign ipsec policy in gpo
    - wait 24h to ensure that change propagated 
    - delete gpo
- __persistent policy__ - provides max protection against atks during comp startup
    - adds to/overrides local/active dir policy
    - remains in effect regardless of whether other policies applied
    - provides backup security in case ipsec policy gets corrupted or if errors occur
    - can be set using cli tools
        - netsh at local station
- NOTE
    - persistent policy AKA static ipsec policy
        - provides 1st line of def right after system powered up
            - since gpo associated to ipsec takes time to be in effect after system reboot

Summary
---
![](https://i.imgur.com/XCUxoN0.png)
![](https://i.imgur.com/lhZH3fB.png)
![](https://i.imgur.com/2fi68IZ.png)







###### tags: `SMW` `DISM` `School` `Notes`