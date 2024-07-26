
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
