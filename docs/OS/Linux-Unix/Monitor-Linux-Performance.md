### vmstat

Linux VmStat command used to display statistics of virtual memory, kernerl threads, disks, system processes, I/O blocks, interrupts, CPU activity and much more. By default vmstat command is not available under Linux systems you need to install a package called sysstat that includes a vmstat program. The common usage of command format is.

### lsof

Lsof command used in many Linux/Unix like system that is used to display list of all the open files and the  processes. The open files included are disk files, network sockets, pipes,
devices and processes. One of the main reason for using this command is when a disk cannot be unmounted and displays the error that files are being used or opened. With this commmand you can easily identify which files are in use. The most common format for this command is:
```
lsof
```

### Tcpdump
Tcpdump is one of the most widely used command- line network packet analyzer or packets sniffer program that is used capture or filter TCP/IP packets that received or transferred on a specific interface over a network. It option to save captured packages in a file for later analysis. tcpdump is almost available in all major Linux distributions.
```
tcpdump -i eth0
```

### Netstat
Netstat is a command line tool for monitoring incoming and outgoing network packets statistics as well as interface statistics. It is very useful tool for every system administrator to monitor network performance and troubleshoot network related problems.
```
netstat -a | more
```

### Htop – Linux Process Monitoring
Htop is a much advanced interactive and real time Linux process monitoring tool.  This is much similar to Linux top command but it has some rich features like user friendly interface to manage process, shortcut keys, vertical and horizontal view of the processes and much more. 

### Iotop – Monitor Linux Disk I/O
Iotop is also much similar to top command and Htop program, but it has accounting function to monitor and display real time Disk I/O and processes. This tool is much useful for finding the exact process and high used disk read/writes of the processes.

### Iostat – Input/Output Statistics
IoStat is simple tool that will collect and show system input and output storage device statistics.  This tool is often used to trace storage device performance issues including devices, local disks, remote disks such as NFS.

### IPTraf – Real Time IP LAN Monitoring
IPTraf is an open source console- based real time network (IP LAN) monitoring utility for Linux. It collects a variety of information such as IP traffic monitor that passes over the network, including TCP flag information, ICMP details, TCP/UDP traffic breakdowns, TCP connection packet and byne counts. It also gathers information of general and detaled interface statistics of TCP, UDP, IP, ICMP, non-IP, IP checksum errors, interface activity etc.

### Psacct or Acct – Monitor User Activity
psacct or acct tools are very useful for monitoring each users activity on the system. Both daemons runs in the background and keeps a close watch on the overall activity of each user on the system and also what resources are being consumed by them.  These tools are very useful for system administrators to track each users activity like what they are doing, what commands they issued, how much resources are used by them, how long they are active on the system etc.

### Monit – Linux Process and Services Monitoring
Monit is a free open source and web based process supervision utility that automatically monitors and managers system processes, programs, files, directories, permissions, checksums and filesystems.  It monitors services like Apache, MySQL, Mail, FTP, ProFTP, Nginx, SSH and so on. The system status can be viewed from the command line or using it own web interface.

### NetHogs – Monitor Per Process Network Bandwidth
NetHogs is an open source nice small program (similar to Linux top command) that keeps a tab on each process network activity on your system. It also keeps a track of real time network traffic bandwidth used by each program or application.

### iftop – Network Bandwidth Monitoring
iftop is another terminal-based free open source system monitoring utility that displays a frequently updated list of network bandwidth utilization (source and destination hosts) that passing through the network interface on your system. iftop is considered for network usage, what ‘top‘ does for CPU usage. iftop is a ‘top‘ family tool that monitor a selected interface and displays a current bandwidth usage betwee

### Monitorix – System and Network Monitoring
Monitorix is a free lightweight utility that is designed to run and monitor system and network resources as many as possible in Linux/Unix servers. It has a built in HTTP web server that regularly collects system and network information and display them in graphs. It Monitors system load average and usage, memory allocation, disk driver health, system services, network ports, mail statistics

### SArpwatch – Ethernet Activity Monitor
Arpwatch is a kind of program that is designed to monitor Address Resolution (MAC and IP address changes) of Ethernet network traffic on a Linux network. It continuously keeps watch on Ethernet traffic and produces a log of IP and MAC address pair changes along with a timestamps on a network. It also has a feature to send an email alerts to administrator, when a pairing added or changes.  It is very useful in detecting ARP spoofing on a network.

### Suricata – Network Security Monitoring
Suricata is an high performance open source Network Security and Intrusion Detection and Prevention Monitoring System for Linux, FreeBSD and Windows.It was designed and owned by a non- profit foundation OISF (Open Information Security Foundation).


