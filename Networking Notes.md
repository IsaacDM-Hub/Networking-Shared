# Networking Notes


## DAY1 
### OSI Model
```
1. Application level Protocol - HTTP, HTTPS, SSH, Telnet, DNS, etc.
2. Presentation - File formatting, Encryption, Code Translation
3. Session - NetBIOS, Named Pipe, RPC, RTP
4. Transport - TCP and UDP
5. Network - IPV4 and IPV6
6. Data Link - LAN, MAN, WAN
7, Pyhsical - Radio waves, Fiber, Phone, Coax
```

## Protocol Data Unit (PDU)
```
Sessions-Application = Data
Transport = Segment/Datagram
Network = Packet
Data Link = Frame
Physical = Bit
```

## Internet Standard Org
```
IETF - RFC's
IANA - Inernet Numbers
IEEE - LAN/WAN electrical Standard
```

## Communcation and tech
### Binary
```
Base2 - Two symbols ( 0 and 1 )

Place Values - 27=128, 26=64, 25=32, 24=16, 23=8, 22=4, 21=2, 20=1

Format - 01000010 01100001 01110011 01100101

Groupings: bit, nibble, byte, half-word, word
```
### Decimal 
```
Base10 - Ten symbols ( 0 to 9 )

Place Values - 103=1000, 102=100, 101=10, 100=1

Format - 7, 66, 115, 1012
```
### Hexadecimal 
```
Base16 - Sixteen symbols ( 0 to 9 and A to F )

Place Values - 23=8, 22=4, 21=2, 20=1

Format - 0x42 0xE3 0x73 0xA5
```
### Base64
```
Base64 - 64 symbols ( A-Z, a-z, 0-9, +, / )

Place Values - 25=32, 24=16, 23=8, 22=4, 21=2, 20=1

Uses ( = ) to represent a null value (max of 2)

Format - MTI=, MTIzNA==, MTIzNDU2Nzg=, QmFzZSA2NA==
```

## Lan Topologies and Devices
### Topolgies
```
Bus - Data will stop at every workstation until it reaches its destination

Star - Everyone is connected to a single point that distributes information

Ring - 1 way everyone connected 

Mesh - Full and Partial. Full everyone is connected directly. Partial Multiple people connected but not every station

Wireless - Like a Star but everyone can connect within the radius 

Hierarchial - Like DOD or large organizations
```

### Devices
```
Hubs

Repeaters

Switches

Routers
```

### Ethernet Timing (BIT-TIME)
```
Speed        Bit-Time
10 Mbps      100ns
100 Mbps     10ns
1 Gbps       1ns
10 Gbps      .1ns
100 Gbps     .01ns
```

## OSI Layer 2 Protocols
### LAN TECH (Benefits and Hindrances)
```
Technology	Standard

Ethernet    802.3(x)

Wireless    802.11(x)

Token Ring    802.5
```
### Data Link Sub-Layers
```
MAC - Medium Access Control
LLC - Logical Link Control
```

### Message Formatting
```
Header - Layer 2 - 7
Data - Payload
```
### ENCAPSULATION AND DECAPSULATION
```
How data moves through the layers
```

## Switch Operation
```
Building MAC-Address (CAM) Table

Learns by reading Source MAC addresses

Forwarding Frames

Decision based on Destination MAC address

```
### Switching Modes
```
Cut-Through = Gets to the information as fast as possbile. 

Fragment-Free = Checks entire packet to enusre the data is all there

Store-and-Forward = Store everything, then forward the entire frame to the other side
```
## CAM Table Overflow Attack 
```
Send frames with bogus source MAC address to switch

Cause switch to fill table with bogus addresses

Switch will not be able to learn new (valid) MAC addresses
```
## Describe MAC Addressing 
```
Length: 48-bit | 6 byte | 12 Hex

Format:

Windows: 01-23-45-12-34-56

Unix/Linux: 01:23:45:12:34:56

Cisco: 1234.5612.3456

Parts:

OUI - First 24-bits assigned by IANA

Vendor Assigned - Last 24-bits assigned by vendor
```
### MAC Adress Types
```Unicast: One to one

8th bit is off

Multicast: One to many

8th bit is on

Broadcast: One to all

All bits on

```
### MAC Spoofing 
```
Could not be changed at first

Used to be called:

hardware

firmware

burned-in

Now it can be changed w/ software
```
## Layer 2 Ethernet
### VLAN Types 
```
Default - VLAN 1 -  If you see a Ethertype is anything other than 08 00, then it is a vlan 

Data - User traffic

Voice - VOIP traffic

Management - Switch and router management

Native - Untagged switch and router traffic

802.1Q and 802.1AD Vlan Headers 
```

### VLAN Hopping Attack 
```
Switch Spoofing (DTP)

Single Tagging

Double Tagging (using native VLAN)
```

## ARP
### ARP Types
```
ARP (OP 1 and 2)

RARP (OP 3 and 4) - Reply

Proxy ARP (OP 2)

Gratuitous ARP (OP 2) - Didn't ask for a reply
```
### ARP Cache
```
All resolved MAC to IP resolutions

If MAC is not in cache then ARP is used

Dynamic entries last from 2-20 minutes

Default gateway is present at minimum

Can be easily duped by attackers
```

### Man-In-The-Middle With ARP
```
Poison ARP Cache with:

Gratuitous ARP

Proxy ARP
```
## VLAN TRUNKING PROTOCOL (VTP)
```
Dynamically add/remove/modify VLANs


Cisco proprietary

Modes:

Server

Client

Transparent
```
### VTP VULNERABILITY 
```
Can cause switches to dump all VLAN information

Cause a DoS as switch will not support configured VLANS
```

## DYNAMIC TRUNKING PROTOCOL (DTP)
```
Used to dynamically create trunk links


Cisco proprietary

Modes:

Dynamic-Auto

Dynamic-Desirable
```

### DYNAMIC TRUNKING PROTOCOL (DTP) VULNERABILITY
```
On by default

Can send crafted messages to form a VLAN trunk link

Recommend to:

Disable DTP negotiations

Manually assign as Access or Trunk
```

## CDP(Cisco Discovery Protocol), FDP, AND LLDP
```
Cisco Discovery Protocol (CDP)

Foundry Discovery Protocol (FDP)

Link Layer Discovery Protocol (LLDP)

```
### CDP, FDP, AND LLDP VULNERABILITY
```
Leaks valuable information

Clear Text

Enabled by default

Disable it:

Globally

Per interface

May require it for VOIP
```
## SPANNING TREE PROTOCOL (STP)
```
Root decision process

Elect root Bridge

Identify the Root ports on non-root bridge

Identify the Designated port for each segment

Set alternate ports to blocking state

Convergence Times is the time it takes for a switch to talk to another switch to give directions to root
```


### SPANNING TREE PROTOCOL (STP) TYPES
```
802.1D STP

Per VLAN Spanning Tree + (PVST+)

802.1w – Rapid Spanning Tree Protocol (RSTP)

Rapid Per VLAN Spanning Tree + (RPVST+)

802.1s (Multiple Spanning Tree)
```
### SPANNING-TREE ATTACK
```
Crafted Bridge Protocol Data units (BPDU)

Used to perform a DoS or MitM
```
## PORT Security Modes
```
Shutdown (default)

Protect

Restrict


PORT SECURITY CAN HELP TO
Restrict unauthorized access

Limit MAC address learned on port

Prevent CAM Table Overflow attacks

```
### PORT SECURITY VULNERABILITIES
```
Dependant on MAC address

MAC spoofing
```

## Layer 2 Attack Mitigation Techniques 
```
Shutdown unused ports

Enable Port Security

IP Source Guard

Manually assign STP Root

BPDU Guard

DHCP Snooping

802.1x - Way to manage logins and restrict access to logins. Server/Switch will athenticate every user 

Dynamic ARP inspection (DAI)

Static CAM entries

Static ARP entries

Disable DTP negotiations

Manually assign Access/Trunk ports

```
# Day 1 Part 2

## Network Layer
```
Addressing Schemes for Network (Logical Addressing)

Routing

Encapsulation

IP Fragmentation and Reassembly

Error Handling and Diagnostics
```
### Internet Protocols
```
IPv4 (ARPANET 1982)

Classful subnetting

Classless subnetting (CIDR)

NAT

IPv6 (Standardized 2017)

```
### IPV4 
```
Class A (0 to 127)

Class B (128 to 191)

Class C (192 to 223)

Class D (224 to 239) - Multicasting

Class E (240 to 255) - Not used



##################
HEADER INFO
1st- Version -  to tell you what IPVx Version you are seeing
2nd - HL - Tells you the header length
3rd - DSCP - used for QoS to prioritize and manage network traffic
4th - A 2-bit field specified for use with explicit congestion signaling
5th - Total length - says how large the data is including header and data
6th - Identification - Individualizes every IP packet from any other.
7th - Flags - To identify if there has been Fragmentation of the data - 3 flags (reserve, don't fragment, more fragment)
8th - Fragment Offset - Incrementing number (first frag packet will have offset of 0)
9th - Time To Live - How many times your packet can hop on the network before it is dropped
10th - Protocol - No used in this header but lets you know what the next header is (TCP UDP)
11th - Header Checksum - Allows our packet to tell the other side what the whole packet is supposed to look like, the recieving side will check if that is correct
12th - Source IP
13th - Destination IP
##################
```
#### Subnetting 
```
IP addresses:

Network Portion

Host Portion

Practice of "borrowing" host bits and used them as subnet bits.
```

#### Identify IPV4 Address types
```
Unicast

  Any Class A thu C

Multicast

  Class D

Broadcast

  Any IP were the host portion is all on

```


#### IPV4 Address scopes
```
Public

Private (RFC 1918)

Loopback (127.0.0.0/8)

Link-Local (APIPA)

Multicast (class D)
```

#### IPV4 Fragmentation
```
Maximum Transmission unit MTU)
Breaking up packets from higher MTU to lower MTU network

Performed by routers

MF flag is on from 1st until 2nd to last

Offset is on from 2nd until the last

Offset = (MTU - (IHL x 4)) ÷ 8

```

#### IPV4 Auto Configuration
```
APIPA

169.254.0.0/16

RFC 3927

DHCP

DORA process

RFC 1531

```


### IPV6
```
IPv6 does not support fragmentation within it’s header

Routers do not fragment IPv6 packets

Source adjusts MTU to avoid fragmentation

Source can use IPv6 fragmentation extension header
```
### FRAGMENTATION VULNERABILITY
```
Can use fragmentation overlaps to avoid firewall detection

Attack depends on how OS deals with overlap

Example: Teardrop attack

```



#### IPV4 AUTO CONFIGURATION VULNERABILITY
```
Rogue DHCP

Evil Twin

DHCP Starvation

```

## OS FINGERPRINTING WITH TTL
```
Vendors have chosen different values for TTL which can provide insight to which OS family a generated packet is from.
Operating System            IP Initial TTl          TCP Window Size

Linux (kernal 2.4-2.6)            64                      5840
Google Customized Linux           64                      5720
FreeBSD                           64                      65535
Windows XP                        128                     65535
Windows 7, Vista, Server          128                     8192
Cisco Router                      255                     4128
```

## ICMP Protocol
```
ICMP is used to provide feedback about network problems that may or do prevent packet delivery. This protocol was designed to provide error reporting, flow control and first-hop gateway redirection. While IP and UDP are unreliable, it is still important to have a way to notify the sender if something goes wrong in a transmission. TCP is able to realize and react when packets aren’t being delivered, but ICMP provides a method for discovering more serious problems like "TTL exceeded" or "need more fragments."

Echo Request (Type 8):

  Sent by a device to request an Echo Reply from another device.

  Often used by the "ping" utility to test network connectivity and measure round-trip time.

  Depending on the operating system Echo Requests (PING) can have different packet sizes and default payloads.

    Linux:

      Default size: 64 bytes (16 byte ICMP header + 48 byte payload)

      Payload message: !\”#\$%&\‘()*+,-./01234567

    Windows:

      Default size: 48 bytes (16 byte ICMP header + 32 byte payload)

      Payload message: abcdefghijklmnopqrstuvwabcdefghi

Echo Reply (Type 0):

  Sent by a device in response to an Echo Request.

  Contains the same payload as the original Echo Request and is used to confirm network connectivity.

Destination Unreachable (Type 3):

  Destination Network Unreachable (Code 0):

    Indicates that the network hosting the destination address is unreachable.

    This can occur if there is no route to the destination network in the routing table.

Destination Host Unreachable (Code 1):

  Indicates that the specific destination host is unreachable.

  This can occur if there is no route to the destination host in the routing table or if the destination host is down.

Destination Protocol Unreachable (Code 2):

  Indicates that the transport protocol specified in the packet’s header is not supported by the destination.

  For example, if a UDP packet is sent to a destination that does not have a process listening on the specified UDP port, this error may be generated.

Destination Port Unreachable (Code 3):

  Indicates that the specified port on the destination host is unreachable.

  This typically occurs when there is no process listening on the specified port or if a firewall is blocking access to the port.

Fragmentation Needed and Don’t Fragment was Set (Code 4):

  Indicates that the packet is too large to be transmitted without fragmentation, but the Don’t Fragment (DF) flag is set in the packet’s header.

  This error is generated to inform the sender that the packet needs to be fragmented to be transmitted successfully.

Source Route Failed (Code 5):

  Indicates that the source route specified in the packet’s header is invalid.

  Source routing allows the sender to specify the route that the packet should take through the network, but if the specified route is invalid, this error may be generated.

Destination Network Unknown (Code 6):

  Indicates that the destination network is unknown.

  This error typically occurs when the destination network is not listed in the routing table.
  
Destination Host Unknown (Code 7):

  Indicates that the destination host is unknown.

  This error typically occurs when the destination IP address is not reachable or is not assigned to any host.

Source Host Isolated (Code 8):

  Indicates that communication with the source host is administratively prohibited.

  This error is generated by a router or firewall to indicate that the source host is isolated or not allowed to communicate with the destination.

Communication with Destination Network Administratively Prohibited (Code 9):

  Indicates that communication with the destination network is administratively prohibited.

  This error typically occurs when access to the destination network is restricted by network policies or firewall rules.

Communication with Destination Host Administratively Prohibited (Code 10):

  Indicates that communication with the destination host is administratively prohibited.

  This error typically occurs when access to the destination host is restricted by network policies or firewall rules.

Network Unreachable for Type of Service (Code 11):

  Indicates that the network is unreachable for the specified type of service.

  This typically occurs when the network does not support the requested type of service or quality of service.

Host Unreachable for Type of Service (Code 12):

  Indicates that the destination host is unreachable for the specified type of service.

  This typically occurs when the destination host does not support the requested type of service or quality of service.

Communication Administratively Prohibited (Code 13):

  Indicates that communication with the destination is administratively prohibited.

  This can occur due to network policies or firewall rules that explicitly block communication with the destination.

Redirect (Type 5):

  Used by routers to inform hosts of a better route to a particular destination.

  Informs the host to update its routing table with the new route information.

    Redirect Datagram for the Network (Code 0): This code indicates that the router has a better route to the destination network and is redirecting the packet to the sender’s specified gateway. It          instructs the sender to update its routing table with the new gateway information.

    Redirect Datagram for the Host (Code 1): This code indicates that the router has a better route to the destination host and is redirecting the packet to the sender’s specified gateway. It instructs      the sender to update its routing table with the new gateway information.

    Redirect Datagram for the Type of Service and Network (Code 2): This code is similar to Code 0 but also includes a Type of Service (ToS) component. It indicates that the router has a better route to     the destination network with a specific Type of Service and is redirecting the packet accordingly.

    Redirect Datagram for the Type of Service and Host (Code 3): This code is similar to Code 1 but also includes a Type of Service (ToS) component. It indicates that the router has a better route to 
    the destination host with a specific Type of Service and is redirecting the packet accordingly.

Time Exceeded (Type 11):

  Indicates that a packet’s Time-to-Live (TTL) value has reached zero or that the packet’s hop limit has been exceeded.

  Subtypes of Time Exceeded include:

    Time to Live Exceeded in Transit (Code 0): Indicates that the TTL of the packet expired while in transit.

    Fragment Reassembly Time Exceeded (Code 1): Indicates that the time allowed for reassembly of fragments has expired.

Timestamp Request (Type 13):

  Sent by a device to request a Timestamp Reply from another device.

  Used to measure round-trip time and clock synchronization between devices.

Timestamp Reply (Type 14):

  Sent by a device in response to a Timestamp Request.

  Contains timestamps indicating the time the request was received and the time the reply was sent.

```


### ICMPV4 OS FINGERPRINTING
```
Linux:

  Default size: 64 bytes

  Payload message:

    !\”#\$%&\‘()*+,-./01234567
Windows:

  Default size: 40 bytes

  Payload message:

    abcdefghijklmnopqrstuvwabcdefghi
```

### ICMPV4 TRACEROUTE
```
Identifies hops between the source and destination

Uses incrementing TTLs

Hops return an ICMP Type 11 Time exceeded message when TTL reaches zero

Continues until it reaches target or 30 hops*

Can use various protocols and ports
  ICMP (windows default)

  UDP (linux default)

  TCP
```

### ICMPV4 TRACEROUTE LINUX
```
Default:
  traceroute 172.16.82.106
  traceroute -U 172.16.82.106

Requires root:

  sudo traceroute -I 172.16.82.106
  sudo traceroute -T 172.16.82.106
  sudo traceroute -T 172.16.82.106 -p 443
```

#### ICMPV4 ATTACKS
```
Firewalking (traceroute)

Oversized ICMP messages

ICMP Redirects

SMURF Attack

Map network w/ IP unreachables

ICMP Covert Channels
```



## IPV6
```
IPv6 Addressing

  128 bit address

  64-bit Prefix (4 hextets)

  64-bit Interface ID (4 hextets)

  340 undecillian addresses
```
### IPV6 SUBNETTING
```
Organizations asigned a 48-bit Prefix by IANA

Last 16-bits of prefix is used for subnetting

Allows for upto 65,536 subnets to be created
```
### IPV6 REPRESENTATION
```
2001:ABCD:1234:DEF0:1111:2222:3333:4444

  128-bit (64bit Prefix and 64bit Int ID)

  Represented using 32 Hex digits

  Hextet: 4 hex separated by (:)

Can shorten consecutive 0’s with (::)
2001:0000:0000:0001:0000:0000:0000:0001
Can only use it once


2001:0:0:1::1
```
### IPV6 ADDRESS TYPES
```
Unicast

Multicast

Anycast

```

### IPV6 ADDRESS SCOPES 
```
Global Unicast Addresses (2000::/3)

Unique Local (fc00::/7)

Loopback (::1/128)

Link-Local (fe80::/10)

Multicast (ff00::/8)
```

### IPV6 ZERO CONFIGURATION (LINK-LOCAL)
```
Hosts generate link-local prefix (FE80::/8)

Interface ID can be:
  Random (Windows default)
  EUI-64 (nix* and Cisco default)

#######################################
IPV6 ZERO CONFIGURATION (GLOBAL)
#######################################

Hosts requests global prefix
  SLAAC (RFC 4862) (default)
  DHCPv6 (configured)

Interface ID can be:
  EUI-64 (nix* and Cisco default)
  Random (Windows default)
```
### IVP6 ZERO CONFIGURATION (EUI-64 LINK-LOCAL) 
```
MAC: fa:16:3e:c3:68:f2

Append: ff:fe between OUI and Vendor assigned

Flip 7th bit

Result: FE80::f816:3eff:fec3:68f2

#######################################
IPV6 ZERO CONFIGURATION (EUI-64 GLOBAL)
#######################################

Prefix from RA: 2001:ABCD:1234:DEF0::

MAC: fa:16:3e:c3:68:f2

Append: ff:fe between OUI and Vendor assigned

Flip 7th bit

Result: 2001:ABCD:1234:DEF0:f816:3eff:fec3:68f2
```


### IPV6 ZERO CONFIGURATION (RANDOM)
```
Prefix from RA: 2001:ABCD:1234:DEF0::

Link-Local: FE80::cdc3:b3ac:1623:f552

Global: 2001:ABCD:1234:DEF0:182f:dd86:f2be:653b
```


### IPV6 ZERO CONFIGURATION VULNERABILITY
```
SLAAC MitM

Can be used to figerprint OS

Rogue DHCP

Evil Twin

DHCP Starvation
```

## NEIGHBOR DISCOVERY PROTOCOL (NDP)
```
Router Solicitation (Type 133)

Router Advertisement (Type 134)

Neighbor Solicitation (Type 135)

Neighbor Advertisement (Type 136)

Redirect (Type 137)
```


## INTERNETWORKING ROUTING METRICS
```
RIP: Hop

EIGRP: Bandwidth, Delay, Load, Reliability

OSPF: Cost

BGP: Policy
```

## AUTONOMOUS SYSTEMS
```
Definition:

Collection of connected Internet Protocol routing prefixes under the control of one or more network operators on behalf of a single administrative entity or domain,
that presents a common and clearly defined routing policy to the Internet.

16 or 32-bit Number
  AS109   CISCO-EU-109 Cisco Systems Global ASN
  AS193   FORD-ASN - Lockheed Martin Western Development Labs
  AS721   DoD Network Information Center Network
  AS3598  MICROSOFT-CORP-AS - Microsoft Corporation
  AS15169 GOOGLE - Google Inc.

```


## CLASSFUL VS CLASSLESS
```
CLASSFUL - RIP, ERIGP
CLASSLESS - OSPF, BGP
```

## ROUTING PROTOCOL VS ROUTED PROTOCOL
```
ROUTING - USED BETWEEN ROUTERS TO TALK TO EACH OTHER

ROUTED - USED BY ROUTERS TO DIRECT USER TRAFFIC
```


## ROUTING PROTOCOL VULNERABILITIES
```
Distributed Denial of Service (DDOS)

Packet Mistreating Attacks (PMA)

Routing Table Poisoning (RTP)

Hit and Run DDOS (HAR)

Persistent Attacks (PA)
```

## BGP
```
Road-map of the Internet

Routes traffic between Autonomous System (AS) Number

Advertises IP CIDR address blocks

Establishes Peer relationships

Complicated configuration

Complicated and slow path selection
```

### BGP OPERATION
```
How BGP chooses the best path:

Advertise a more specific route. 192.168.1.0 /24 is more specific than 192.168.0.0 /16.

Offer a shorter route to certain blocks of IP addresses.

A route to ip prefix with 4 AS 'hops" is better than route with 5 AS 'hops'
```

### BGP HIJACKING
```
Illegitimate advertising of addresses

BGP propagates false information

Purpose:

stealing prefixes

monitoring traffic

intercept (and possibly modify) Internet traffic

'black holing' traffic

perform MitM
```

### BGP HIJACKING DEFENSE
```
IP prefix filtering

BGP hijacking detection

Tracking the change in TTL of incoming packets

Increased Round Trip Time (RTT) which increases latency

Monitoring misdirected traffic (change in AS path from tools like Looking Glass)

BGPSec
```

## FHRP ATTACK
```
Intercept the FHRP message exchange

Inject manipulated messages

MitM by becoming active forwarder
```


## FIRST HOP REDUNDANCY PROTOCOL
### HOT STANDBY ROUTER PROTOCOL (HSRP)
```
Provides default gateway and a backup router
```

### VIRTUAL ROUTER REDUNDANCY PROTOCOL (VRRP)
```
Open standard to Cisco's HSRP, Same Functionality
```

### Gateway Load Balancing protocol (GLBP)
```
Supports arbitray load balancing in addition to redundancy across gatewats, cisco proprietary
```


# Day 2
## Layer 4 Ports
## 11 IS UDP AND 06 IS TCP AND 01 IS ICMP
### Transport Layer Protocols
```
Connection-oriented

  TCP - Segments

  Unicast traffic

Connection-less

  UDP - Datagrams

  Broadcast, Multicast, or Unicast Traffic
```

### Port Ranges
```
Ranges          Category

0-1023          Well-known(system)
1024-49151      Registered(user)
49152-65535     Dynamic(Private)
```
### TCP RELIABILITY
```
1. Connection establishment

  1. 3-way handshake

2. Data Transfer

  1. Established phase

3. Connection Termination

  1. 4-way Termination

  2. Reset connection
```
### TCP HEADERS

```
1. SRC PORT
2. DST PORT
3. SUQEUENCE NUMBER - For the system to see which part of the data it is looking at
4. ACKNOWLEDGMENT NUMBER - Checks to see if syn/ack match up to verify correct stream
5. OFFSET - lets you know the size of the TCP Header
6. RESERVED - Should never be used and at 0
7. TCP FLAGS - A bit toggled in this field to display syn, syn/ack, ack
8. WINDOW - Information from the host to tell the other side how much information it can host
9. CHECKSUM - Checks data
10. URGENT POINT -  if you have the URG flag set
11. OPTIONS - Not applicable to this course
```
### TCP FLAGS
```
URG
ACK
PSH
RST
SYN
FIN

TCP Flag Breakout (Binary and Hex)

0X02  SYN
0X12  SYN, ACK
0X10  ACK

ACK    SYN
 0      1
 1      1
 1      0

Collection of Exceptionally Unskilled Attackers Pester Real Security Folks

Coach Explained to the University of Alaska to Play Really Snowy Football
```
### UDP HEADERS
```

1. SRC PORT
2. DST PORT
3. LENGTH
4. CHECKSUM
```

## LAYER 5 PROTOCOLS AND HEADER
### VPN
```
Types:

  Remote Access(client-to-site)

  Site-to-Site
```
### L2TP (UDP 1701)
```
RFC 2661

Origins from Cisco L2F and Microsoft PPTP

Tunnel only. No Encryption
```

### PPTP (TCP 1723)
```
RFC 2637

Microsoft

Provides encryption

Obsolete with many vulnerabilities
```

### L2F (UDP 1701)
```
Cisco

Tunnel only. No Encryption

Requires L2F Network Server (LNS) and a L2F Access Concentrator (LAC)
```

### IPSEC (A SUITE OF MULITPLE THINGS TO PROVIDE ENCRYPTION)
```
Modes: Transport or Tunnel

Headers:

  ESP (protocol 50)

  AH (protocol 51)

  IKE (UDP port 500 or 4500)
```
### OPENVPN
```
Open source

Uses OpenSSL for encryption

UDP*/TCP port 1194
```
### PROXY - SOCKS 4/5 (TCP 1080)
```
RFC 1928

Uses various Client / Server exchange messages

  Client can provide authentication to server

  Client can request connections from server
```
#### SOCKS4
```
No Authentication

Only IPv4

No UDP support

No Proxy binding. Client’s IP is not relayed to destination.
```

#### SOCKS5
```
Various methods of Authentication

IPv4 and IPv6 support

UDP support

Supports Proxy binding. Client’s IP is relayed to destination.
```

### NETWORK BASIC INPUT OUTPUT SYSTEM (NETBIOS) PROTOCOL
```
TCP 139 and UDP 137/138

Name Resolution (15 characters)

Largely replaced by DNS
```
### SMB/CIFS (TCP 445)
```
SMB Rides over Netbios

  Netbios Dgram Service - UDP 138

  Netbios Session Service - TCP 139

  SAMBA and CIFS are just flavors of SMB
```

### RPC (ANY PORT)
```
Allows a program to execute a request on a local/remote computer

Hides network complexities

XML, JSON, SOAP, and gRPC

User application will:

  Request for information from external server

  Receives the information from the external server

  Display collected data to User
```
### API
```
Framework of rules and protocols for software components to interact.

Methods, parameters, and data formats for requests and responses.

REST and SOAP
```

## OSI LAYER 6
### RESPONSIBILITIES
```
Translation

Formating

Encoding (ASCII, EBCDIC, HEX, BASE64)

Encryption (Symmetric or Asymmetric)

Compression
```

## OSI LAYER 7 
### TELNET (TCP 23)
```
Remote Login

Authentication

Clear Text

Credentials susceptible to interception
```
### SSH (TCP 22)
```
Messages provide:

  Client/server authentication

  Asymmetric or PKI for key exchange

  Symmetric for session

  User authentication

  Data stream channeling
```
#### COMPONENTS OF SSH ARCHITECTURE
```
Client / Server / Session

Keys

User Key - Asymmetric public key used to identify the user to the server

Host Key - Asymmetric public key used to identify the server to the user

Session Key - Symmetric key created by the client and server to protect the session’s communication.

```

#### SSH IMPLEMENTATION CONCERNS AND USAGE 
```
Using password authentication only

Key rotation

Key management

Implementation specification (libssh, sshtrangerthings)



$ ssh {user}@{ip}

$ ssh student@172.16.82.106

-p {port} - Alternate port
-l {username} - Specify the username
-X - Enable X11 forwarding
-v(vv) - Add logging and debugging
-i {identity file} - Specify a private key identity
-F {config file} - Specify an alternate user config file
-N - Do not send remote commands
-T - Do not create a pseudo vty
-C - Enable compression
-f - Backgroud process after authentication
-J user@host - Proxy jump
-L [bind_address:]port:host:hostport
-R [bind_address:]port:host:hostport
-D {port}
```
##### SSH FIRST CONNECT AND RE-CONNECT 
```
student@internet-host:~$ ssh student@172.16.82.106
The authenticity of host '172.16.82.106 (172.16.82.106)' can't be established.
ECDSA key fingerprint is SHA256:749QJCG1sf9zJWUm1LWdMWO8UACUU7UVgGJIoTT8ig0.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '172.16.82.106' (ECDSA) to the list of known hosts.
student@172.16.82.106's password:
student@blue-host-1:~$

You will need to approve the Server Host (Public) Key

Key is saved to /home/student/.ssh/known_hosts



ssh student@172.16.82.106
student@172.16.82.106's password:
student@blue-host-1:~$

Further SSH connections to server will not prompt to save key as long as key does not change
```

##### SSH HOST KEY CHANGED AND FIX
```
ssh student@172.16.82.106
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:RO05vd7h1qmMmBum2IPgR8laxrkKmgPxuXPzMpfviNQ.
Please contact your system administrator.
Add correct host key in /home/student/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /home/student/.ssh/known_hosts:1
remove with:
ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
ECDSA host key for 172.16.82.106 has changed and you have requested strict checking.
Host key verification failed.

####################################
SSH KEY CHANGE FIX

ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
Copy/Paste the ssh-keygen message to remove the Host key from the known_hosts file

When you re-connect it will prompt you to save the new Host key
```
#### SSH FILES
```
Known-Hosts Database
  ~/.ssh/known_hosts

Configuration Files
  /etc/ssh/ssh_config
  /etc/ssh/sshd_config
```
#### VIEW/CHANGE SSH PORT
```
To view the current configured SSH port
  cat /etc/ssh/sshd_config | grep Port

Edit file to change the SSH Port
  sudo nano /etc/ssh/sshd_config

Restart the SSH Service
  systemctl restart ssh
```

#### SSH-KEYGEN
```
ssh-keygen -t rsa -b 4096 -C "Student"

Create your own SSH Public/Private keys

  -t Encryption (rsa|dsa|ecdsa|ed25519)

  -b Bit length (1024|2048|4096)

  -C Adds a comment

~/.ssh/id_rsa and ~/.ssh/id_rsa.pub
```
#### SSH-COPY-ID
```
ssh-copy-id student@172.16.82.106

Copies your SSH Public key to the remote server

Saves key to ~/.ssh/authorized_keys on remote server

Allows you to authenticate with server using your key instead of password

Must secure your private key
```

### HTTP(S) (TCP 80/443)
```
User Request methods
  GET / HEAD / POST / PUT

Server response Codes
  100, 200, 300, 400, 500
```

#### HTTP(S) VULNERABILITIES
```
Flooding

Amplification

Low and slow

Drive-By Downloads

BeEF Framework
```

### DNS (TCP/UDP 53)
#### DNS QUERY/RESPONSE
```
Resolves Names to IP addresses

Queries and responses use UDP

DNS response larger than 512 bytes use TCP

  DNS Zone Transfer

  DNS Security
```
#### DNS RECORDS 
```
A - IPv4 record

AAAA - IPv6 record

MX - Mail Server record

TXT - Human-readable text

NS - Name Server record

SOA - Start of Authority
```

### FTP (TCP 20/21)
```
RFC 959

Port 21 open for Control

Port 20 only open during data transfer

Authentication or Anonymous

Clear Text

Modes:

  Active (default)

  Passive
```
#### FTP ACTIVE ISSUES
```
NAT and Firewall traversal issues

Complications with tunneling through SSH

Passive FTP solves issues related to Active mode and is most often used in modern systems
```

### TFTP (UDP 69)
```
Clear-Text

Reliability provided at Application layer

Used by routers and switches to transfer IOS and config files
```

### SMTP (TCP 25)
```
Used to send email

No encryption

SMTP over TLS/SSL (SMTPS)

TCP Ports 587 and 465
```
### POP (TCP 110)
```
Receives email

No sync with server

No encryption

POP3
```
### IMAP (TCP 143)
```
Receives email

Sync with server

No encryption

IMAP4
```

### DHCP (UDP 67/68)
```
-DHCPV4-

DORA
  Discover (Broadcast)
  Offer (Unicast)
  Request (Broadcast)
  Acknowlege (Unicast)


DHCPV6

If Managed flag is set during SLAAC:

  Solicit (Multicast)
  Advertise (Unicast)
  Request or Information Request (Multicast)
  Reply (Unicast)
```
#### DHCP VULNERABILITIES
```
Rogue DHCP

Evil Twin

DHCP Starvation
```

### NTP (UDP 123)
```
Stratum 0 - authoritative time source

Up to Stratum 15

Vulnerable to crafted packet injection
```
### AAA PROTOCOLS
```
Authentication, Authorization, and Accounting

For third party authentication

TACACS (TCP 49) SIMPLE/EXTENDED
RADIUS (UDP 1645/1646 AND 1812/1813)
DIAMETER (TCP 3868)
```
### SNMP (UDP 161/162)
```
Versions:

SNMPv1 - RFC 1157

SNMPv2c - RFC 1441

SNMPv3 - RFC 3410



7 Message Types

  Get Request

  Set Request

  Get Next

  Get Bulk

  Response

  Trap

  Inform
```

#### SNMP VULNERABILITIES
```
v1 and 2c

  Weak Community Strings

  Lack of Encryption

  Information Disclosure

  Can be "sniffed"  
```
### RDP (TCP 3389)
```
Developed by Microsoft (Open Standard)
  No server software needed

Other Proprietary RDP software
  Requires to have 3rd pary software installed
```

### KERBEROS (UDP 88)
```
Secure network authentication protocol

Clients obtain tickets to access services

Mutual authentication

Used by Active Directory
```
### LDAP(S) (TCP 389 AND 636)
```
Client/server model

Hierarchical

Directory schema

Unsecure and secure versions
```

### RTP (UDP ANY ABOVE 1023)

# Day 3
## CAPTURE LIBRARIES
```
Libpcap - https://www.tcpdump.org/

WinPcap - https://www.winpcap.org/

NPcap - https://nmap.org/npcap/
```
## SNIFFING TOOLS AND METHODS
```
Practical Uses:

  Network troubleshooting

  Diagnosing improper routing or switching

  Identifying port/protocol misconfigurations

  Monitor networking consumption

  Intercepting usernames and passwords

  Eavesdrop on network communications


Disadvantages:

  Requires elevate permissions

  Can only capture what NIC can see

  Cannot capture local traffic

  Can consume massive amounts of system resources

  Lost packets on busy networks



########### PACKETS CAN BE CAPTURED IN TWO WAYS:
  Hardware Packet Sniffers

  Software Packet Sniffers
```


 ## SOCKET TYPES
```
User Space Sockets

  Stream socket - TCP

  Datagram socket - UDP

Kernel Space Sockets

  RAW Sockets


CAPTURE LIBRARY
Requires root for:
  Promicious Mode (Listen on all NICs)

  All captured packets are created as RAW Sockets

```


## TYPES OF SNIFFING 
```
Active

Passive
```


## INTERFACE NAMING
```
Traditional:
  eth0, eth1

Consistent:
  eno1, ens3
```


## TCPDUMP PRIMITIVES
```
User friendly capture expressions
  src or dst

  host or net

  tcp or udp


TCPDUMP PRIMITIVE QUALIFIERS
type - the 'kind of thing' that the id name or number refers to
  host, net, port, or portrange

dir - transfer direction to and/or from
  src or dst

proto - restricts the match to a particular protocol(s)
  ether, arp, ip, ip6, icmp, tcp, or udp
```

### TCPDUMP PRIMITIVE EXAMPLES
```
Simple

Extended
```

## BASIC TCPDUMP OPTIONS
```
-A = print payload in ASCII

-D = list interfaces

-d = Dump the compiled packet-matching code in a human readable form (verify)
tcpdump "ether[12:2] = 0x800" -d

-i = specify capture interface

-e = print data-link headers

-X or XX = print payload in HEX and ASCII

-w = write to pcap

-r = read from pcap

-v, vv, or vvv = verbosity

-n = no inverse lookups
```

## LOGICAL OPERATORS
```
Primitives may be combined using:

Concatenation: 'and' ( && )

Alteration: 'or' ( || )

Negation: 'not' ( ! )

< or < =

> or >=

= or !=
```

## COMPARE PRIMITIVES AND BPFS
```
Primitives (macros)

  CMU/Stanford Packet Filter (CSPF) Model commonly called Boolean Expression Tree

  Simple and easy filter expressions

  First user-level packet filter model

  Memory-stack-based filter machine which can create bottlenecks on model CPUs

  can have redundant computations of the same information



Berkley Packet Filters (BPF)

  Control Flow Graph (CFG) Model

  Uses a simple (non-shared) buffer model which can make it 1.5 to 20 times faster than CSPF

  Can be more complex to create expressions but offer far more precision
```
## BERKLEY PACKET FILTER (BPF)
```
Similar in function to primitives

Reduces redudant computations

More complex expressions
```


## CONSTRUCT A BPF


### KERNEL API
```
TCPDUMP requests a RAW Socket creation

Filters are set using the SO_ATTACH_FILTER

SO_ATTACH_FILTER allows us to attach a Berkley Packet Filter to the socket to capture incoming packets.
```

### BERKLEY PACKET FILTERS
```
tcpdump {A} [B:C] {D} {E} {F} {G}

A = Protocol (ether | arp | ip | ip6 | icmp | tcp | udp)
B = Header Byte offset
C = optional: Byte Length. Can be 1, 2 or 4 (default 1)
D = optional: Bitwise mask ( & )
E = Operator ( = | == | > | < | <= | >= | != | () | << | >> )
F = Result of Expression
G = optional: Logical Operator ( && || ) to bridge expressions
```

#### BPF EXAMPLES
```
tcpdump -i eth0 'ether[12:2] = 0x0806'
tcpdump -i eth1 'ip[9] = 0x06'
tcpdump -i eth0 'tcp[0:2] = 53 || tcp[2:2] = 53'
tcpdump 'ether[12:2] = 0x0800 && (tcp[2:2] != 22 && tcp[2:2] != 23)'
```
### BITWISE MASKING
```
BPFs can read 1 (byte), 2 (half-word) or 4 (word)

BPFs alone will only filter to the byte level

Bit-wise masking allow filtering precision to the bit level

Binary (0) to ignore bit

Binary (1) to match bit
```
#### BITWISE MASKING EXAMPLES
```
tcpdump 'ether[12:4] & 0xffff0fff = 0x81000abc'
tcpdump 'ip[1] & 252 = 32'
tcpdump 'ip[6] & 224 != 0'
tcpdump 'tcp[13] & 0x11 = 0x11'
tcpdump 'tcp[12] & 0xf0 > 0x50'
```
### FILTER LOGIC 
```
MOST EXCLUSIVE:
tcp[13] = 0x11
--assumes this--
tcp[13] & 0xFF = 0x11
#####################
LESS EXCLUSIVE:
tcp[13] & 0x11 = 0x11
#####################
LEAST EXCLUSIVE 
tcp[13] & 0x11 > 0
tcp[13] & 0x11 !=0
#####################
```

## BPFS AT THE DATA LINK LAYER
```
Search for the destination broadcast MAC address.
'ether[0:4] = 0xffffffff && ether[4:2] = 0xffff'
'ether[0:2] = 0xffff && ether[2:2]= 0xffff && ether[4:2] = 0xffff'

Search for the source MAC address of fa:16:3e:f0:ca:fc.
'ether[6:4] = 0xfa163ef0 && ether[10:2] = 0xcafc'
'ether[6:2] = 0xfa16 && ether[8:2] = 0x3ef0 && ether[10:2] = 0xcafc'


Search for unicast (0x00) or multicast (0x01) MAC address.
'ether[0] & 0x01 = 0x00'
'ether[0] & 0x01 = 0x01'
'ether[6] & 0x01 = 0x00'
'ether[6] & 0x01 = 0x01'


Search for IPv4, ARP, VLAN Tag, and IPv6 respectively.
ether[12:2] = 0x0800
ether[12:2] = 0x0806
ether[12:2] = 0x8100
ether[12:2] = 0x86dd


Search for 802.1Q VLAN 100.
'ether[12:2] = 0x8100 && ether[14:2] & 0x0fff = 0x0064'
'ether[12:4] & 0xffff0fff = 0x81000064'

Search for double VLAN Tag.
'ether[12:2] = 0x8100 && ether[16:2] = 0x8100'
```

## BPFS AT THE NETWORK LAYER
```
Search for IHL greater than 5.
'ip[0] & 0x0f > 0x05'
'ip[0] & 15 > 5'


Search for ipv4 DSCP value of 16.
'ip[1] & 0xfc = 0x40'
'ip[1] & 252 = 64'
'ip[1] >> 2 = 16'

Search for traffic class in ipv6 having a value.
'ip6[0:2] & 0x0ff0 != 0'


Search for ONLY the RES flag set. DF and MF must be off.
'ip[6] & 0xE0 = 0x80'
'ip[6] & 224 = 128'

Search for RES bit set. The other 2 flags are ignored so they can be on or off.
'ip[6] & 0x80 = 0x80'
'ip[6] & 128 = 128


Search for ONLY the DF flag set. RES and MF must be off.
'ip[6] & 0xE0 = 0x40'
'ip[6] & 224 = 64'

Search for DF bit set. The other 2 flags are ignored so they can be on or off.
'ip[6] & 0x40 = 0x40'
'ip[6] & 64 = 64'


Search for ONLY the MF flag set. RES and DF must be off.
'ip[6] & 0xe0 = 0x20'
'ip[6] & 224 = 32'

Search for MF bit set. The other 2 flags are ignored so they can be on or off.
'ip[6] & 0x20 = 0x20'
'ip[6] & 32 = 32'


Search for offset field having any value greater than zero (0).
'ip[6:2] & 0x1fff > 0'
'ip[6:2] & 8191 > 0'

Search for MF set or offset field having any value greater than zero (0).
'ip[6] & 0x20 = 0x20 || ip[6:2] & 0x1fff > 0'
'ip[6] & 32 = 32 || ip[6:2] & 8191 > 0'


Search for TTL in ipv4(6) packet.
'ip[8] = 128'
'ip[8] < 128'
'ip[8] >= 128'
'ip6[7] = 128'
'ip6[7] < 128'
'ip6[7] >= 128'



Search for ICMPv4(6), TCP, or UDP encapsulated within an ipv4(6) packet.
'ip[9] = 0x01'
'ip[9] = 0x06'
'ip[9] = 0x11'
'ip6[6] = 0x3A'
'ip6[6] = 0x06'
'ip6[6] = 0x11'



Search for ipv4 source or destination address of 10.1.1.1.
'ip[12:4] = 0x0a010101'
'ip[16:4] = 0x0a010101'

Search for ipv6 source or destination address starting with FE80.
'ip6[8:2] = 0xfe80'
'ip6[24:2] = 0xfe80'
```


## BPFS AT THE TRANSPORT LAYER
```
Search for TCP source port 3389.
'tcp[0:2] = 3389'

Search for TCP destination port 3389.
'tcp[2:2] = 3389'

Search for TCP source or destination port 3389.
'tcp[0:2] = 0x0d3d || tcp[2:2] = 0x0d3d'


Search for TCP with options.
'tcp[12] & 0xF0 > 0x50'
'tcp[12] & 240 > 80'

Search for TCP Reserve field with a value.
'tcp[12] & 0x0F != 0'
'tcp[12] & 15 > 0'


Search for TCP Flags set to ACK+SYN. No other flags can be set.
'tcp[13] = 0x12'

Search for TCP Flags set to ACK+SYN. The other flags are ignored.
'tcp[13] & 0x12 = 0x12'


Search for TCP Flags ACK and SYN (both or 1 must be on).
'tcp[13] & 0x12 != 0'
'tcp[13] & 0x12 > 0'



Search for TCP Urgent Pointer having a value.
'tcp[18:2] != 0'
'tcp[18:2] > 0'

```


## WIRESHARKS USE OF BPFS
```
Capture filters - used to specify which packets should be saved to disk while capturing.

Display filters - allow you to change the view of what packets are displayed of those that are captured.

Can use most primitives and/or BPFs

```
### WIRESHARK DISPLAY FILTERS 
```
Protocol Headers

Addresses/Ports

Header Fields

Follow Streams

Apply as Filter
```

### POPULAR WIRESHARK MENUS 
```
Colorize Traffic - Menu → View → Coloring Rules…​

Protocol Hierarchy - Menu→ Statistics → Protocol Hierarchy

Firewall Rules - Menu → Tools → Firewall ACL Rules

Exporting Objects - Menu → File → Export Objects

Decrypt Traffic - Menu → Edit → Preference → Protocols → SSL

Conversations - Menu → Statistics → Conversations

Endpoints - Menu → Statistics → Endpoints

I/O Graph - Menu → Statistics → I/O Graph

ipv4 and ipv6 statistics - Menu → Statistics → ipv4 Statistics ################ Menu → Statistics → ipv6 Statistics

Expert Information - Menu → Analyze → Expert Information

Geo Location - Menu → Edit → preferences → name resolution → GeoIP database directories "Edit"
```



## PASSIVE OS FINGERPRINTING (P0F)
```
Similar to tcpdump except it only captures traffic that matches signatures in its database file.


P0F SIGNATURE DATABASE
less /etc/p0f/p0f.fp


P0F HELP
p0f -h


RUN P0F ON INTERFACE
p0f -i eth0


RUN P0F ON A PCAP
p0f -r capture.pcap


OUTPUT TO GREPPABLE LOG FILE
p0f -r wget.pcap -o /var/log/p0f.log
cat /var/log/p0f.log | grep {expression}
```

### OPERATING SYSTEMS
```
Searches for specific signatures in:

Most Operating Systems

Most Browsers

Search Robots

Command Line Tools
```

## DAY 4

### SOCKET TYPES
```
Stream Sockets(TCP) - Connection oriented and sequenced; methods for connection establishment and tear-down. Used with TCP, SCTP, and Bluetooth.

Datagram Sockets(UDP) - Connectionless; designed for quickly sending and receiving data. Used with UDP.

RAW Sockets(ACTIVLY CREATING SOCKET HEADER) - Direct sending and receiving of IP packets without automatic protocol-specific formatting.
```

### User Space vs. Kernel Space Sockets
```
User Space Sockets (AUTOMATIC TCP OR UDP)
  Stream Sockets
  Datagram Sockets

Kernel Space Sockets (MANUAL)
  RAW Sockets
```

### Socket Creation and Privilege Level
```
User Space Sockets - The most common sockets that do not require elevated privileges to perform actions
on behalf of user applications.

Kernel Space Sockets - Attempts to access hardware directly on behalf of a user application to either prevent
encapsulation/decapsulation or to create packets from scratch, which requires elevated privileges.
````


### Understanding Python Terminology
```
Libraries (Standard Python Library)
  Modules (_import module)
    Functions (module.function)
    Exceptions (try:)
    Constants (AF_INET)
    Objects ()
    List [] vs Tuple ()
```

#### String vs Integer
```
String
  my_string = "Hello World"

Number
  int = 1234
  float = 3.14
  hex = 0x45
```

#### Built-In Functions
```
int()

len()

str()

sum()

print()
```

##### Built-In Methods
```
my_string.upper()

my_string.lower()

my_string.split()

my_list.append()

my_list.insert()
```
#### How Imports Work
```
import {module}

import {module} as {name}

from {module} import *

from {module} import {function}

from {module} import {function} as {name}



```


### Network Programming with Python3
```
Network sockets primarily use the Python3 Socket library and socket.socket function.

import socket
  s = socket.socket(socket.FAMILY, socket.TYPE, socket.PROTOCOL) 
```
#### The socket.socket Function
```
Inside the socket.socket. function, you have these arguments, in order:

socket.socket( *family*, *type*, *proto* )
family: AF_INET*, AF_INET6, AF_UNIX

type: SOCK_STREAM*, SOCK_DGRAM, SOCK_RAW

proto: 0*, IPPROTO_TCP, IPPROTO_UDP, IPPROTO_IP, IPPROTO_ICMP, IPPROTO_RAW
```
#### Python3 Libraries and References
```
Socket

Errors

Struct

Exceptions

Sys
```
### Raw IPV4 Sockets
```
RAW Socket scripts must include the IP header and the next headers.

Requires guidance from the "Request for Comments" (RFC) to follow header structure properly.
  RFCs contain technical and organizational documents about the Internet, including specifications and policy documents.

See RFC 791, Section 3 - Specification for details on how to construct an IPv4 header.
```

#### Raw Socket Use Case
```
Testing specific defense mechanisms - such as triggering and IDS for an effect, or filtering

Avoiding defense mechanisms

Obfuscating data during transfer

Manually crafting a packet with the chosen data in header fields
```
### Encoding and Decoding
```
Encoding
  The process of taking bits and converting them using a specified cipher.

Decoding
  Reverse of the conversion process used by the specified cipher for encoding.

Common encoding schemes
  UTF-8, Base64, Hex
```

#### Hex Encoding and Decoding
```
Encode text to Hex:
  echo "Message" | xxd

Encode file to Hex:
  xxd file.txt file-encoded.txt

Decode file from Hex:
  xxd -r file-encoded.txt file-decoded.txt
```
#### Python Hex Encoding
```
import binascii
message = b'Message'
hidden_msg = binascii.hexlify(message)
```


#### Base64 Encoding and Decoding
```
Encode text to base64:
  echo "Message" | base64

Endode file to Base64:
  base64 file.txt > file-encoded.txt

Decode file from Base64:
  base64 -d file-encoded.txt > file-decoded.txt
```

#### Python Base64 Encoding
```
import base64
message = b'Message'
hidden_msg = base64.b64encode(message)
```
### Encoding vs Encryption
```
Encoding - converts data into a different format

Encryption - scrambles data to make it unreadable without a secret key
```


### RUNNING SOCKET SCRIPTS
```
nc -lvp 1111 for tcp
nc -luvp 2222 for udp
```

## DAY 5
### Reconnaissance Stages
```
Passive External

Active External

Passive Internal

Active Internal
```

#### Passive Recon Activities
```
IP Addresses and Sub-domains

Identifying External/3rd Party sites

Identifying People

Identifying Technologies

Identifying Content of Interest

Identifying Vulnerabilities
###############
Useful Sites
  OSINT Framework
  Pentest-Standard
  SecuritySift
###############

IP Addresses and Sub-domains
  DNS Lookups
  BGP advertised prefixes
  IANA listed address blocks
###############

Identifying External/3rd Party sites
  Parent/Subordinate organizations
  Clients/Customers
  Service organizations
  Partners
###############

Identifying People
  Target website
  Crawler tools like Maltego or Creepy
  Search engines
  Social Media
  Job Portals
  Tracking active emails
###############
Identifying Technologies
  File extensions
  Server responses
  Job listing
  Website content
  Google Hacking
  Shodan.io
###############
Identifying Content of Interest
  /etc/passwd and /etc/shadow or SAM database
  Configuration files
  Log files
  Backup files
  Test pages
  Client-side code
################
Identifying Vulnerabilities
  Known Technologies
  Error messages responses
  Identify running services
  Identify running OS
  Monitor running Applications
```
#### Dig vs Whois
```
Whois - queries DNS registrar over TCP port 43
  Information about the owner who registered the domain
    Whois
whois zonetransfer.me

Dig - queries DNS server over UDP port 53
  Name to IP records
      Dig
dig zonetransfer.me A
dig zonetransfer.me AAAA
dig zonetransfer.me MX
dig zonetransfer.me TXT
dig zonetransfer.me NS
dig zonetransfer.me SOA
```
#### Zone Transfer
```
Between Primary and Secondary DNS over TCP port 53

https://digi.ninja/projects/zonetransferme.php
  dir axfr {@soa.server} {target-site}
  dig axfr @nsztm1.digi.ninja zonetransfer.me
```
#### Netcraft
```
Similar to whois but web-based

https://sitereport.netcraft.com/
```
#### Web-check.xyz
```
Checks various information about a website

https://web-check.xyz/
```
#### Historical Content
```
Wayback Machine

http://archive.org/web/
```
#### Google Searches
```
Advanced searches.
List of filters
Dork Search

site:*.ccboe.net

site:*.ccboe.net "administrator"
```

#### Shodan
```
Shodan: A search engine for Internet-connected devices

https://www.shodan.io

Be aware of attribution
```
#### Passive OS Fingerprinter (p0f)
```
p0f: Passive scanning of network traffic and packet captures.

  more /etc/p0f/p0f.fp
  sudo p0f -i eth0
  sudo p0f -r test.pcap
```
#### Social Tactics
```
Social Engineering (Hack a person)

Technical based (Email/SMS/Bluetooth)

Other Types (Dumpster Diving/Shoulder Surf)
```


### ACTIVE EXTERNAL DISCOVERY 

#### Scanning Nature
```
Active

Passive
```
#### Scanning Strategy
```
Remote to Local

Local to Remote

Local to Local

Remote to Remote
```
#### Scanning Approach
```
Aim
  Wide range target scan
  Target specific scan

Method
  Single source scan
    1-to-1 or 1-to-many

  Distributed scan
    many-to-one or many-to-many
```

#### Scanning Approach
```
Vertical Scan - Range of ports on 1 box

Horizontal Scan - 1 or many ports on a range of boxes
```
#### NMAP Scan Types
```
Broadcast Ping/Ping sweep (-sP, -PE)

SYN scan (-sS)

Full connect scan (-sT)

Null scan (-sN)

FIN scan (-sF)

XMAS tree scan (-sX)

UDP scan (-sU)

Idle scan (-sI)

Decoy scan (-D)

ACK/Window scan (-sA)

RPC scan (-sR)

FTP scan (-b)

OS fingerprinting scan (-O)

Version scan (-sV)

Discovery probes

-PE - ICMP Ping

-Pn - No Ping


NMAP - Time-Out
-T0 - Paranoid - 300 Sec

-T1 - Sneaky - 15 Sec

-T2 - Polite - 1 Sec

-T3 - Normal - 1 Sec

-T4 - Aggresive - 500 ms

-T5 - Insane - 250 ms


NMAP - Delay
--scan-delay <time> - Minimum delay between probes

--max-scan-delay <time> - Max delay between probes


NMAP - Rate Limit
--min-rate <number> - Minimum packets per second

--max-rate <number> - Max packets per second



Traceroute - Firewalking
traceroute 172.16.82.106
traceroute 172.16.82.106 -p 123
sudo traceroute 172.16.82.106 -I
sudo traceroute 172.16.82.106 -T
sudo traceroute 172.16.82.106 -T -p 443



Netcat - Scanning
nc [Options] [Target IP] [Target Port(s)]
-z : Port scanning mode i.e. zero I/O mode

-v : Be verbose [use twice -vv to be more verbose]

-n : do not resolve ip addresses

-w1 : Set time out value to 1

-u : To switch to UDP



Netcat - Horizontal Scanning
Range of IPs for specific ports

TCP
for i in {1..254}; do nc -nvzw1 172.16.82.$i 20-23 80 2>&1 & done | grep -E 'succ|open'

UDP
for i in {1..254}; do nc -nuvzw1 172.16.82.$i 1000-2000 2>&1 &



Netcat - Vertical Scanning
Range of ports on specific IP

TCP
nc -nzvw1 172.16.82.106 21-23 80 2>&1 | grep -E 'succ|open'

UDP
nc -nuzvw1 172.16.82.106 1000-2000 2>&1 | grep -E 'succ|open'



Netcat - TCP Scan Script

#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done



Netcat - UDP Scan Script

#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nuvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done



Netcat - Banner Grabbing

Find what is running on a particular port

nc [Target IP] [Target Port]
nc 172.16.82.106 22
nc -u 172.16.82.106 53
-u : To switch to UDP
```
#### Curl and Wget
```
Both can be used to interact with the HTTP, HTTPS and FTP protocols.

Curl - Displays ASCII
  curl http://172.16.82.106
  curl ftp://172.16.82.106

Wget - Downloads (-r recursive)
  wget -r http://172.16.82.106
  wget -r ftp://172.16.82.106
```

### PASSIVE INTERNAL DISCOVERY 

#### Packet Sniffers
```
Wireshark
Tcpdump
p0f

Limited to traffic in same local area of the network
```

#### Native Host Tools
```
Show TCP/IP network configuration

Windows: ipconfig /all
Linux: ip address (ifconfig depreciated)
VyOS: show interface
```

#### Native Host Tools
```
-Show DNS configuration-

Windows: ipconfig /displaydns
Linux: cat /etc/resolv.conf


-Show ARP Cache-

Windows: arp -a
Linux: ip neighbor (arp -a depreciated)


-Show network connections-

Windows: netstat
Linux: ss (netstat depreciated)

Example options useful for both netstat and ss: -antp
a = Displays all active connections and ports.
n = No determination of protocol names. Shows 22 not SSH.
t = Display only TCP connections.
u = Display only UDP connections.
p = Shows which processes are using which sockets
(RECOMMENDED IS ss -ntlp) 

-Services File-

Windows: %SystemRoot%\system32\drivers\etc\services
Linux/Unix: /etc/services


-OS Information-

Windows: systeminfo
Linux: uname -a and /etc/os-release


-Show Running Processes-

Windows: tasklist
Linux: ps or top

Example options useful for ps: -elf
e = Show all running processes
l = Show long format view
f = Show full format listing


-Command path-

which
whereis


-Routing Table-

Windows: route print
Linux: ip route (netstat -r deprecated)
VyOS: show ip route


-File search-

find / -name hint* 2> /dev/null
find / -iname flag* 2> /dev/null
```

### ACTIVE INTERNAL DISCOVERY

#### Active Internal Network Reconnaissance
```
Will use similar tools as Active External Network Reconnaissance

Scope and addresses may differ


-ARP Scanning-
arp-scan --interface=eth0 --localnet

nmap -sP -PR 172.16.82.96/27


-Ping Scanning-
ping -c 1 172.16.82.106

for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
sudo nmap -sP 172.16.82.96/27


-DEV TCP Banner Grab-
exec 3<>/dev/tcp/172.16.82.106/22; echo -e "" >&3; cat <&3


-DEV TCP Scanning-
for p in {1..1023}; do(echo >/dev/tcp/172.16.82.106/$p) >/dev/null 2>&1 && echo "$p open"; done
```


### PREFORMING NETWORK FORENSICS - MAPPING
```
Diagram devices

Line Types

Written Information

Coloring

Groupings

Device type (Router/host)

System Host-names

Interface names (eth0, eth1, etc)

IP address and CIDRs for all interfaces

TCP and UDP ports

MAC Address

OS type/version

Known credentials
```
#### Network Mapping Tools
```
Draw.io Local (Template)

Draw.io Web

Witeboard.com

Draw.Chat

SmartDraw

Ziteboard

Tutorialspoint Whiteboard

Explain Everything Whiteboard

```

### Reconnaissance Steps
```
Network Footprinting

Network Scanning

Network Enumeration

Vulnerability Assessment
```

#### Network Footprinting
```
Collect information relating to target

Network

Systems

Organization
```
#### Network Scanning
```
Port Scanning

Network Scanning

Vulnerability Scanning
```
#### Network Enumeration
```
Network Resource and shares

Users and Groups

Routing tables

Auditing and Service settings

Machine names

Applications and banners

SNMP and DNS details

Other common services and ports
```
#### Vulnerability Assessment
```
Injection

Broken Authentication

Sensitive Data Exposure

XML External Entities

Broken Access Control

Security Misconfiguration

Software/Components with Known Vulnerabilities
```




## Netcat command
```
nc 172.16.20.1 22 (ip then port)
```


