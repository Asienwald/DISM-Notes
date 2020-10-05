

NETF Lecture 03 IP Addressing
===




## Table of Contents

- [NETF Lecture 03 IP Addressing](#netf-lecture-03-ip-addressing)
  * [IPv4 Addressing](#ipv4-addressing)
    + [Binary Math](#binary-math)
    + [Converting Binary to Decimal](#converting-binary-to-decimal)
  * [IP Addresses Classes](#ip-addresses-classes)
    + [Address Class Summary](#address-class-summary)
    + [Private IP Address](#private-ip-address)
    + [Classless Interdomain Routing](#classless-interdomain-routing)
  * [Broadcast Domains](#broadcast-domains)
  * [Subnetting](#subnetting)
    + [Calculating Subnet Mask](#calculating-subnet-mask)
    + [Supernetting](#supernetting)
  * [Configuring IPv4 Addresses](#configuring-ipv4-addresses)
    + [Configuring Multiple IP Addresses](#configuring-multiple-ip-addresses)
    + [Configuring Default Gateway](#configuring-default-gateway)
  * [Network Address Translation](#network-address-translation)
    + [Port Address Translation](#port-address-translation)
  * [Internet Protocol Version 6](#internet-protocol-version-6)
    + [IPv6 Address Structure](#ipv6-address-structure)
    + [IPv6 Interface ID](#ipv6-interface-id)
    + [IPv6 Autoconfiguration](#ipv6-autoconfiguration)
    + [Transitioning from IPv4 to IPv6](#transitioning-from-ipv4-to-ipv6)
  * [IPv6 Address Types](#ipv6-address-types)
    + [IPv6 Unicast Addresses](#ipv6-unicast-addresses)
    + [IPv6 Special-Purpose Addresses](#ipv6-special-purpose-addresses)
    + [Multicast Addresses](#multicast-addresses)
    + [Anycast Addresses](#anycast-addresses)
  * [Chapter Summary](#chapter-summary)

IPv4 Addressing
---
- IP addresses - 32bit numbers divided into 4 8bit values __(octet)__
    - ea octet have value from 0 to 255
    - 4 decimal numbers separated by periods in format called __dotted decimal notation__
- subnet masks also 32bit numbers
    - determines how many bits are network ID & how many is host ID
- when written in binary, 1's in subnet mask that correspond to bits in IP address mean matching bit locations part of network ID
![](https://i.imgur.com/KhfaLuN.png)

### Binary Math
- how is subnet mask used to determine network ID?
    - computers determine net ID by doing logical AND operation between its IP & subnet
    - logical AND is op between 2 binary values
![](https://i.imgur.com/QuQr3D0.png)

### Converting Binary to Decimal
- binary digits multiplied by 2 to the power of the position the digit is in
    - right to left


IP Addresses Classes
---
- IP categorised in classes A-E
    - only IP in A, B and C classes available for host assignment
- class A
    - values of 1st octet between 1 and 127
    - IP registry assigns 1st octet, leaving last 3 octets assigned to host
    - intended for large corps & gov
- class B
    - values of 1st octet between 128 & 191
    - IP registry assigns 1st 2 octets, leaving 3rd and 4th octets assigned to hosts
    - intended for use in medium to large networks
- class C
    - value of 1st octet between 192 & 223
    - IP registry assigns 1st 3 octets
    - networks limited to 254 hosts per network
    - intended for small networks
- class D
    - 1st octet between 224 and 239
    - reserved for multicasting
- class E
    - 1st octet between 240 and 255
    - reserved for experimental use & can't be used for address assignment

### Address Class Summary
![](https://i.imgur.com/IUZcGqv.png)


### Private IP Address
- due to poppularity of TCP/IP & internet, running out of unique IP addresses
- series of addresses reserved for private networks
    - networks whose hosts can't be accessed directly through internet
- reserved addresses
    - class A addresses beginning with 10
        - not used a lot
    - class B address from 172.16 to 172.31
    - class C address from 192.168.0 to 192.168.255
    - address in these ranges can't be routed across internet
- another type of address is __link-local address__
    - not assigned manually or through DHCP
    - assigned automatically when computer configured to receive an IP through DHCP but no DHCP service available
    - AKA __automatic private IP addressing (APIPA)__
    - assigned in range 169.254.1.0 through 169.254.254.255 with subnet of 255.255.0.0

### Classless Interdomain Routing
- __classless interdomain routing (CIDR)__ - use of IP without requiring default subnet mask
- use of IP with their default subnets referred to __classful addressing__
- with CIDR, can assign IP of 172.31.210.10 with subnet of 255.255.255.0
    - 172.31.210.0 is net ID & .10 is host ID

__CIDR Notation__
- uses format A.B.C.D/n where n is num of 1bits in subnet
    - Eg. 172.31.210.10 with 255.255.255.0 subnet is 172.31.210.0/24
    - net ID is 24bits, leaving 8 bits for host ID


Broadcast Domains
---
- __broadcast domains__ - which devices must receive packet that's broadcast by any other device
- broadcast is packet addresses to all computers in network
- TCP/IP comm relies heavily on broadcast packets
    - DHCP & ARP use broadcasts to perform tasks

Subnetting
---
- subnetting - process that reallocates bits from IP address's host portion to network portion, creating multiple smaller address spaces
- reasons to subnet
    - divide very large network into many smaller subnetworks
    - conserve IP
    - divide network into smaller groups

### Calculating Subnet Mask
- to divide large network into smaller subnets, follow this process
    - decide how many subnets you need
        - ea router interface indicates required subnet
    - decide how many bits you need to meet/exceed num of required subnets
    - use formula 2^n, n rep num of bits must reallocate from host ID to net ID
    - num of subnets you create always a power of 2 so if need 60 subnets, must reallocate 6 bits (2^6 = 64)
        - reallocating 5 bits only gives 32 subnets
    - reallocate bits from host ID, starting from most significant host bit
        - from left side of host ID
    - must ensure that have enough host bits available to assign to comps on ea subnet
        - to determine num of host addresses available, use formula 2^n -2 with n rep num of host (0) bits in subnet

__Pattern__
![](https://i.imgur.com/ThQ2h6N.png)
![](https://i.imgur.com/TVuVUoD.png)

__Determining Host Address__
![](https://i.imgur.com/ecmPusC.png)

__Calculating subnet based on needed host addresses__

### Supernetting
- supernetting sometimes ncessary to solve certain net config problems & to make routing tables more streamlined
- sometimes AKA __route aggregation__ or __route summarisation__
- reallocates bits from network portion of IP to host portion
    - make 2 or more smaller subnets a larger supernet


Configuring IPv4 Addresses
---
- rules for IP assignment
    - host can be assigned only class A, B or C address
    - every IP config must have subnet mask
    - all hosts on same phy network must share same net ID in their IP
    - all host IDs on same net must be unique
    - can't assign IP in which all host ID bits are binary 0
        - or all 1
    - comps assigned diff net IDs can comm only if router present to forward packets
    - default gateway address assigned to computer must have same net ID as that comp

### Configuring Multiple IP Addresses
- Windows allow assigning multiple IP to single net connection, via advanced TCP/IP settings dialog box
- multiple IP can be useful when
    - comp hosting service that must be accessed using diff addresses
    - comp connected to physical network that hosts multiple IP networks

### Configuring Default Gateway
- __default gateway__ almost always used in IP configs
- must have same net ID as host's net ID
- multiple gateways can be configured
- windows selects gateway with best metric automatically
    - __metric__ is value assigned to gateway based on speed of interface used to access gateway
![](https://i.imgur.com/WsoZMLd.png)


Network Address Translation
---
- NAT allows org to use private IP while connected to internet
- NAT process translates workstation's private address (as packet leaves corporate network) into valid public internet address
    - when data returns to workstation, address translated back to original private address
    - nat usually handled by network device connected to internet, like router
    - address translation kept track of in NAT table
![](https://i.imgur.com/CU1OEtb.png)

### Port Address Translation
- PAT 
    - allows several hundred workstations to access internet with single public internet address
    - ea packet contains src & dest IP along with src & dest port nums
    - single public IP used for all workstation but diff src prot nums used for ea comm session
![](https://i.imgur.com/M5K2iBz.png)


Internet Protocol Version 6
---
- IPv4 developed more than 40 years ago & address space getting used up
    - IPv6 replace IPv4
- IPv6 have built-in hierarchy & fields with distinct purpose
- methods developed to allow IPv4 & IPv6 networks to coexist & comm with 1 another
- Overview
    - originally named IPng (IP next gen)
    - created in 1994 by Internet Engineering Task Force (IETF)
    - includes following improvements
        - larger address space
        - hierarchical address space
        - autoconfig
        - built-in quality of server (QoS) support
        - built-in support for security
        - support for mobility
        - extensibly

### IPv6 Address Structure
- subnetting done in IPv4 not applicable
- uses 128bits instead of IPv4's 32bits for address
- IPv6 addresses written as 8 16bit hex nums separated by colons
    - Eg. Fe80:0:0:0:18ff:0024:8e5a:60
    - __Note__
        - 1 or more consecutive 0s can be written as double colon, but only 1 double colon can exist in an IPv6 address
        - leading 0s optional
        - hex nums easier to convert to bin

### IPv6 Interface ID
- interface ID of IPv6 typically 64bits & uses interface's 48bit MAC address for large portion of address and 16bit value of FE-FE that's inserted after 1st 24bits of MAC
- 1st 2 0s in MAC replaced with 02
- this autoconfigured 64bit host ID referred to as __extended unique identifier (EUI)-64 interface ID__
- IPv6 address entered manually in interface's properties dialog box

### IPv6 Autoconfiguration
- occurs by 2 methods
    - __stateless autoconfiguration__ - node listens for router advertisement messages from local router
    - __stateful autoconfiguration__ - node uses autoconfig protocol, such as DHCPv6 to obtain its IPv6 address & other config info

### Transitioning from IPv4 to IPv6
- __dual IP layer architecture__ - both IPv4 & IPv6 share other components of stack
    - started with Windows Server 2008 & Vista
- tech to help ease transition to IPv6
    - dual IP arch
    - IPv6-over-IPv4 tunneling
    - Intra-Site Automatic Tunnel Addressing Protocol (ISATAP)
    - 6to4
    - Teredo


IPv6 Address Types
---
- IPv6 defines following address types
    - unicast
    - multicast
    - anycast
- unicast & multicast addresses in IPv6 perform much like IPv4 counterparts
    - with few exceptions

### IPv6 Unicast Addresses
- unicast address specifies single interface on device
- 3 primary types of unicast addresses
    - __link-local__ - addresses starting with fe80 are self-configuring & can't be routed
        - used for comp-to-comp comm
    - __unique-local__ - addresses starting with fc or fd that are for use behind firewall & are preconfigured on routers
    - __global__ - accessible on public internet & can be routed

### IPv6 Special-Purpose Addresses
- __loopback address__ - equivalent to 127.0.0.1 used in IPv4 written as ::1
- __zero address__ - used as placeholder in src address field of outgoing IPv6 packet & written as ::
- documentation - global unicast address 2001:b8::/32 reserved for use in books & other doc discussing IPv6
- __IPv4 to IPv6 transition__ - several address prefixes used for transitioning from IPv4 to IPv6

### Multicast Addresses
- same func as counterpart in IPv4

### Anycast Addresses
- can be assigned to multiple interfaces on diff nodes
    - recognised as anycast addresses only be devices that use them
    - assigned on routers used to allow other IPv6 nodes to deliver packets to nearest router on subnet
- don't have special format


Chapter Summary
---
![](https://i.imgur.com/idvQtYd.png)
![](https://i.imgur.com/giQKygB.png)
![](https://i.imgur.com/m3rlEVX.png)



###### tags: `NETF` `DISM` `School` `Notes`