---
title: '03 Account Manager & Managing Resource Access'
disqus: hackmd
---

:::info
ST2612 Secure Microsoft Windows
:::

Lecture 03 Account Manager & Managing Resource Access
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

User Account Management
---
- default accounts
    - admin & guest
- accs can be setup in 2 general envs
    - accs setup through stand-alone server dont have active dir installed
        - __local user accounts__
    - accs setup in domain when active dir installed
        - __domain user accs__
        - these accs can access any server or res in domain

### Creating Accounts when AD not Installed
- new accs created by first installing local users & grps MMC snap-in for stand-alone servers that dont have AD

### Creating Accounts when AD Installed
- when AD installed & server is DC
    - use active dir users & comps tool either from
        - windows admin tools folder
        - tools in server manager
        - MMC snap-in
    - activity 4-4 for creating acc in AD

### Disabling, Enabling & Renaming Accounts
- when user take LOA, can disable acc
    - orgs can practice disabling accs when someone leaves & enable acc for replacement person
    - activity 4-5 for disabling/renaming/enabling acc

### Moving an Account
- when employee moves to diff department might need to move acc from 1 container to another
    - actvity 4-6

### Reset Password
- admin cant lookup password
    - but can reset password for users
- for orgs that have accs that manage sensitive info,
    - advisable to have specific guidelines that govern the circumstances which an acc password is reset
    - activity 4-7
- AD recycle bin - to recover deleted acc
    - by default off

![](https://i.imgur.com/9frsZRC.png)




### Deleting Account
- good prac to delete acc not in use
    - if not can expose company to security risks
- when deleting acc
    - its __globally unique identifier (GUID)__ is also deleted & will not be reused even if u create another acc using same name
    - activity 4-8


Security Group Management
---
- for res permission management, best way is by grping accs with similar characteristics
- scope of influence
    - reach of grp for gaining access to res in AD
- types of grps
    - local AKA machine local
    - domain local
    - global 
    - universal
- these grps can be used for security of distribution grps
    - security grps
        - used to enable access to res on stand-alone server or in AD
        - res access permission implemented via grp membership
    - distribution grps
        - used for email/telephone lists
        - provide quick mass distro of info

### Properties of Groups
- can config properties of specific grp
    - through local users & grps tool for local grps
    - in AD users & comps tool for domain grps
- properties configed using these tabs
    - general
    - members
    - member of
    - managed by

### Organisational Units (OU) VS Security Membership
- diff between security grps & OU
    - grp policies applied to OUs
        - Eg. password policies
    - delegation of authority also applied to OUs
    - security grps used to assign file & folders permissions, shared folders permissions and any type of res permissions

![](https://i.imgur.com/5OxZuHz.png)

### Implementing Local Groups
- local security grp
    - manage res on stand-alone comp that's not in domain or member servers of domain
- instead of installing AD, can divide accs into local grps
    - ea grp given diff security access based on res at server

### Implementing Domain Local Groups
- domain local security grp
    - used when AD deployed
    - typically used to manage res in domain & give global grps same & other domains access to these res
- scope of domain local grp is the domain in which grp exists
- purpose of domain local grp is to provide access to res
    - can grant access to servers, folders, shared folders & printers to domain local grp
- shld put domain local grp in access control lists only
    - members shld be mainly global grps

![](https://i.imgur.com/o0lveF6.png)

### Implmenting Global Groups
- global security grp
    - intended to contain user accs from single domain
    - can be setup as member of domain local grp in same/other domain
- global grp can contain user accs & other global grps from domain in which its created
- can be converted to universal grp
    - as long as not nested in another global grp/universal grp

![](https://i.imgur.com/wBZJjrE.png)

- use of global grp to build with accs that need access to res in same/other domains
    - then make global grp in 1 domain a member of a domain local grp in same/other domain
    - enables you to manage user accs & their access to res through 1/more global grps
        - while reducing complexity of managing accs

![](https://i.imgur.com/CzQhLk0.png)

### Implementing Universal Groups
- universal security grps
    - provide means to span domains & tress
    - membership can include user accs/global grps/universal grps from any domain
    - offered to privde easy means to access any res in a tree
        - or among trees in a forest

### Guidelines to Simplify Plan to use Groups
- use global grps to hold accs as members
- use domain local grps to provide access to res in specific domain
- use universal grps to provide extensive access to res

![](https://i.imgur.com/jwb8occ.png)

### Implementing Security Groups & Resources Permission
- best practices

![](https://i.imgur.com/LPVLZci.png)

#### Example
![](https://i.imgur.com/dEcSM1P.png)
![](https://i.imgur.com/gTwUWOG.png)
![](https://i.imgur.com/LgXWDE0.png)
![](https://i.imgur.com/pQ5fzuE.png)


Managing Folder & File Security
---
- creating accs & grps are initial steps for sharing res
    - next steps to create access control lists (ACL) to secure these objs & set up for sharing
- __discretionary acl (DACL)__
    - configed by server admin/owner of obj
- __system acl (SACL)__
    - contains info used to audit access to an obj
- DACL & SACL controls for folders & files
    - attributes
    - permissions
    - auditing
    - ownership

### Configuring Attributes
- attributes stored as header info with ea folder/file
    - tgt with other characteristics including volume label, designation as subfolder, date of creation & time of creation
- 2 basic attributes in NTFS (still compatible with FAT)
    - read-only & hidden
        - on general tab in NTFS folder/file's properties dialog box
- NTFS offers advanced/extended attributes
    - accessed by clicking general tab's advanced btn
    - advanced attributes
        - archive
        - index
        - compress
        - encrypt

![](https://i.imgur.com/HegIqX5.png)

#### Archive Attribute
- indicates that folder/file needs to be backed up as new/changed
    - file server backup systems can be set to detect files with archive attribute to ensure files are backed up

#### Index Attribute VS Windows Search Service
- NTFS index attribute used to index folder & file contents so file props can be quickly searched in server 2016 through indexing service
- server 2016 offers newer, faster search service called __Windows Search Service__
    - to use must install file & storage services role via server manager

#### Compress Attribute
- folder & contents can be stored on disk in compressed format
    - compression saves space
    - can work on files similar as uncompressed
    - compressed files increase cpu overhead to open files & copy them
- best practices
    - dont use compression on busy servers with high-volume write/execute operations
    - can use on servers that are rarely busy
    - can use on files rarely accessed.archived on server
    - dont use on user home folders
        - typically have high lvls of read/write activity

#### Encrypt Attribute
- protects folder & files so only user who encrypts folder/file can read
- uses __microsoft encrypting file system (EFS)__
    - sets up unique, private encryption key associated with user acc that's encrypted in file
- EFS uses both symmetric/asymmetric encryption
- when moving encrypted file to another folder on same comp, file remains ecnrypted even if you rename
- __cipher__ command
    - tool in powershell for EFS operations
- best practices
    - movile files for encryption into designated folders flagged for encryption
    - safer for app to work on file in encrypted folder than on file that's individually encrypted
    - workstation users & server admins shld consider encrypting My Document/Documents folder
    - users/sysadmins shld frequently export certs & priv keys to portable keys & store in secure place

![](https://i.imgur.com/8QNHi1F.png)


### Configuring Permissions
- permissions
    - control access to obj (Eg. folder/file)
- when config folder so domain local grp has access to only read contents of folder
    - you're configuring permissions
    - at same time also configuring folder's DACL of security descriptors
- can customise permissions
    - can set special permission

#### Best Practices Guidelines by Microsoft
- protect /windows folder than contains OS files from general users
    - allow limited access
- protect server utility folders with access permissions only for admins, server operators & backup operators grps
- protect software app folders with read & execute
    - write to enable users to run apps & write temporary files
- create publicly used folders to have modify access 
- provide users full control of home folders
- remove unnecessary access grps from confidential folders
- use deny sparingly

### Configuring Auditing
- auditing
    - enables you to track activity on folder/file
- windows server 2016 NTFS folders & files
    - enable you to audit combination of any/all activities listed as advanced permissions

### Configuring Ownership
- folders 1st owned by acc that creates them
- folder owners can change permission for folders they create
- ownership can be transferred only by having the Take Ownership advanced permission
    - or full control permission (includes take ownership)

![](https://i.imgur.com/NxhSp5r.png)

Configuring Shared Folders/Files Permissions
---
- folder can be set up as shared folder for users to access over network
    - includes features so person configuring share is more aware of security options
    - must 1st enable sharing

### Enabling Sharing
- 1st step to share folder/file over network
- network discovery can be turned on
    - network discovery - ability to view other network computers & devices
- only need to do once
    - but necessary for users to access server's shared file/folder & printer resources

![](https://i.imgur.com/nuQ6AMi.png)

### Configuring Sharing through File Properties
- share permissions can be set using the file sharing window & file's sharing tab in its properties dialog box
- when configuring sharing using advanced sharing options
    - share permission include full control & change 
    - configed using advanced sharing btn on sharing tab of properties
- share permissinons
    - read
    - write
    - change/contribute
    - custom
    - full control
    - owner
- can cache folder to make contents of shared folder available offline
    - offline modified files can be sync with network ver of files
    - cached in 3 ways
        - only files & programs that user specify will be available offline
        - all files & programs that user opens from shared folder are auto avail offline
- __Access-based enumeration__
    - permits user to view only files whr they have permissions
- besides hiding shared folder using $ sign, can enable access-based enumeration

### Configuring Sharing through Server Manager
- server manager
    - another way to config file/share permissions
    - offers interface for managing permissions & shares from 1 tool
    - there's more easily accessed options for share management
- __server message block (smb) protocol__
    - enables os to offer shared files, folders, printers, serial ports & other port comms on network
- __network file system (nfs) protocol__
    - used for file & folder sharing on linux systems
    - when installed on windpws system share, enables it to be accessed by unix/linux comps
- file server resource manager role service
    - allows you to set folder quotas

### Publishing Shared Object in Active Directory
- to publish obj
    - means make it avail to users to access when viewing AD contents
    - easier to find when user searches for it
- active dir search capabilities auto built in all modern windows os
    - including win10 and server 2016
- when publishing obj, can publish it to be shared for domain-wide access or through OU

### Combining NTFS & Shared Folder Permissions
- when accessing shared folder over network, both NTFS & share perms considered
    - when they combined, more restrictive perm apply

#### Example
![](https://i.imgur.com/wbSUmAm.png)



Troubleshooting Security Conflict
---
- server 2016 offers effective active tab in props of file
    - to help troubleshoot permission conflicts
    - can view effective perms assigned to user/grp
- calculation will take into acc grp membership & perm inheritance
- take into acc what happens when folder/file are copied/moved
    - can be affected as follows

![](https://i.imgur.com/9tkPvJA.png)


Important Features in Windows Server 2016 Active Directory
---
- 5 impt features
    - restart capability
    - read-only domain controller
    - cloning domain controllers
    - fine-grained password policy enhancements
    
### Restart Capability
- server 2016 provides option to stop AD domain services w/o taking down comp
- after work done in AD, simply restart AD domain services

![](https://i.imgur.com/9o22Cih.png)

### Read-Only Domain Controller (RODC)
- read only domain controller (RODC)
    - cannot use to update info in AD
    - dont replicate to regular DCs
- RODC can still func as key distribution center for kerberos auth method
- purpose for better security at branch locations
    - phy measures might not be as strong
- can be configed as DNS server

### Cloning Domain Controllers
- server 2012 r2 introduced ability to clone domain controllers
    - targeted for easier deployment of multiple DCs in env with multiple VMs
- cloning cuts down steps required to create more virtual DCs
- server admin can config active dir
    - then create copy of virtual DC
    - more steps can be handled by running powershell cmdlets & using ps scripts to define config params

### Fine-Grained Password Policy Enhancement
- diff security grps have diff password policies
    - server 2012 r2 introduced AD admin center for managing password settings objs in AD schema
        - make server access more secure
        - help reduce errors made by server admins when working with fine-grained passwords


Protected Users Global Group
---
- enforces strict locked-in security protection measures that cannot be reconfigured
    - only way to change security of member of this grp is to remove from grp
    - user accs, comps, printers & servers can be members

#### Security Restrictions
- grp members cannot use weaker forms of auth
- kerberos ticket granting ticket's lifetime limited to 4hours
    - means grp member must be auth every 4 hours
- connections to system that dont utilise this global grp cannot succeed
- only higer-lvl encryption methods compatible with kerberos security can be used


Implementing User Profiles
---
- local user profile auto created on local comp when login first time
    - profile can be modified to customise desktop settings

### User Profile Advantages
- multiple users can use same comp & maintain own customised settings
- profiles stored on network server so avail to users regardless of comp they use
    - AKA __roaming profile__
- profiles can be made mandatory so users have same settings everytime they login
    - AKA __mandatory profile__

### Setting Up Profile
- 1 way is to 1st create generic acc on server with desired desktop config
    - then copy `Ntuser.dat` to `/Users/Default` folder in server 2016
- to create roaming profile, setup generic acc & customise desktop
    - setup those users to access profile by opening profile tab in ea user's acc properties
    - enter path to profile


Summary
---
![](https://i.imgur.com/7rCI11h.png)





###### tags: `SMW` `DISM` `School` `Notes`