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
