
# CTF ANSWERS AND BREAKDOWNS

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

A:

()
```
