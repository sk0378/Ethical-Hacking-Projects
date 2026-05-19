# Lab 06: Network Analysis
# Course: Ethical Hacking | Platform: NETLAB+

# Overview
Network analysis is a critical skill in cybersecurity. Being able to capture and inspect network traffic allows security professionals to detect intrusions, investigate breaches, and understand how attackers move through a network. In this lab, I used industry-standard tools to capture live network traffic and analyze it for suspicious or sensitive activity.

# Tools Used
ToolPurposetcpdumpCommand-line packet capture tool used to record raw network trafficWiresharkGUI-based traffic analyzer used to inspect captured packets in detailsmbclientLinux tool used to interact with SMB file shares

# Lab Environment
* Kali Linux – Attacker/analyst machine (192.168.9.2)
* pfSense – Firewall/router separating network segments
* OWASP Broken Web App (BWA) – Intentionally vulnerable target machine (192.168.68.12)


# What I Did
# Part 1 – Capturing Traffic with tcpdump

Logged into Kali Linux and used tcpdump to begin capturing all packets on the network interface, saving them to a .pcap file for later analysis:
bashtcpdump -i eth0 -s0 -w testdump.pcap
While the capture was running, I also generated the real network traffic by:

_Connecting to an SMB file share on the OWASP target machine using smbclient
Browsing to the target machine's web server via Firefox and clicking on links_

This simulates what an analyst would do when capturing traffic during a security assessment or incident investigation.
![Step 1](Step%201.png)
![Step 2](Step%202.png)
![Step 3](Step%203.png)
![Step 4](Step%204.png)
![Step 5](Step%205.png)
![Step 6](Step%206.png)
![Step 7](Step%207.png)

# Part 2 – Analyzing Traffic with Wireshark
Opened the saved testdump.pcap file in Wireshark and performed the following analysis:

* SMB Filter – Isolated SMB (file sharing) traffic to see the authentication and file share activity that was captured
* HTTP Filter – Isolated web traffic and inspected individual GET requests, including headers, source/destination IPs, and browser information
* Follow TCP Stream – Reassembled a full TCP conversation from start to finish, allowing me to read the complete exchange between the client and server
![Step 8](Step%208.png)
![Step 9](Step%209.png)
![Step 10](Step%2010.png)
![Step 11](Step%2011.png)
![Step 12](Step%2012.png)
![Step 13](Step%2013.png)
![Step 14](Step%2014.png)

# Key Takeaways
* I learned that tcpdump is widely used by security analysts and penetration testers to capture traffic quietly from the command line,  especially on servers with no GUI
* As for Wireshark, it's known to be the industry standard for packet analysis and is used in incident response, network forensics, and penetration testing itself
* I also learned that the SMB traffic can expose credentials and file access patterns that's not properly encrypted, which is a common target in real-world attacks
* HTTP traffic is unencrypted by default, meaning sensitive data like login info can be visible in a packet capture
* And the Follow TCP Stream feature, which is a powerful way to reconstruct what happened during a network session
