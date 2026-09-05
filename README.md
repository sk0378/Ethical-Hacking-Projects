[Home](https://github.com/sk0378/Ethical-Hacking-Projects/blob/Network-Traffic-Analysis-%26-Packet-Capture/Network_Analysis.md)

# Vulnerability Assessment & Exploitation

# Overview
Before exploiting a target, a proper security assessment starts with identifying what vulnerabilities actually exist on it. In this lab, I set up and ran OpenVAS (via the Greenbone Security Assistant web interface) to perform a full vulnerability scan against an OWASP Broken Web Application target, analyzed the resulting findings by severity, and identified critical, exploitable vulnerabilities in the target's services.

# Tools Used
| Tool | Purpose |
|------|---------|
| OpenVAS (Greenbone Vulnerability Manager) | Open-source vulnerability scanner used to identify security weaknesses on the target |
| Greenbone Security Assistant (GSA) | Web-based UI used to configure scans, manage tasks, and review vulnerability reports |

# Lab Environment
* Kali Linux – Attacker/analyst machine, running the OpenVAS scanner and manager services
* OWASP Broken Web App (BWA) – Target machine (192.168.68.12)

# What I Did

# Part 1 – Setting Up OpenVAS
Started the OpenVAS scanner and manager services on Kali, which loaded the vulnerability database and launched the Greenbone Security Assistant web interface:
```bash
systemctl status openvas-scanner
systemctl status openvas-manager
```
Logged into the Greenbone Security Assistant dashboard and reviewed the SecInfo Dashboard, which showed the scale of the vulnerability database in use: over 59,000 NVTs (Network Vulnerability Tests) and 144,000+ CVEs categorized by severity.
![Step 1](s1.png)
![Step 2](s2.png)
![Step 3](s3.png)

# Part 2 – Running an Immediate Vulnerability Scan
Launched an immediate scan against the OWASP BWA target IP directly from the dashboard, and monitored its progress as it worked through the target's services:
* Target: 192.168.68.12
* Scan Config: Full and very deep ultimate (the most thorough OpenVAS scan profile, covering 64 NVT families)
![Step 4](s4.png)
![Step 5](s5.png)

# Part 3 – Analyzing the Scan Report
Once the scan completed, reviewed the full results report, which returned 699 total findings. Several critical (10.0 High severity) vulnerabilities stood out immediately, including:
* **Tiki Wiki CMS Groupware End of Life Detection** — an outdated, unsupported CMS running on the target, a common real-world entry point for attackers
* **Apache Tomcat Manager/Host Manager/Server Status Default/Hardcoded Credentials** default credentials left active on an administrative interface
* Multiple high-severity Joomla! and Apache HTTP Server vulnerabilities

Also reviewed the built-in CVSS Base Score Calculator, which is used to manually compute a vulnerability's severity score from its access vector, complexity, and impact metrics.
![Step 6](s6.png)
![Step 7](s7.png)
![Step 8](s8.png)

# Part 4 – Creating a Reusable Scan Task
Rather than relying only on the one-off "Immediate Scan," configured a saved, named scan task ("OWASP Scan") targeting the OWASP asset group, using the same "Full and very deep ultimate" scan config, to demonstrate how a task can be reused, scheduled, or rerun for continuous assessment instead of a single ad hoc scan.
![Step 9](s9.png)
![Step 10](s10.png)
![Step 11](s11.png)

# Key Takeaways
* I learned that OpenVAS's "Full and very deep ultimate" scan profile is extremely thorough, checking against tens of thousands of NVTs across 64 categories, which is why a single scan can take a significant amount of time to complete
* The scan results reinforced how outdated software (like an end-of-life CMS) and default/hardcoded credentials remain some of the most common and highest-severity findings in real-world environments, and are often the easiest vulnerabilities for an attacker to exploit
* Reviewing the CVSS calculator helped me understand how a vulnerability's severity score is actually derived from its access vector, complexity, and required authentication, rather than treating a "High" severity rating as a black box
* Setting up a named, reusable scan task instead of only running immediate scans showed me how a real vulnerability management program works: scans need to be repeatable and scheduled, not just one-time checks, since new vulnerabilities are discovered constantly
* This lab reinforced why vulnerability scanning is the natural first step before any exploitation and that you can't prioritize what to test manually or exploit further without first knowing what's actually exposed on a target
