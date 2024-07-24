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
### VTP Vulnreability 
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

802.1x

Dynamic ARP inspection (DAI)

Static CAM entries

Static ARP entries

Disable DTP negotiations

Manually assign Access/Trunk ports

```
