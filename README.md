[Home](https://github.com/sk0378/Ethical-Hacking-Projects/tree/Network-Traffic-Analysis-%26-Packet-Capture)

# Network Reconnaissance & Packet Analysis

# Overview
Before any exploitation can happen, an attacker first has to map out what's alive on a network and which doors are open. In this lab, I used hping3 to manually craft ICMP and TCP packets for host discovery, traceroute analysis, and port scanning, then used tcpdump to capture and correlate the traffic in real time. This hands-on, packet-level approach builds a much deeper understanding of how scanning tools work under the hood compared to relying on a single automated scanner.

# Tools Used
| Tool | Purpose |
|------|---------|
| hping3 | Command-line packet crafting tool used for host discovery, traceroute, and custom TCP/ICMP scans |
| tcpdump | Command-line packet capture tool used to record and correlate live traffic during scanning |

# Lab Environment
* Kali Linux – Attacker/analyst machine (192.168.9.2)
* OWASP Broken Web App (BWA) – Target machine (192.168.68.12)
* Local gateway/router – 192.168.9.1

# What I Did

# Part 1 – Host Discovery with ICMP
Used hping3 in ICMP mode to confirm the target host was alive and measure round-trip response times:
```bash
hping3 192.168.68.12
```
Sent ICMP timestamp requests (type 13) to gather originate, receive, and transmit timestamps from the target, another technique for confirming a live host and estimating clock skew:
```bash
hping3 -c 3 -1 -V -C 13 192.168.68.12
```
![Step 1](s1.png)
![Step 2](s2.png)

# Part 2 – Traceroute Analysis
Used hping3's traceroute mode with ICMP packets to map the path to the target and identify the local gateway as the first hop:
```bash
hping3 -c 5 -T -1 -V 192.168.68.12
```
![Step 3](s3.png)

# Part 3 – TCP Port Scanning & Packet Correlation
Opened a second terminal and started a live tcpdump capture on the interface to observe traffic in real time while scanning:
```bash
tcpdump -i eth0
```
In a separate terminal, sent crafted TCP SYN packets to specific ports using hping3, interpreting the returned TCP flags to determine port state. A SYN/ACK response confirmed an open port, while no response indicated the port was filtered or closed:
```bash
hping3 -S -c 1 -s 5151 -p 80 -V 192.168.9.1
hping3 -S -c 1 -s 5151 -p 22 -V 192.168.9.1
```
Port 80 responded with SYN/ACK flags (open), while port 22 returned 100% packet loss (filtered/closed) — and tcpdump's live capture confirmed the same SYN, SYN/ACK, and RST flag sequence for the correlating traffic.
![Step 4](s4.png)
![Step 5](s5.png)
![Step 6](s6.png)

# Part 4 – Full Range Port Scan
Ran a single hping3 command to scan a full range of ports (20-80) against the gateway, rather than testing each port individually:
```bash
hping3 -S -8 20-80 -c 1 -s 5151 -V 192.168.9.1
```
Out of the 61 ports scanned, only ports 53 (domain/DNS) and 80 (http) responded, with every other port in the range showing as unresponsive.
![Step 7](s7.png)

# Key Takeaways
* I learned that hping3 gives far more granular control over packet crafting than a standard scanner, letting me choose exact flags, source ports, and packet types to test host and port behavior manually
* ICMP timestamp requests are a lesser-known but useful host discovery technique, since some environments block standard ping (echo request) traffic but still respond to other ICMP types
* Running tcpdump alongside hping3 reinforced how a TCP three-way handshake attempt looks at the packet level, and how the returned flags (SYN/ACK vs. no response vs. RST) directly indicate a port's state
* Scanning a full port range in a single command was much more efficient than testing each port one at a time, and it's the same underlying principle that automated tools like Nmap use at scale
* This lab reinforced why understanding manual packet crafting matters even when automated tools exist — knowing what's happening at the protocol level makes it much easier to troubleshoot false positives/negatives or evade basic detection during a real assessment
