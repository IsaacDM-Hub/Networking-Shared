fin / -iname hint* 2>/dev/null
find / -iname flag* 2>/dev/null

BPF filter
  tcpdump 'ether[12:4] & 0xffff0fff = 0x810000abc'
  # looking at the vlan header (8100 header)
  ether[12:4]&0xffff0fff=0x81000001&&ether[16:4]&0xffff0fff=0x8100000a
  # this filters for vlan hopping from vlan 1 to vlan 10 (looks through the vlan tags) [double-tagging]

sudo iptables -P INPUT DROP (changes default policy)
                 OUTPUT
                 FORWARD

sudo iptables -P INPUT ACCEPT (IF NOT CHANGED TO THISBEFORE FLUSHING YOU W I L L LOCK OUT THE COMPUTER)
                  OUTPUT
                  FORWARD
## refer to filtering.md for good iptables and nftables syntax AND SNORT RULES 

Snort IDS/IPS General Rule options:
/> alert [tcp,udp,icmp] [SIP] [SPORT] [<-,->,<->] [DIP] [DPORT] (msg:<message>; sid:<ID>; rev:<rev number>;)
> msg:"text" - specifies the human-readable alert message
> reference: - links to external source of the rule
> sid: - used to uniquely identify Snort rules (required)
> rev: - uniquely identify revisions of Snort rules
> classtype: - used to describe what a successful attack would do
> priority: - level of concern (1 - really bad, 2 - badish, 3 - informational)
> metadata: - allows a rule writer to embed additional information about the rule

Snort Rules
> Installation Directory
  > /etc/snort
> Config file
  > /etc/snort/snort/conf
> Rules Directory
##  > /etc/snort/rules we will touch 
> Advanced IDS (snort) Rules
  > Rule naming
    > [name].rules
  > Default Log Directory
    > /var/log/snort

snort -D -l /var/log/snort/ -c /etc/snort/snort.conf 
#  runs snort as process, d for daemon, l for log placment and c for config 
To see binary log file in plain text along with hex
#  tcpdump -r <log file> -XX -vv -n
## running with just the -r will display the rules 

 Configure IPtables mangle rules
> Mangle examples with IPtables
 ##  /> iptables -t mangle -A POSTROUTING -o eth0 -j TTL --ttl-set 128      ets a new ttl remember for hard box
  /> iptables -t mangle -A POSTROUTING -o eth0 -j DSCP --set-dscp 26
































  
