# Ethical Hacking Projects

Hi, I'm Saniyyah Kelly — a Cybersecurity graduate student at Johns Hopkins University (Whiting School of Engineering) with a background in Computer Information Systems and Network Systems Management from CUNY Medgar Evers College. This repository documents hands-on offensive security labs I've completed, covering network analysis, password cracking, exploitation, and post-exploitation techniques using industry-standard tools in a Kali Linux environment.

Each project lives on its own branch below, with a full write-up and screenshots documenting the process step by step.

## Skills & Tools

**Certifications:** CompTIA Security+ (In Progress) · TryHackMe Introduction to Cybersecurity Learning Path (June 2024) · HubSpot Social Media Certification (October 2023)

**Offensive Security Tools:** Nmap, Wireshark, Metasploit, msfvenom, John the Ripper, Hashcat, CeWL, Crunch, tcpdump, Scapy, hping3, Xplico, Armitage

**Platforms & Languages:** Kali Linux, GCP, Virtual Machines, PowerShell, Python

**Other:** Microsoft Office, Google Workspace

## Projects

| Project | Summary |
|---------|---------|
| [Network Traffic Analysis & Packet Capture](https://github.com/sk0378/Ethical-Hacking-Projects/tree/Network-Traffic-Analysis-%26-Packet-Capture) | Captured live traffic with tcpdump, generated multi-protocol activity against an OWASP target, and reconstructed full TCP sessions in Wireshark to expose cleartext data on unencrypted connections. |
| [Password Cracking & Wordlist Generation](https://github.com/sk0378/Ethical-Hacking-Projects/tree/password_cracking_wordlist_generation) | Built custom wordlists with CeWL and Crunch, merged them with John the Ripper's dictionary, then cracked SHA-512 Linux password hashes using both John the Ripper and Hashcat. |
| [System Hacking & Privilege Escalation](https://github.com/sk0378/Ethical-Hacking-Projects/tree/System_Hacking_%26_Privilege_Escalation) | Performed Nmap reconnaissance against a Windows Active Directory target, delivered a custom Meterpreter payload with msfvenom, and escalated privileges to NT AUTHORITY\SYSTEM, followed by hash dumping and remote command execution. |
| Network Reconnaissance & Packet Analysis | Used hping3 and Scapy to perform host discovery, port scanning, and custom packet crafting at the protocol level, validating results against Wireshark captures. |
| Vulnerability Assessment & Exploitation | Configured Metasploit with a PostgreSQL backend, scanned an OWASP target with WMAP, and exploited a TikiWiki CMS remote code execution vulnerability to gain and enumerate a remote shell. |
