============== Network Traffic Sniffing ================
 Packet Capture Libraries
> LibCap
> WinPcap
> NPcap
Tools And Methods
> Disadvantages
  > # Can only capture what NIC can see
  > # Cannot capture local traffic
  > # Lost packets on busy networks
  > # Requires elevate permissions
  > # Can sonsume massive amounts of local storage


Packet Sniffers
> Hardware
  > # Something that can be plugged in to capture packets (Not Software)
> Software
  > # Wireshark


Socket Types
> User Space Sockets
  > # Stream Socket (Normally used with TCP/SCTP)
  > # Datagram Socket (Normally used with UDP)
  [EXAMPLE tcpdump]
> Kernel Space Sockets
  > # Raw Socket (receiving of IP packets without automatic protocol-specific transport layer formatting)


Types of Sniffing
> Active
  > # Actually interacting with the device
  > # OS Fingerprinting
  > # Nmap scan
> Passive
  > # Listening to all traffic (All look no touch)


Interface Naming
> Traditional
  > # eth0, eth1
> Consistent
  > # en0, en1


TCPDUMP Primitives
> User Friendly cpature expressions aka human readable
  > # src or dst
  > # host, net, port, portrange
  > # tcp or udp

TCPDUMP Options !!!!!!!!!!
> -A
  > # Prints frame payload in ASCII
> -D
  > # Print list of network interfaces available on the system
> -i
  > # Select a different interface
> -e
  > # Prints data-link headers (MAC adresses)
> -r 
  > # Reads from pcap
> -w
  > # Writes the capture to an output file
> -X
  > # Displays packet data in hex
> -XX
  > # Displays everything in hex (Including Layer 2)
> -vv/v/vvv
  > # Gives verbose output with detail on the TTL, IPID, ect.
> -n
  > # Does not convert protocol and addresses to names
  [EXAMPLE]
  /> tcpdump port 80 or 22 -vn
    > # TCPDUMP for specific protocol traffic
/> tcpdump <pcap> -XX -vv
  > # Magic command (Gives everything)
/> tcpdump <protocol>

Compare Primitives and BPFS
> Primitives [MORE SIMPLE]
  > # CMU/Stanford Packet Filter (CSPF) Model commonly called Boolean Expression Tree
  > # Simple and easy filter expressions
  > # First user-level packet filter model
  > # Memory-stack-based filter machine which can create bottlenecks on model CPUs
  > # can have redundant computations of the same information
> Berkley Packet Filters (BPF) [MORE COMPLICATED BUT CAN BE MORE SPECIFIC]
  > # Control Flow Graph (CFG) Model
  > # Uses a simple (non-shared) buffer model which can make it 1.5 to 20 times faster than CSPF
  > # Can be more complex to create expressions but offer far more precision
  > # Faster because you can set it to look at specific things and doesnt show you bloated information (Saves Computational Power)

## construct BPF
Kernel API
> TCPDUMP requests a RAW Socket creation
> Filters are set using the SO_ATTACH_FILTER
  > # Allows us to attach a bpf to the socket to capture the incoming packets


BPF Virtual Machine
> Consists of an accumulator
> Index register
> Scratch memory store


TCPDump filtering with BPF’s and bit-masking [SYNTAX] !!!!!!!!!!
----[ tcpdump {A} [B:C] {D} {E} {F} {G} ]----
> A = Protocol (ether | arp | ip | ip6 | icmp | tcp | udp)
> B = Header Byte number
> C = optional: Byte Length. Can be 1, 2 or 4 (default 1)
> D = optional: Bitwise mask (&)
> E = Operator (= | == | > | < | <= | >= | != | () | << | >>)
> F = Result of Expression
> G = optional: Logical Operator (&& ||) to bridge expressions

[EXAMPLE]
 /> tcpdump 'ether[12:2] = 0x0800 && (tcp[2:2] != 22 || tcp[2:2] != 23)'
 /> tcpdump -r BPFCheck.pcap 'ip[8] <= 64 || ip6[7] <= 64'


BitWise Masking
> Can Read 1 (BYTE), 2 (HALF-WORD), or 4 (WORD)
> Will only filter the byte level (alone)
> binary 0 to ignore bit or 1 to match bit
[EXAMPLES]
  /> tcpdump 'ether[12:4] & 0xffff0fff = 0x810000abc'
    > # looking at the vlan header (8100 header)
    > oxffff0ffff
        ||||-||||
    >   810000abc
     > # [f] is all bits on
     > # [0] is no bits
    > # fc is the same as 0xffff00
  /> tcpdump 'ip[1] & 252 = 32'
> More frament flag
 /> tcpdump 'ip[6:2] & 0x1fff > 0'
  > # This looks at the ip header


BPF [EXAMPLES]
/> tcp[0:2]=53||tcp[2:2]=53||udp[0:2]=53||udp[2:2]=53'
 > # this filters for any packet that uses dns protocol
/> ip[9]=0x11||ip6[6]=0x11
 > # this filters for packets that are using udp
/> ip[4:2]=213
 > # this filters for packets that have the ip ID of 213
/> tcp[0:2]>1024||udp[0:2]>1024'
 > # this filters for packets that have a source port greater than 1024
/> tcp[13]=0x10
 > # this filters for SYN-ACK in tcp
/> tcp[13]=0x04
 > # this filters for RST in tcp
/> tcp[2:2]<1024||udp[2:2]<1024
 > # this filters for well-known ports in tcp and udp
/> tcp[0:2]=80||tcp[2:2]=80
 > # this filters for all http traffic
/> ether[12:2]=0x0806
 > # this filters for arp
/> ip[6]&0x80=0x80
 > # this filters for the reserved bit "EVIL BIT"
/> tcp[13]&0x20=0&&tcp[18:2]!=0'
 > # this filters for the URG bit not being set and the URG pointer having a value
/> tcp[13]=0&&ip[16:4]=0x0a0a0a0a
 > # this filters for tcp null scan to the destination ip 10.10.10.10
/> ip[8]=1&&(ip[9]=0x01||ip[9]=0x11)'
 > # this filters for traceroute being used
/> ether[12:4]&0xffff0fff=0x81000001&&ether[16:4]&0xffff0fff=0x8100000a
 > # this filters for vlan hopping from vlan 1 to vlan 10 (looks through the vlan tags) [double-tagging]

## BPFs at the data link layer
> # Search for the destination broadcast MAC address.
>  'ether[0:4] = 0xffffffff && ether[4:2] = 0xffff'
>  'ether[0:2] = 0xffff && ether[2:2]= 0xffff && ether[4:2] = 0xffff'
> # Search for the source MAC address of fa:16:3e:f0:ca:fc.
>  'ether[6:4] = 0xfa163ef0 && ether[10:2] = 0xcafc'
>  'ether[6:2] = 0xfa16 && ether[8:2] = 0x3ef0 && ether[10:2] = 0xcafc'

> # Search for unicast (0x00) or multicast (0x01) MAC address.
>   'ether[0] & 0x01 = 0x00'
>   'ether[0] & 0x01 = 0x01'
>   'ether[6] & 0x01 = 0x00'
>   'ether[6] & 0x01 = 0x01'

> # Search for IPv4, ARP, VLAN Tag, and IPv6 respectively.
>  ether[12:2] = 0x0800
>  ether[12:2] = 0x0806
>  ether[12:2] = 0x8100
>  ether[12:2] = 0x86dd

> # Search for 802.1Q VLAN 100.
>  'ether[12:2] = 0x8100 && ether[14:2] & 0x0fff = 0x0064'
>  'ether[12:4] & 0xffff0fff = 0x81000064'

># Search for double VLAN Tag.
>  'ether[12:2] = 0x8100 && ether[16:2] = 0x8100'

## BPFs at the network layer
> # Search for IHL greater than 5.
>  'ip[0] & 0x0f > 0x05'
>  'ip[0] & 15 > 5'

> # Search for ipv4 source or destination address of 10.1.1.1.
>  'ip[12:4] = 0x0a010101'
>  'ip[16:4] = 0x0a010101'

> # Search for ipv6 source or destination address starting with FE80.
>  'ip6[8:2] = 0xfe80'
>  'ip6[24:2] = 0xfe80'

> # Search for TCP Flags set to ACK+SYN. No other flags can be set.
>  'tcp[13] = 0x12'

> # Search for TCP Flags set to ACK+SYN. The other flags are ignored.
>  'tcp[13] & 0x12 = 0x12'

## DESCRIBE PASSIVE OS FINGERPRINTING (P0F)
Similar to tcpdump except it only captures traffic that matches signatures in its database file.

> # P0F database
> less /etc/p0f/p0f.fp

> # help
>  p0f -h

# run on interface
 p0f -i eth0

# RUN P0F ON A PCAP
p0f -r capture.pcap

# OUTPUT TO GREPPABLE LOG FILE
p0f -r wget.pcap -o /var/log/p0f.log
cat /var/log/p0f.log | grep {expression}




































