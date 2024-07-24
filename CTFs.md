# CAT README Notes
```
The map of the environment has been provided in your home directory:
    blue_range_complete.png

All activity PCAPS are provided here:
    /home/activity_resources/pcaps 

Below are a series of all the folders and commands you will use in this course.

    1. To view your IP address and interface information:
        a. current =        ip address (ip addr)
        b. deprecated =     ifconfig

    2. To view your ARP cache:
        a. current =        ip neighbor (ip nei)
        b. deprecated =     arp -a

    3. To view open TCP and UDP sockets:
        a. current = 
            i. TCP =        ss -antlp
            ii. UDP =       ss -anulp
        b. deprecated =     netstat

    4. To create, edit, or modify a file from the command line:
        a. vi =             vi <file>
        b. vim =            vim <file>
        c. nano =           nano <file>
    
    5. To view active processes:
        a. static =         ps -elf
        b. real-time =      top or htop

    6. To open file manager from the command line from X11 connection:
        a. nautilus
        b. pcmanfm

    7. Web Browsers from X11 connection:
        a. Firefox
        b. Chromium
        c. Konqueror

    8. To open images from the command line from X11 connection:
        a. Eye of Gnome =                   eog [file]
        b. Nomacs =                         nomacs [file]
        c. Eye of Mate =                    eom [file]
        d. GNU Image Manipulation Program = gimp [file]

    9. Find command:
        a. find / -iname <file pattern> 2>/dev/null
            / = starting location of search
            -iname = search for <file patter> with no case sensitivity
            <file pattern> = name of file to search for. Can use '*' as wildcards.
            2>/dev/null = send all errors to /dev/null

    10. Network scanning:
        a. nmap
            -sT = TCP Full connection
            -sS = TCP SYN scanning
            -Pn = Disable ping sweep
            -sU = UDP scanning
        b. zenmap
        c. netcat
            TCP: nc -nzvw1 10.10.0.40 21-23 80
            UDP: nc -unzv 10.10.0.40 53 69
        d. ping
        e. traceroute

    10. Network Utilization:
        a. iftop
        b. iptraf-ng

    12. Packet Manipulation (requires root privileges):
        a. scapy
        b. hping3
        c. yersinia     yersinia -G

    13. Packet Sniffing (requires root privileges):
        a. Wireshark
        b. tcpdump
        c. p0f
        d. tshark

    14. Banner Grabbing:
        a. netcat
            Client: nc 10.10.0.40 1234
        b. telnet
            telnet 10.10.0.40 1234
        c. wget
            wget -r http://10.10.0.40
            wget -r ftp://10.10.0.40
        d. curl
            curl http://10.10.0.40
            curl ftp://10.10.0.40

    15. DNS Query:
        a. whois
        b. dig
            Records:
                A - IPv4
                AAAA - IPv6
                NS - Name Server
                SOA - Start of Authority
                MX - Mail Server
                TXT - Human readable message
                AXFR - Zone Transfer

    16. Remote access:
        a. ssh
            ssh student@10.10.0.40
            ssh student@10.10.0.40 -p 2222
            ssh student@localhost -p 2222
        b. telnet
            telnet 10.10.0.40
            telnet 10.10.0.40 23
            telnet localhost 2222

    17. File Transfer:
        a. scp
            scp student@10.10.0.40:file .
            scp file student@10.10.0.40:
        b. netcat
            nc 10.10.0.40 1234 < file
            nc -lvp 1234 > file

    18. Creating SSH Tunnels:
        a. Local Port Forward
            ssh <user>@<ip> -p <ssh port> -L <local bind port>:<tgt ip>:<tgt port>
        b. Remote Port Forward
            ssh <user>@<ip> -p <ssh port> -R <remote bind port>:<tgt ip>:<tgt port>
        c. Dynamic
            ssh <user>@<ip> -p <ssh port> -D 9050

    19. To determine if tool or application is installed:
        a. which =              which <tool>
        b. whereis =            whereis <tool>

    20. Create a named pipe file:
        a. mknod =              mknod <file> -p
        b. mkfifo =             mkfifo <file>

    21. File and locations discusses:
        a. /etc/passwd =                List of user accounts
        b. /etc/shadow =                User password database
        c. /etc/ssh/ssh_config =        SSH user config 
        d. /etc/ssh/sshd_config =       SSH Daemon config
        e. ~/.ssh/known_hosts =         Public keys of all saved SSH servers
        f. /etc/snort =                 Snort directory
        g. /etc/snort/snort.conf  =     Snort config file
        h. /etc/snort/rules =           Default snort rules directory
        i. /var/log/snort =             Default snort log file directory
        j. /usr/share/cctc =            Default location of flags and files in shared environments
        k. /etc/proxychains.conf =      Proxychains config file
        l. /etc/p0f/p0f.fp =            p0f fingerprint file

    22. File descriptors:
        0 = Standard Input
        1 = Standard Output
        2 = Standard Error 

```
# CTF ANSWERS AND BREAKDOWNS
```
1. ARP Storm
5
What MAC address is initiating the ARP Storm?



```
