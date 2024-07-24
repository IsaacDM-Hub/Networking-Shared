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
Default - VLAN 1

Data - User traffic

Voice - VOIP traffic

Management - Switch and router management

Native - Untagged switch and router traffic
```

### VLAN Hopping Attack 
```
Switch Spoofing (DTP)

Single Tagging

Double Tagging (using native VLAN)
```
