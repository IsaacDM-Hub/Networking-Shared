
# CTF ANSWERS AND BREAKDOWNS
# Day 1
## 1. ARP Storm
```
What MAC address is initiating the ARP Storm?

A: 00:07:0d:af:f4:54

(Filter for "arp", check the source MAC)
```
## 2. ARP – 1
```
What is the MAC of 10.10.10.1?

A: 00:1d:09:f0:92:ab


(Filter "ip.addr==10.10.10.1", check the MAC)
```

## 3. ARP – 2
```
What is the MAC of 10.10.10.2?

A: 00:1a:6b:6c:0c:cc

(Filter "ip.addr==10.10.10.2", Check the MAC)
```

## 4. ARP – 3
```
What is the MAC address of the system trying to perform the ARP MitM attack?

A: fa:16:3e:35:21:5a

(Filter "arp.opcode==2", When looking for MitM, search for multiple different ip's under the same MAC)
```
## 5. RARP – 1
```
What is the OP code of a RARP Request?

A: 3 

(Google, RARP appears when filtering "arp.opcpde==3")
```

## 6. RARP – 2
```
What is the OP code of a RARP Response?

A: 4

(Google, RARP appears when filtering "arp.opcpde==4")
```

## 7. RARP – 3
```
What is the RARP requestor’s MAC?

A: 00:0c:29:34:0b:de

(Filter "arp.opcode==4", grab the senders MAC)
```

## 8. RARP – 4
```
What was the RARP requestor’s resolved IP address?


A: 10.1.1.100

(Filter "arp.opcode==4", grab the responding IP in info)
```

## 9. Gratuitous ARP – 1
```
What is the MAC of the system spamming gratuitous ARPs for 192.168.1.254?


A: 00:00:5e:00:01:01

(Filter "arp.opcode==2", look for the Gratuitous ARP and look at the sender MAC)
```

## 10. CDP – 1
```
What is the software version of the Cisco Switch IOS (copy entire field “as is” from Wireshark)?


A: IOS (tm) C2950 Software (C2950-I6K2L2Q4-M), Version 12.1(22)EA14, RELEASE SOFTWARE (fc1)

(Filter for "cdp.version==2 or cdp", this searches for cisco devices)
```

## 11. CDP – 2
```
What is the software version of the Cisco Router IOS (copy entire field “as is” from Wireshark)?

A: IOS (tm) 1600 Software (C1600-NY-L), Version 11.2(12)P, RELEASE SOFTWARE (fc1)

(Filter for "cdp.version==2 or cdp", this searches for cisco devices)
```

## 12. LLDP – 1
```
What is the System Name of one of the LLDP sending devices?

A: S1.cisco.com

(Filter "lldp", look for system in link layer discoery protocol)
```

## 13. STP – 1
```
What is the Bridge Priority of the STP Root Bridge?

A: 0

(Filter "stp", Check the Spanning Tree Protocol for "Root Identifier")
```

## 14. STP – 2
```
What is the MAC address of the STP Root Bridge?

A: 00:1f:27:b4:7d:80

(Filter "stp", Check the Spanning Tree Protocol for "Root Identifier")
```

## 15. VTP – 1
```
What is the VTP Management Domain Name?

A: cisco

(Filter "vtp", Search in VLAN Trunking Protocol for Management Domain )
```

## 16. VTP – 2
```
What is the latest configuration revision number?

A: 11

(Filter "vtp", look for revision number in info)
```
## 17. VTP – 3
```
How many total VLANs are being advertised via VTP?

A: 22

(Filter "vtp", look into the advertisment, count the total VLAN information)
```

## 18. VLAN – 1
```
What is the message contained within the single tagged VLAN traffic coming from 11.22.33.44?

A:I pitty the foo

(filter "ip.addr==11.22.33.44", look in the information field )
```
## 19. VLAN – 2
```
What is the VLAN ID of this traffic?

A: 999

(with the same filter, look in 802.1Q, look at "ID")
```

## 20. VLAN Hopping – 1
```
What is the VLAN ID being attacked by 10.10.10.10 using Double Tagging?

A: 250

(with the same filter, look in 802.1Q, look at "ID")

```

## 21. VLAN Hopping – 2
```
What is the combined message being sent via ICMP?

A: Wouldn't you like too be a Pepper Too!

(filter "icmp", look for the info in the bottom right)
```

## 22. ICMP – 1
```
What is the OS of 192.168.1.1 host based off its Echo Request message to the Google DNS?

A: Linux

(Filter "ip.addr==192.168.1.1", look at the info section, it is all symbols which means Linux)
```

## 23. ICMP – 2
```
What is the message that 192.168.65.20 is sending to Google's DNS via ICMP?

A: Exsqueeze me?

(filter "ip.addr==192.168.65.20 && icmp", look in the info field)
```

## 24. ICMP – 3
```
How many Hops away is the 151.101.64.84 address?

A: 11

(filter "ip.src==151.101.64.84 && icmp" look at he IPV4 TTL)
```
## 25. ICMP – 4
```
What is the OS of 10.10.205.253 host based off its Echo Request message to 10.10.0.40?

A: Windows

(Filter "ip.src==10.10.205.253, the info seection is all letters which is only winodws)
```

## 26. Fragmented – 1
```
What is the IP ID of the fragmented ICMP packet in Decimal? (starting at packet 6472)

A: 46544

(Search for the packet, look for the identification)
```

## 27. Fragmented – 2
```
What is the offset value of the fragments?

Not the calculated value shown in Wireshark

Suggest converting the value from the Hex Dump

A: 122

(Look at the Fragment Offset at the end of the exchange, convert the hex value in the info to decimal)
```

## 28. ICMPv6 – 1
```
What is the ICMPv6 type number of Echo Request?

A: 128

(google)
```

## 29. ICMPv6 – 2
```
What is the ICMPv6 type number of Echo Reply?

A: 129

(google)
```

## 30. ICMPv6 – 3
```
What is the ICMPv6 type number of the Router Advertisement message?

A: 134

(filter "icmpv6.type==134)
```
## 31. ICMPv6 – 4
```
What is the link-layer address of the advertising router?

A: fa:16:3e:35:21:5a

(In the same packet, look into the ICMPV6 option source link-layer)
```

## 32. ICMPv6 – 5
```
What is the IPv6 prefix being advertised?

A: beef:4:f00d::

(In the same packet, look into the ICMPV6 option prefix info then the Prefix at the bottom)
```

## 33. HSRP – 1
```
What is the HSRP virtual IP?

A: 192.168.0.1

(filter "hsrp" search the cisco Hot standby for Virtual IP)
```

## 34. HSRP – 2
```
What is the HSRP multicast address used?

A: 224.0.0.2

(filter "hsrp" and grab the ip of the MCASt)
```
## 35. HSRP – 3
```
What is the IP address of the HSRP Active forwarder (before the takeover)?

A: 192.168.0.30

(Filter "hsrp, first packet src ip)
```
## 36. HSRP – 4
```
What is the IP address of the HSRP Active forwarder (after the takeover)?

A: 192.168.0.10

(Filter "hsrp, last packet src ip)

```
## 37. VRRP – 1
```
What is the VRRP multicast address used?

A: 224.0.0.18

(filter "vrrp" grab the mcast ip)
```
## 38. VRRP – 2
```
What is the VRRP virtual IP?

A: 192.168.1.254

(filter "vrrp", go into Virtual router and grab the ip)
```
## 39. VRRP – 3
```
How many total devices are communicating via VRRP?

A: 3

(filter "vrrp" count the total unique IP's)
```

## 40. RIP – 1
```
How many networks are being advertised via RIP?

A: 2

(filter "rip" look in the routing information protocol and count unqiue ips)
```
## 41. RIP – 2
```
What are the networks being advertised (in numeric order separated by commas and no spaces)?
(i.e. 1.0.0.0,2.0.0.0 )

A: 200.0.1.0,200.0.2.0

(filter "rip" look in the routing information protocol and search ip)
```
## 42. RIP – 3
```
What Protocol and port is being used for RIP?

PROTOCOL PORT

A: UDP 520

(same packet, look in IPV4)
```

## 43. EIGRPv4 – 1
```
What network is being advertised via EIGRPv4

A: 192.168.4.0

(filter "eigrp" search the "CISCO EIGRP" for internal route and grab ip)
```

## 44. EIGRPv4 – 2
```
What is the IP protocol number used for EIGRP?

A: 88

(google)
```
## 45. EIGRPv4 – 3
```
What multicast address is used to send EIGRPv4 updates?

A: 224.0.0.10

(google)
```
## 46. EIGRPv6 – 1

```
What network is being advertised via EIGRPv6

A:2001:db8:0:400::/64

(filter "eigrp" go to a IPV6 and grab the internal route)
```

## 47. EIGRPv6 – 2
```
What multicast address is used to send EIGRPv6 updates?

A: FF02::A

(google)
```
## 48. EIGRPv6 – 3
```
What Autonomous system number is being used?

A: 100

(filter "eigrp" go to a IPV6 and grab the system number)
```
## 49. OSPF – 1
```
What is the IP protocol number used for OSPF?

A: 89

(google)
```
## 50. OSPF – 2
```
What is the IP address of the OSPF designated router (DR)?

A: 192.168.170.8

(filter "ospf" look into OSPF, go to very bottom to DR and look for ip)
```

## 51. OSPF – 3
```
What multicast address is used by the DR to send updates?

A: 224.0.0.5

(filter "ospf" and grab the dst ip)
```

## 52. BGP – 1
```
How many networks are being advertised via BGP?

A: 3

(filter "bgp" go into each packet, look through the BGP.find IPs in NLRI)
```
## 53. BGP – 2
```

What are the networks being advertised (in numeric order separated by commas and no spaces)?

(i.e. 1.0.0.0,2.0.0.0)

A: 10.0.0.0,172.16.0.0,192.168.4.0

(same packet, same IP's just listed in order)
```

## 54. BGP – 3
```
What Autonomous system number is the 192.168.0.10 peer in?

A: 65210

(same packet, look into the path attributes and grab the AS of the IP)
```

## 55. BGP – 4
```
What Protocol and port is being used for BGP?

Transport PROTOCOL PORT

A: TCP 179

(same packet, look through the IPV4 and find Protocol and google port)
```


# DAY 2 

## 1. SMB – 1
```

What Protocol and port is being used for SMB?

PROTOCOL PORT

A: TCP 445

(GOOGLE)
```

## 2. SMB – 2
```
What is the name of the file accessed via SMB?

A: putty.exe

(filter "smb" and follow TCP stream, look in the traffic)
```

## 3. DHCP – 1
```
What is the IP address of the DHCP server?

A: 192.168.0.1

(filter "dhcp" use the SRC IP in the DHCP ACK)
```

## 4. DHCP – 2
```
What is the “offered” IP address?

A: 192.168.0.10

(same filter as last, look in the DST IP in the DHCP OFFER)
```

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
