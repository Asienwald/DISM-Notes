

07 Planning & Deploying Public Key Infrastructure & Secured Web Content Access Services
===


## Table of Contents

- [07 Planning & Deploying Public Key Infrastructure & Secured Web Content Access Services](#07-planning---deploying-public-key-infrastructure---secured-web-content-access-services)
  * [Digital Certificates](#digital-certificates)
    + [Defining Certificate Requirements](#defining-certificate-requirements)
      - [Where are Certs Needed?](#where-are-certs-needed-)
    + [What is a Digital Certificate?](#what-is-a-digital-certificate-)
  * [Certificate Authority](#certificate-authority)
    + [CA Hierarchies and Roles](#ca-hierarchies-and-roles)
      - [Rooted Trust Model](#rooted-trust-model)
      - [Cross-Certificates Model](#cross-certificates-model)
    + [Using 3rd Party CAs](#using-3rd-party-cas)
  * [Installing Certification Authority Role](#installing-certification-authority-role)
    + [Selecting Cert Enrollment & Renewal Method](#selecting-cert-enrollment---renewal-method)
      - [Methods for Automatic Enrollment](#methods-for-automatic-enrollment)
      - [Obtaining Cert from Issuing CA](#obtaining-cert-from-issuing-ca)
    + [Certificate Renewal](#certificate-renewal)
    + [Configuring Cert Templates](#configuring-cert-templates)
    + [Configuring Archival & Recovery of Keys](#configuring-archival---recovery-of-keys)
    + [Deploying and Revoking Cert for Users, Computers and CAs](#deploying-and-revoking-cert-for-users--computers-and-cas)
    + [Certificate Revocation Lists](#certificate-revocation-lists)
      - [OCSP & OCSP Responder](#ocsp---ocsp-responder)
  * [Secured Web Access](#secured-web-access)
    + [Deploying and Managing SSL Certificates](#deploying-and-managing-ssl-certificates)
    + [IIS Authentication Methods](#iis-authentication-methods)
    + [HTTPS](#https)
    + [Configuration of Web Server for SSL Certs](#configuration-of-web-server-for-ssl-certs)
    + [Configuration of Client for SSL Certs](#configuration-of-client-for-ssl-certs)
  * [Types of Certs](#types-of-certs)
    + [Self-Issued Certs](#self-issued-certs)
    + [Publicly Issued Certs](#publicly-issued-certs)
  * [Summary](#summary)


Digital Certificates
---
### Defining Certificate Requirements
- microsoft windows server enables secure data access through digital certs
    - certs allow users/systems prove their identity (they're who they say they are)
- before using digital certs, need to design a __public key infrastructure (PKI)__
    - pki supports digital certs operations
    - these operations designed to ensure 2 communicating parties can trust ea other even though they dont know/associate with ea other prior to current comm
        - if new site operating with proper digital cert, might give user certain lvl of confidence to proceed
- to protect exchanging msgs from eavesdropping atk with async encryption algo
    - key pair associated with indiv party
    - ea indiv party keeps its priv key as secret but share pub key to everyone
    - msgs being encrypted with pub key can only be decrypted by corr priv key
    - digital signed msg with indiv priv key can only be verified by corr. pub key
- problem
    - how to obtain genuine pub key before establishing secure comm channel with pt?
- __public key infrastructure (PKI)__
    - tech with series of features relating to auth and encryption
    - based on system of certs
        - ea cert contains pub key & name of subj
    - allows org to publish, use, renew and/or revoke certs & enroll clients
- NOTE
    - async encryption algo used to enable secure comm
        - need secure way to exchange/distribute pub keys to make it work
        - use digital certs to verify if received pub keys are real
    - more comprehensive definition of pki - set of roles, policies, hardware, software and procedures needed to create, manage, distribute, use, store and revoke digital certs & manage pub key encryption

#### Where are Certs Needed?
- digital signatures
- secured email
- secured http comm (HTTPS/SSL)
- internet auth
- software code signing
    - verify origin of piece of code using pub key in cert
- ip security
- smart card logon
- encrypted file system
- 802.1x auth


### What is a Digital Certificate?
- https://www.youtube.com/watch?v=LRMBZhdFjDI
- NOTE (from vid)
    - digital cert needed to hold trustworthy pub key
        - this key used for subsequent secure comms between cert recipient & owner of pub key
        - owner of pub key knows corr. priv key
    - need root CA & subsidiary issuer CAs which is responsible for signing on digital cert
        - if receive cert & verified its signed by trustworthy root CA or subsidiaries, can trust cert content (pub key)
    - questions
        - how to verify that cert signed by trustworthy CA?
        - how to trust root CA?
            - who decides which root CA is trustworthy?

Certificate Authority
---
- cert authority (CA) is entity that issues digital certs to other parties
- root CA can issue certs to subordinate/intermediate/issuing CAs
    - issuing CAs can issue certs to users/clients

### CA Hierarchies and Roles
- types of hierarchies used for CAs
    - rooted trust model
    - cross-certification trust model
    - hybrid trust model
- possible roles for CA
    - for standalone CA
        - rudimentary CA
        - intermediate CA
    - for enterprise CA
        - basic-security CA
        - medium-security CA
        - high-security CA
- NOTE
    - servers at diff lvl in hierarchy plays diff roles
    - for standalone ca, target clients not bound to enterprise which implements the services
        - applicable if cert services offering to general public
    - for enterprise ca, target clients are within enterprise
        - Eg. internal staff & computing operations

#### Rooted Trust Model
- root CA has self-signed cert & CA issues cert to all direct subordinate CAs
- CAs in this model can be offline/online
    - allows flexibility when deploying & managing PKI
- ea CA serves single role within hierarchy & not dependent on other CAs
    - allows rooted trust hierarchies to be more scalable
    - easier to administer than other hierarchies
- possible to add new CA to hierarchy
- falls into 2 subcategories
    - 2-tier CA hierarchy 
    - 3 tier CA hierarchy
- any ca in rooted trust hierarchy is either root or subordinate but nvr both
- ea ca responsible for processing requests, issuing certs, revoking certs and publishing CRLs
- ea ca can be managed independently

![](https://i.imgur.com/1CbPK9H.png)
- root ca trusted by everyone
    - it signs a few certs to empower couple of servers to be intermediate ca
    - these ca then empower next lvl of ca
        - these servers are operational servers issuing out digital certs to clients which ask for services
- NOTE
    - top lvl ca always based on self-signed cert to distribute its public key
        - somehow everyone unconditionally trusts this self-signed cert & pub key it holds

#### Cross-Certificates Model
- all ca self-signed & trust r/s between ca based on cross-certs
    - certs issued by 1 ca trusted by comps which belong to other ca hierarchy (cross hierarchy trust)
- cross certs dont need to be bidirectional
- advantages
    - low cost
    - greater flexibility
- disadvantages
    - more administrative overhead
    - increase risk of unauthorised access to internal resources
- NOTE
    - who decides which ca to be trusted in system?
        - all OS has set of pre-installed root ca (most self-signed)
        - because of these pre-installed root ca certs, system accepts digital certs signed by anyone of these root ca
    - in rooted trust model, ea root ca trusted by everyone
        - its root ca cert (self signed, contains pub key) will be required to pre-install in everyone's machines
        - hence when num of rooted trust model root ca grow, may face serious prob of too many pre-installed root CAs
            - 1 approach is to use cross-cert model
            - in cross-cert model mutually trusted ca will issue digital certs to ea other
            - Eg. ea machine pre-installed with root ca of XXX
                - if new CA YYY gets digital cert issued by XXX, through cert chain, every machine will trust digital cert issued by Y

![](https://i.imgur.com/us53UrV.png)
![](https://i.imgur.com/qKCke4I.png)
- Let's Encrypt is free charge root ca that uses cross-cert model

### Using 3rd Party CAs
- useful when org conducts most of business with external customers & clients
    - Eg. Digicert, Globalsign or GoDaddy
- advantages
    - customers have greater degree of confidence when conducting secure transactions with orgs as they trust 3rd pt ca
    - allows org to take advantage of 3rd pt ca's understanding of technical, legal and business issues with cert use
- disadvantages
    - high per-cert cost
    - less flexibility in managing certs
    - autoenrollment not possible
- windows system alr configured with list of trusted commercial 3rd pt CAs
    - easily viewed & configured via web browser
    - these certs kept in trusted root certification authorities store of the system
        - these certs always trusted by system
        - when system receives cert signed by 1 of these root ca, trusted

![](https://i.imgur.com/zhSKcev.png)

- NOTE
    - most public facing commercial sites use 3rd pt ca issued certs as most systems & browsers accept certs signed by 3rd pt CAs
    - below shows usage & market shares of popular 3rd pt CAs

![](https://i.imgur.com/nVWx3KV.png)


Installing Certification Authority Role
---
- root ca installed first, followed by intermediate ca and finally issuing ca
- root CA - CA at top of certification hierarchy and trusted unconditionally by clients in an org
    - enterprise root ca stores info in active dir & server that hosts the service must be joined to a domain
    - storing the root ca offline is much more secure
- intermediate CA - CA subordinate to root CA
- issuing CA - issues certs to users & comps

![](https://i.imgur.com/dWj6CTa.png)
- active dir certificate services is an avail server role
    - can setup own in-house PKI with this role

### Selecting Cert Enrollment & Renewal Method
- __cert enrollment__ - operation of requesting for a cert from an issuer CA
    - client initiated
- __cert renewal__ - routine to request replacement/renewal cert
    - pub key stored may be same
    - but issuer CA sign its digital cert on the renewal cert with new expiry date
- depends on
    - types of certs you intend to use
    - num & type of clients to enroll
- 2 types
    - manual
        - if administrative approval required
        - most useful for issuing & renewing comp & ipsec certs
    - automatic
        - if no approval necessary
        - can improve administrative control over certs

#### Methods for Automatic Enrollment
- cert autoenrollment & renewal
    - based on combi of grp policy settings & cert templates
- cert request wizard & cert renewal wizard
- web enrollment support pages
- smart card enrollment station
- NOTE
    - autoenrollment is feature only avail for in-house CAs
        - for selected types of cert requests, ca will auto approve client requests & provide new certs
    - manual enrollment is safer approach
        - ea client request needs administrative approval


#### Obtaining Cert from Issuing CA
![](https://i.imgur.com/vGwUpj4.png)
- for windows ca, it comes with web interface that can let users request for cert enrollment
    - also allows users to download root CA cert & its cert chain
    - after downloading cert chain, user may install into system's trusted root CA repo

### Certificate Renewal
- security and renewal requirements for certs
    - value of network res protected by ca trust chain
    - degree to which you trust your cert users
    - amt of admin effort you're willing to devote to cert & ca renewal
    - business value of cert
- NOTE
    - renewal requirement refers to how often to renew keypair and cert
        - these are 2 diff operations
        - more often you renew, higher security measure can be assured
            - though more operational overhead
    - highlights
        - All certificates have an expiry date
        - need to renew a certificate before its expiry date
        - Since each certificate contains a pub key for a specific application, 1 type of renewal is just to create and sign on a new cert which contains the same pub key.
        - The pub key owner may generate a new key-pair and replace the old pub key with newly generated pub key while renewing the cert
        - Finally, the signer itself should also update its key-pair. 
            - Once the signer’s key-pair is changed, a new rootCA certificate should be generated too.
        - To keep the PKI operation smooth, you may see multiple rootCA certificates for the same CA organization co-existing in the Trusted Root Certificate Authorization store. 


![](https://i.imgur.com/l4dDK2D.png)



### Configuring Cert Templates
- cert templates - windows utility to help ca administrator facilitate diff types of cert enrollment
    - compared to cli approach, cert templates may help CA admin better manage CA services
- cert services provides cert templates to simplify process of requesting & issuing certs
    - ea template contains rules & settings
    - can serve single purpose or multiple purposes
- cert templates are avail only on enterprise root and subordinate CAs
    - stored in active dir
    - avail to every enterprise CA in forest
- cert templates MMC snap-in provides admins capability to
    - create additional templates by duplicating & modifying existing templates
    - modify template properties
    - configure policies applied to cert enrollment, issuance and app
    - allow autoenrollment of certs
    - configure ACLs on cert templates
- issuance of cert requests can be controlled in 3 ways
    - configuring perms on template from security tab
    - preventing CA from issuing cert type by deleting template
    - configuring perms on CA
- restrict perms on your CAs to prevent unauthorised access
- configure discretionary access control list (DACL) for ea template
- NOTE
    - depending on app, diff types of digital cert keeps diff info in cert content
        - cert templates provide default input requirement & settings for diff type of cert
        - helps to reduce errors and make operations more efficient

![](https://i.imgur.com/g9sUdrD.png)
![](https://i.imgur.com/c6LPUPz.png)


### Configuring Archival & Recovery of Keys
- possible to config CA to archive priv keys of certs at time of issuance
    - enable to recover key if lost
- only highly trusted indivs granted privilege of archiving & recovering keys
- cert services dont archive priv keys by default
- key recovery methods
    - key recovery agent
    - certutil tool
    - krt.exe
- NOTE
    - generation of key pair in PKI (2 approaches)
        - 1st approach - cert owner (& requester) will 1st create key pair & send pub key to CA to enclose the pub key in a digital cert with CA's digital signature
            - ca dk owner's priv key
        - 2nd approach - cert owner asks for compehensive service from ca to help generate key pair and seal pub key in digital cert
            - requester gets priv key of key pair back & digital cert that holds pub key
            - requester has to trust ca, which will delete the priv key from the CA's system
            - this approach gives CA option to archive the priv key

### Deploying and Revoking Cert for Users, Computers and CAs
- possible to automate deployment of certs by configuring grp policy
- manual approval shld be required for
    - all certs that are needed to perform network administration or software dev
    - all certs issued to joint venture partners
- conditions to auto enroll certs
    - client comp must be integrated into active dir
    - users require read, enroll and autoenroll perms
- reasons for revoking cert
    - cert is compromised
    - termination of acc to whom cert issued
- NOTE
    - lifespan of cert default limited by expiry date setting
        - but in some cases need invalidate digital cert before it rches expiry date

![](https://i.imgur.com/hdEifdC.png)
- CA admin can revoke issued cert
    - though since PKI based on trusted model which dont always need online validation
    - even some certs revoked by CA other systems wont know of revocation
        - hence we need the __certificate revocation list__

### Certificate Revocation Lists
- all certs have specified lifetimes
    - in some situations, there's need to invalidate/revoke cert before it rches end of lifetime
- revoked certs published in cert revocation list (CRL)
    - CRLs valid only for limited time
    - PKI clients need to retrieve new CRL periodically
    - must define CRL location with access path before deploying certs
- NOTE
    - CA publishes crl periodically to let others know which certs aint valid anymore
        - needs other systems to download published crl from ca
    - extra res and effort may incur for ca side when publishing crl
    - in many cases client may not download crl for validation but rather take the risk to any certs as long as its signed properly and not expired yet

#### OCSP & OCSP Responder
- online cert status protocol (OCSP)
    - proposed in 2013
    - internet protocol used for obtaining revocation status of an X.509 digital cert
    - complements (not replace) operations of CRLs
- OCSP responder
    - server typically run by cert issuer which returns signed response on status of particular issued cert
    - possible response
        - good, revoked or unknown
        - no response, as issuer doesnt implement responder service
- comparison to CRLs
    - less burden for clients to maintain crl
        - network and storage
    - easier to implement as compared to crl for up to date checking
    - ocsp use non-encrypted msg so subjected to interception
    - ocsp is optional component for cert server
- NOTE
    - ocsp compensates limitations of crl by letting outsider systems/users check the validity of a cert
    - for ocsp responder, unknown status might return due to issues in query
        - Eg. signature of cert not signed properly
        - unknown is diff from revoked but user shouldnt trust cert anyway


Secured Web Access
---
- 2/3 issues for non secured web access
    - how to auth identity of remote server
        - Eg. hackers setup phishing site to mislead clients to submit confidential info/pay for non-existing service
    - how to ensure transferred content not tampered
    - for enterprise servers, how to auth identity of remote client trying to access its services
- possible solution
    - SSL certs

### Deploying and Managing SSL Certificates
- need to install IIS in highly secured & locked configuration
- __secure sockets layer (SSL)__ - pub key based security protocol
- SSL uses
    - certs for auth
    - encryption for msg integrity & confidentiality
- need installation of valid server cert to establish encrypted comms using SSL
- cert based SSL features in IIS consists of
    - server cert
    - client cert (optional)
    - various digital keys
- ways to obtain certs
    - created using cert services
    - obtained from trusted 3rd pt ca

### IIS Authentication Methods
![](https://i.imgur.com/fWCn9Tk.png)
- diff ways to auth remote client
    - cert auth is 1 method that applied PKI
    - for the rest they can also operate with SSL (which is another way to apply PKI) for secured data comm and server auth

### HTTPS
- https (http over SSL)
    - tech that encrypts indiv msgs in web comms rather than establishing secure channel
    - popular ecommerce tech & used for secure online shopping
    - port 443
    - ssl-secured URLs begin with `https://` prefix

### Configuration of Web Server for SSL Certs
- use ssl encryption only for sensitive info
    - encrypted transmission can significantly reduce transmission rates and server perf
- server certs provide way for users to cfm identity of website
- server cert contains
    - org name affiliated with server content
    - name of org that issued cert
    - pub key used to establish encrypted conn

![](https://i.imgur.com/jUQ8RhB.png)
![](https://i.imgur.com/61WaLOS.png)

### Configuration of Client for SSL Certs
- typical client cert contains
    - identity of user
    - identity of cert authority
    - pub key used for establishing encrypted comms
    - validation info like expiration date & serial num
- to protect web content from unauthorised access, you must
    - use basic, digest or integrated windows auth tgt with requiring client cert
    - create windows acc mapping for client certs
- NOTE
    - windows acc mapping for client certs is unique feature
        - once client presented client cert to server, clieht system accesses server with mapped user credential
        - it provides more convenience to user w/o higher security risk
        - mapping itself done manually by system admin

![](https://i.imgur.com/9nzIIok.png)



Types of Certs
---
### Self-Issued Certs
- considerations when issuing your own server certs
    - microsoft cert services can accomodate diff cert formats & provide auditing & loggin of cert-related activity
    - evaluate cost of ea
    - keep learning curve in mind
    - evaluate willingness of outside vendors clients to trust your org as cert supplier
- NOTE
    - SSL needs digital cert for server to setup https services
        - this cert can be self-signed or self-issued cert which may incur lower cost but general public might not accept
        - other way is to get cert from 3rd pt ca

### Publicly Issued Certs
- used when user suspects your self-issued certs
- can be obtained from mutually trusted 3rd pt ca
    - Eg. verisign, globalsign or thawte
- wait time - several days to months
- must be renewed on regular basis
- general rules abt any type of web certs
    - ea site can only have 1 server cert assigned to it
    - 1 cert can be assigned to multiple web sites
    - can assign multiple ip addr per site
    - can assign multiple ssl ports per site


Summary
---
![](https://i.imgur.com/47gLFZ0.png)
![](https://i.imgur.com/eQp9FtC.png)
![](https://i.imgur.com/IX8o3wg.png)





###### tags: `SMW` `DISM` `School` `Notes`