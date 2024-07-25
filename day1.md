## day 1
https://net.cybbh.io/public/networking/latest/02_network/fg.html is the day 1 guide 
Blue Internet Host
Student#: student17

Command: ssh student@10.50.29.222 -X

Password: password
http://10.50.20.180:8000/challenges

## PDU protocol data unit
session-application = data
transport = segment/datagram
network = packet
data link = frame 
physical = bit

## internet standard orgs
IETF = RFCS
IANA - internet numbers
  # in charge of ips and domains, who has what ip
IEEE - LAN/WAN electrical standards
  # responsible for maintaining standards and protocols

========================Layer 1 (physical)========================
# bits are at this level
# binary, decimal, hex, base64
# binary:
  word = 32 bits
  half word = 16 bits
  byte = 8
  nibbles = 4
# hexadecimal:
  base16 (0-9 and A-F)
# base64 (A-Z a-z 0-9 + /)
  uses = to show a null value with a max of 2
# bus topology
  straight line, half-duplex
# star topology
  switch at the center where everything is plugged into it
# ring toplogy
   keys are shared among connected devices 
# mesh topology
  everyone is connected to everyone else, or some are connected to others
# wireless 
  devices are connected to a modem
# hierarchal 
  used at an enterprise level, different layers and uses firewalls

## devices
hubs: 
everyone gets everything (doesnt check frames that are sent)
sends to all ports (has packet collision)

repeater:
strengthens the signal by repeating it to reach a greater distance

switches:
similar to hubs but organizes based off collision domains, knows and keeps mac addresses so prevents packet collisions, dont go between networks

routers:
allows you to move across networks 

## ethernet timing (bit times)
Speed        Bit-Time
10Mbps       100ns
100Mbps      10ns
1 Gps        1ns
10 Gbps     .1ns
100 Gbps    .01ns


=====================layer 2 Data-link=============================
## MAC
  goes up the layer model from 2 to 3, holds alot of information
## LLC
  goes down the layers, from 2 to 1, 

moving between layers is called encapd/ecapsulation  

## switch operation
  # build MAC Address (CAM) Table
    > # Learns by reading source MAC Addresses
  # Forwarding Frames
    > # Decision based on destination MAC Address
  # switching modes
    cut through
      default method*
      only checks the destination MAC*
    Fragment free
      Stores first 64 bytes of the frame (Ethernet portion) before forwarding*
    Store-and-Forward
       Information is kept and sent at a later time to the destination*
## CAM table overflow attack
  sends frames with fake source MAC addresses to switch 
  cause switch to fill table with fake addresses
  switch wont be able to learn new valid addresses

## MAC Addressing
on windows uses - for every 2 chars
on unix uses : for every 2 chars
Cisco uses . for every 4chars
> Length:  48-bit | 6 byte | 12 Hex

## MAC address Types
  > Unicast: One to One
    > # 8TH bit is off
  > Multicast: One to Many
    > # 8TH bit is on
  > Broadcast: One to All
    > # All bits on

## Ethernet Header and Frame
> Mac Header/Trailer: 14 Bytes
> Data: 46-1500 Bytes
> EtherType
  > 0x0800 - IPv4
  > 0x0806 - ARP
  > 0x86DD - IPv6
  > 0x8100 - VLAN (important)

## MAC spoofing 
  changes MAC address

## VLAN
# Splitting up a switch into virtual ports
> Trunk Link
  > # Joining two switches together with VLAN Ports as if they were physically connected with ethernet
> Types
  > # Default: VLAN 1
  > # Data - User Traffic
  > # Voice - VOIP Traffic
  > # Management - Switch and router managment
  > # Native - Untagged switch and router traffic
> Headers
  > # Header length is: 32 bits
  > # 802.1Q
  > # 802.1AD
> VLAN Hopping Attack
  > # Switch Spoofing (DTP)
  > # Single Tagging
  > # Double Tagging (using native VLAN) and only works with a direct connection one of the vlans

## ARP
> Types
  > ARP (OPcode 1 and 2)
    > # Requests info. Example: knows ip asks for mac (Location)
  > RARP (OPcode 3 and 4)
    > # The client requesting an IP Address from the server's gateway
  > Proxy ARP (OPcode 2)
    > # The host answering the ARP Request from whatever asked where they were
  > Gratuitous ARP (OPcode 2)
    > # The host broadcasts their location without the request
> ARP Cache
    > # A tables that has translations in it
    > # Collection of Address Resolution Protocol Entries
    >     last from 2-20 mins
    >     default gateway is always present bare min
# poison arps cache with gratuitous and proxy arp

# Man-In-The-Middle With ARP
   Causes victim machines to populate their ARP Cache with the MAC Address of the attacker's machine instead of the local router's MAC Address

## VLAN Trunking Protocol (VTP)
  > # Dynamically add/remove/modify VLANs
> is Cisco Proprietary
> Modes
  > Server: central management  
  > Client: pulls from server
  > Transparent: ignore server
> Vulnerablities
  > Spoofing Attacks
  > can cause switches to dump all VLAN info 

## Dynamic Trunking Protocol (DTP)
> # Used to dynamically create trunk links
> # 2 modes:
>   dynamic auto: default, makes it willing to be a trunk port
>   dynamic desirable: tries to convert to a trunk 
> Vulnerabilities
  > # Can send crafted messages to form a VLAN trunk link
  > # On By Default
  > # Recomment to:
    > # Disable and manually access trunk link

## CDP (Cisco Discovery Protocol)
  # Network Discovery tool or admins that identifies the neighbors
## FDP (Foundry Discovery Protocol)
  # Proprietary data link layer protocol
## LLDP (Link Layer Discovery Protocol)
  # Neighbors are able to find each other on the local network (principally wired Ethernet)
# vulnerabilities: 
  leaks valuable info, clear text, enabled by default, may require them for VIP

## Spanning Tree Protocol (STP)
  # Layer 2 network protocol used to prevent looping within a network topology 
  # Always forward traffic in specific patterns
  # packets stuck in a loop is a broadcast storm
	  > # STP is a method to prevent this as it disables temporarily any link that is not the best route out. Redundancy can still be in place as a backup

> ## Types
  > # 802.1D STP
  > # Per VLAN Spanning Tree + (PVST+)
  > # 802.1w - Rapid Spanning Tree Protocol (RSTP)
  > # Rapid per VLAN Spanning Tree + (RPVST+)
  > # 802.1s (Multiple Spanning Tree)
> route bridge selection route out of the network
> spanning tree attack
	# can craft a bpdu (bridge protocol data units) to deny service with a false/erroneous/spoofed bridge

## Port Security modes
	> # Restrict – block without shutting down
	> # protect- lets through but logs the mac
	> # shutdown – is shutdown (default)
> ## Vulnerabilities to port security
  > # Dependent on MAC Addresses
  > # MAC Spoofing
>attack Mitigiation techniques Layer 1
  > # Shutdown unused ports
  > # Enable Port Security
  > # IP Source Guard
  > # Manually assign STP Root
  > # BPDU Guard
  > # DHCP Snooping
>attack Mitigation Techniques Layer 2
  > # 802.1x
  > # Dynamic ARP inspection (DAI)
  > # Static CAM Entries
  > # Static ARP Entries
  > # disable DTP negotiations
  > # manually assign access/trunk ports



===================================layer 3 Network====================================
## IPv4 (0x0800)
> # Classful subnetting
  > Class A (0-127)
  > Class B (128-191)
  > Class C (192-223)
  > Class D (224-239) multicasting
  > Class E (240-255) not used
> Classless subnetting (CIDR)
> NAT
> # TTL
  > Linux (64)
  > Windows (128)
  > Network Devices
> # Types
  > Unicast: any class a-c
  > Multicast: class D
  > Broadcast:  any ip where the host portion is all on
> # ipv4 Scopes
  > Public
  > Private (RFC 1918)
  > Loopback (127.0.0.1)
  > Link-Local (APIPA)
  > Multicast (class D)
> ## ipv4 Fragmentation
  # Breaking up packets from higher MTU to lower MTU (Maximum Transmission Unit) network
  # Performed by routers
  # MF Flag is on from 1st until 2nd to last
  # offset is on from 2nd until the last
  # offset = (MTU - (IHL x 4)) / 8
> # Auto Config
  > APIPA
  > DHCP
  > DORA
> # Vulnerability 
  > Rogue DHCP
  > Evil Twin
  > DHCP Starvation 
    # Denial of service
## IPv6 (Standardized 2017)
> Fragmentation
  > # Does not support fragmentation within its header
  > # Routers do not fragment IPv6 packets !!!!!!!!!!!!!1
  > # Source adjusts MTU to avoid Fragmentation
  > # Source can use IPv6 fragmentation extension header
> Addressing
  > # 128 bit addressing
>  # 64-bit prefix and interface ID
>  # 340 undeillian addresses 
> Subnetting
  > # Organizations assigned a 48-bit Prefix by IANA
> Types
  > Unicast
  > Multicast
  > Anycast
## ICMPv4
  # IPv4 Protocol
> ## OS Fingerprinting
  > Linux
    >  # default TTL is 64
    >  # Default Size: 64 Bytes
    >  # Payload Message: nfo/./.345/.,0u98fgoij (numbers and symbols)
  > Windows:
    > # Default Size: 40 Bytes and TTL is 128
    > # Payload Message: abcdefghijklmnopqrstuvwxyz (letters only)
> # icmpv4 Traceroute
  > # Identifies Hops between the source and the destination
  > # Uses incrimenting ttls
  > # Uses ICMP (windows default), UDP (linux default), TCP
> Attacks
  > # Firewalking (Traceroute)
  > # Oversized ICMP Messages
  > # ICMP Redirects
  > # SMURF Attack
  > # Map Network w/ IP unreachables
  > # ICMP Covert Channels

## NDP
	type 133,134,135,136,137
 > RTR solicitation 133
 > RTR ADVERT 134
 > neighbor solicitation 135
 > neighbor ADVERT 136
 > redirect 137
(Classful)
  > # Do not Carry subnet mask information within the routing updates
  > # Exchange routing updaates at the regular time intervals
(Classless)
  > # Opposite of both

## Routing Protocol
> # Used Between Layer 3 devices to learn and advertise routes and maintain routing tables
> # Routes a routed protocol for learning and maintaining routing table
## Routed Protocol
> # Used between Routers to direct use traffic. It is also called network protocols
> # Routed by routing protocols


IGP and EGP
> IGP (Interior Gateway Protocols)
  > # Routing protocols that are used within an Autonomous System (AS).
  > # Referred to as intra-AS routing.
  > # Organizations and service providers IGPs on their internal networks.
  > # IGPs include RIP, EIGRP, OSPF, and IS-IS.
> EGP (Exterior Gateway Protocols)
  > # Used primarily for routing between autonomous systems.
  > # Referred to as inter-AS routing.
  > # Service providers and large companies will interconnect their AS using an EGP.
  > # The Border Gateway Protocol (BGP) is the only currently viable EGP and is the official routing protocol used by the Internet.
> OSPF: cost
> RIPv2: hop
> EIGRP: bandwidth,delay,load,reliability
> ISIS
> BGP: policy

Distance Vector Routing Protocols
> # They share entire routing tables with their directly connected neighbors and from these shared tables they determine:
  > Distance
    > # How far away the destination network is from the outer and is based on a metric such as the hop count, cost, bandwidth, delay
  > Vector
    > # Specifies direction to the remote network
Link State Routing Protocols
>  Each router receives an LSA (Link State Adverstisement) and begins to build a map of the entire network


Routing Protocol Vulnerabilities
> DDOS
> Packet Mistreating Attacks (PMA)
> Routing Table Poisoning (RTP)
> Hit and Run DDOS (HAR)
> Persistence Attacks (PA)


BGP
> # Roadmap of the internet
> # Routes traffic between AS Number
> # Advertises IP CIDR address blocks
> # Establishes Peer relationships
> # Complicated Configuration
> # Complicated and slow path selection
> BGP Hijacking
  > # This works by illegitimate advertising of addresses, and takes over the CIDR address blocks corrupting the internet routing tables by falsifying the advertising addresses


Static Routing
> # Manually Configured routes
> # They dont advertise over the network
> # They dont use bandwidth


Dynamic Routing
> # Discover new remote networks
> # Maintaining current routing information
> # Choose the best path to remote networks
> # Recalculate a new path to a remote network should the primary fail

first hop redundancy protocol
	vulnerable to attack via injecting manipulated messages witha MitM attack
=========================== Layer 4 (Transport) ============================
## Well-Know Ports: 0-1023 well-known (system)
## Registered : 1024-49151 registered (user)
## Dynamic: 49152-65535 dynamic (private)


## TCP Flags:
> CWR - 128
> ECE - 64
> URG - 32
> ACK - 16
> PSH - 8
> RST - 4
> SYN - 2
> FYN - 1


========================== Layer 5 (Session) ==================================
VPN
> # Encasulate a private IP through public IPs
> Types
  > # Remote Access VPN
  > # Site-to-Site VPN
  > # Client-to-Site VPN


L2TCP
> # Tunneling Protocol Cisco uses
> # tunnel only, no encryption
> # RFC 2661

IPSEC
> # Suite of protocols used to secure IP Communications by providing 3 triad of security at layer 3
> Transport Mode
  > # Only encrypts the payload of the original IP packet leaving the original IP header intact
> Tunnel Mode
  > # IP gets encapsulated and gets a new ip packet by adding an additional ip header
  > # Creates a secure VPN

Openvpn
> #open source
> # uses SSL for encryption
> # UDP/TCP port 1194

Proxy
> # Functions as a messenger (An intermediary)
> # EXAMPLE: We want to give Bob a secret santa gift (He wont know it was us who have it to him), instead we use a messenger to give the present to Bob.



Socks4
> # TCP ONLY!
> # Forwards TCP Traffic (Proxychains)

socks5 
> # supports UDP
> # supports proxy binding

Netbios (Examine Network Basic Input Output System)
> # Name Resolution
> # TCP 139, UDP 137/138


SMB
> # TCP 139/445 and DUP 137/138
> # Acilitate the sharing of files, printers, serial ports, and various communications among network nodes
> # Datagram is port 138 while session is 139

RPC (Examine Remote Procedure Call)
> # allows a program to request a service from another program located on the same system or on remote computer
> # hides network complexities
> # XML,JSON,SOAP,gRPC

API
> # Framework of rules and protocols for software components to interact
> # Methods, parameters, and data formats for requests and responses
> # REST and SOAP

======================= Layer 6 (Presentation) =====================
Responsibilities
> Translation
> Formating
> Encoding
> Encryption (Symmetric and asymmetric)
> Compression


======================== Layer 5 (Application) ===============================
Telnet
> Port 23
> Remote Login
> Authentication
> clear text
> credentials susceptible to interception

## SSH
> Port 22
> Remote Login
> Encrypted
> Asymmetric or PKI for key exchange
> User authentication
> Architecture
  > # User Key - Aymmetric public key used to identify the user to the server
  > # Host Key - Asymmetric Public key created to identify a server to a user
  > # Session Key - Symmetric Key created by the client and the server that protects the communication for a particular session
> First Connect
  > ## RSA Key is saved to /home/<user>/.ssh/known_hosts file !!! Probably Important !!!
> Reconnect
  > # Wont prompt because the host is saved in the known_hosts file
> # If SSH gives an error that the rsa key is changed use this command:
  /> ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"
> View/change the ssh port, cat the known_hosts file and grep for port to check, and use vi to edit the file and change the port
> ssh files
> 	known hosts database: ~./ssh/known_hosts
> 	config files: /etc/ssh/ssh_config or sshd_config
# To view the current configured SSH port
> 	cat /etc/ssh/sshd_config | grep Port
# Edit file to change the SSH Port
> 	sudo nano /etc/ssh/sshd_config
# Restart the SSH Service
> 	systemctl restart ssh

## SSH-KEYGEN
> ssh-keygen -t rsa -b 4096 -C "Student"
> 	creates your own key
> 	-t is for encryption (rsa|dsa|ecdsa|ed25519), -b is bit length (1024|2048|4096), -C adds a comment 
> ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub

# SSH-COPY-ID
> ssh-copy-id student@172.16.82.106
> 	copies your ssh public key to the remote server
> 	saves key to ~/.ssh/authorized_keys on remote server
> 	allows authentication to server with key instead of password
> 	must secure your private key 

## HTTP(S) (TCP 80/443)
> User Request Methods
  > # GET / HEAD / POST / PUT
> User response codes
  > # 100,200,300,400,500
> Vulnerabilities
  > Flooding
  > Amplification
  > Low and slow
  > Drive-by Downloads
  > BeEF Framework


## DNS
> UDP 53 (Handles Queries/Responses)
> TCP 53 (Zone Transfer)
  > # When the server shares the domain information
> responses larger than 512 bytes use TCP
# DNS records
> A - IPv4
> AAAA - IPv6
> MX - mail server
> TXT - human-readable
> NS - name server
> SOA - start of authority 


## FTP
> Port 21
  > # command and control
> Port 20
  > # Data transfer
> Modes
  > # Active (Initiated on Port 21) <- Default
  > # Passive (Uses both ports)
> uses clear text
> suthentication or anonymous 

## TFTP (Port 69)
> # Clear-Text
> # Reliability provided at the application layer
> # used by routers and switches to transfer IOS and config files

SMTP (Port 25)
> # Internet standard used for sending electronic mail
> #  no encryption
> # smtp over TLS/SSL (SMTPs)
> 	TCP ports 587 and 465

POP (Port 110)
> # Used to retrieve electronic mail from a server
> # no sync with server and no encryption
> # POP3

IMAP (Port 143)
> # Download electronic mail from a server
> # sync with server
> # no encryption
> # IMAP4

DHCP (UDP Port 67/68)
> # Assigns IP Address parameters across an enterprise
> # DORA
> 	Discover (broadcast)
> 	Offer (unicast)
> 	Request (broadcast)
> 	Acknowledge (unicast)
> # vulnerabilities
>	rogue DHCP
>	evil twin
>	DHCP starvation

DHCPV6
> # if flag is set during SLAAC:
> 	Solicit (multicast)
> 	Advertise (unicast
> 	Request or information request (multicast)
> 	Reply (unicast)

NTP (UDP Port 123)
> # Allows for clock sync between computers over packet-switched data networks
> # vulnerable to crafted packet injection
> # stratum 0 - authoritative time source
> # up to stratum 15

## AAA protocols
> authentication,authorization and accounting
> for third party authentication

# TACACS (Port 49)
> # Used for centralized authentication, authorization, and accounting.
> # Cisco

# RADIUS (UDP 1645/1646 AND 1812/1813)
> # Open source networking protocol used for centralized autentication, authorization and accounting

# DIAMETER (TCP 3868)
> # exchange authentication, authorization, and accounting (AAA) information in Long-Term Evolution (LTE) and IP Multimedia Systems (IMS) networks.

# SNMP (UDP Port 161/162)
> # Collects and organizes information about managed devices on IP networks
> # versions:
> 	SNMPV1 - RFC 1157
> 	SNMPV2C - RFC 1441
> 	SNMPV3 - RFC 3410
> # 7 message types
> 	get request, set request, get next, get bulk, response, trap, inform
> # vulnerabilities
>	in V1 and 2C:
> 		weak community strings, lack of encryption, information disclosure, can be sniffed

# RTP (UDP ANY ABOVE 1023)
> # Streaming in real-time media over IP networks, designed for transmitting audio and video when speed is of essense


# RDP (Port 3389)
> # Remote Desktop
> # developed by miscrosoft
> 	no server software needed
> # other proprietary RDP software
> 	requires to have 3rd party software installed 

# Kerberos (UDP Port 88)
> # Network authentication protocol that ensures secure authentication for client-server applications.
> # used by active directory
> # mutual authentication
> # clients get tickets to access services 

# LDAP (Port 389 and 636)
> # Accessing and managing distributed directory information services
> # client/server model
> # directory schema
> # unsecure and secure versions 



