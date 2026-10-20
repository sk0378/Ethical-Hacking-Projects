[Back to all projects](https://github.com/sk0378/Ethical-Hacking-Projects/tree/Network-Traffic-Analysis-%26-Packet-Capture)

# Ethical Hacking Projects 
# Author: Saniyyah Kelly

Hi, I'm Saniyyah Kelly, a Cybersecurity graduate student at Johns Hopkins University (Whiting School of Engineering) with a background in Computer Information Systems and Network Systems Management from CUNY Medgar Evers College. This repository documents hands-on vulnerability assessment and security labs I've completed, covering network analysis, vulnerability scanning, password auditing, and offensive security techniques using industry-standard tools in a Kali Linux environment and many more.

Each project lives on its own branch below, with a full write-up and screenshots documenting the process step-by-step.

## Current Focus

I am currently focused on vulnerability management and GRC; that being said,  this repository reflects the hands-on offensive security foundation behind that work.

## Skills & Tools

**Certifications:** CompTIA Security+ (In Progress) | TryHackMe Introduction to Cybersecurity Learning Path (June 2024) | Google Cybersecurity Certificate (Expected - December/2026)

**Offensive Security Tools:** Nmap, Wireshark, Metasploit, msfvenom, John the Ripper, Hashcat, CeWL, Crunch, tcpdump, Scapy, hping3, Xplico, Armitage

**Risk & Vulnerability Analysis:** CVSS Scoring, OpenVAS/Greenbone, & Vulnerability Prioritization

**Platforms & Languages:** Kali Linux, GCP, Virtual Machines, PowerShell, Python

## Projects

| Project | Summary |
|---------|---------|
| [Vulnerability Assessment with OpenVAS](https://github.com/sk0378/Ethical-Hacking-Projects/blob/Vulnerability_Assessment_with_OpenVAS/README.md) | Deployed OpenVAS/Greenbone to run a full-depth vulnerability scan against an OWASP target, identifying critical (CVSS 10.0) findings including an end-of-life TikiWiki CMS and default Apache Tomcat credentials.|
| [Password Cracking & Wordlist Generation](https://github.com/sk0378/Ethical-Hacking-Projects/blob/password_cracking_wordlist_generation/README.md) | Built custom wordlists with CeWL and Crunch, merged them with John the Ripper's dictionary, then cracked SHA-512 Linux password hashes using both John the Ripper and Hashcat. |
| [System Hacking & Privilege Escalation](https://github.com/sk0378/Ethical-Hacking-Projects/blob/System_Hacking_%26_Privilege_Escalation/README.md) | Performed Nmap reconnaissance against a Windows Active Directory target, delivered a custom Meterpreter payload with msfvenom, and escalated privileges to NT AUTHORITY\SYSTEM, followed by hash dumping and remote command execution. |
| [Network Reconnaissance & Packet Analysis](https://github.com/sk0378/Ethical-Hacking-Projects/blob/Network_Reconnaissance_%26_Packet_Analysis/README.md) | Used hping3 and Scapy to perform host discovery, port scanning, and custom packet crafting at the protocol level, validating results against Wireshark captures. |
| [Network Traffic Analysis & Packet Capture](https://github.com/sk0378/Ethical-Hacking-Projects/blob/Network-Traffic-Analysis-%26-Packet-Capture/Network_Analysis.md) | Captured live traffic with tcpdump, generated multi-protocol activity against an OWASP target, and reconstructed full TCP sessions in Wireshark to expose cleartext data on unencrypted connections. |


## NOTE

All labs were performed in a practical, isolated NETLAB+ environment using OWASP BWA and Windows Server VMs; no unauthorized systems were accessed :)
