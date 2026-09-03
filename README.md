[Back to all projects](https://github.com/sk0378/Ethical-Hacking-Projects/tree/Network-Traffic-Analysis-%26-Packet-Capture)

# Password Cracking & Wordlist Generation

# Overview
Weak and reused passwords remain one of the most common ways attackers gain access to systems. Understanding how password hashes are stored, cracked, and defended against is a core skill in cybersecurity. In this lab, I built custom wordlists from target-specific data and used industry-standard cracking tools to recover passwords from Linux password hashes, simulating how an attacker or penetration tester would approach a real password audit.

# Tools Used
| Tool | Purpose |
|------|---------|
| CeWL | Spiders a target website and generates a custom wordlist from the words found on it |
| Crunch | Generates wordlists from scratch based on defined character sets and length rules |
| unshadow | Combines /etc/passwd and /etc/shadow into a single crackable file |
| John the Ripper | Command-line password cracking tool used to crack hashed passwords |
| Hashcat | GPU/CPU-accelerated password recovery tool used to crack hashes at high speed |
| Mousepad | Text editor used to inspect and reformat hash files for compatibility with Hashcat |

# Lab Environment
* Kali Linux – Attacker/analyst machine
* OWASP Broken Web App (BWA) – Intentionally vulnerable target machine (192.168.68.12), used as the source site for wordlist generation
* Two local test accounts (fake3, fake4) were created to simulate real user credentials to crack

# What I Did

# Part 1 – Building Custom Wordlists
Used CeWL to spider the OWASP BWA target site and pull words directly off the pages into a custom wordlist, since real-world passwords are often based on content specific to a target (company names, product names, staff names, etc.):
```bash
cewl -w owaspwords.txt -d 2 -m 5 192.168.68.12
```
Used Crunch to generate a brute-force style wordlist from scratch, based on a defined character set and word length:
```bash
crunch 4 8 charset.lst lalpha -o list.txt
```
Combined the CeWL wordlist, the Crunch wordlist, and John the Ripper's built-in default password list into a single master wordlist for cracking:
```bash
cat owaspwords.txt list.txt > mylist.txt
cat /usr/share/john/password.lst >> mylist.txt
```
![Step 1](s1.png)
![Step 2](s2.png)
![Step 3](s3.png)
![Step 4](s4.png)
![Step 5](s5.png)
![Step 6](s6.png)

# Part 2 – Creating Test Accounts & Extracting Hashes
Created two local user accounts with known passwords to simulate real credentials that would need to be cracked:
```bash
useradd fake3
useradd fake4
passwd fake3
passwd fake4
```
Reviewed /etc/shadow to see how the passwords were stored as salted hashes, then used unshadow to merge /etc/passwd and /etc/shadow into a single file that John the Ripper can read, and isolated just the two test accounts into their own file:
```bash
cat /etc/shadow
unshadow /etc/passwd /etc/shadow > hashes.txt
cat hashes.txt | grep fake* > hashes2.txt
```
![Step 7](s7.png)
![Step 8](s8.png)
![Step 9](s9.png)
![Step 10](s10.png)
![Step 11](s11.png)

# Part 3 – Cracking Passwords with John the Ripper
Ran John the Ripper against the extracted hashes using the built-in default password list, then used the --show flag to confirm the recovered plaintext passwords:
```bash
john --wordlist=/usr/share/john/password.lst hashes2.txt
john --show hashes2.txt
```
Both test accounts were cracked successfully: fake3 (123456) and fake4 (password).
![Step 12](s12.png)
![Step 13](s13.png)
![Step 14](s14.png)

# Part 4 – Cracking Passwords with Hashcat
Reviewed Hashcat's usage options, then opened the hash file in Mousepad to reformat it, stripping it down to just the raw sha512crypt ($6$) hash strings since Hashcat requires a specific input format rather than the full passwd-style line John uses:
```bash
hashcat -h | more
```
Ran Hashcat against the reformatted hash file using the custom mylist.txt wordlist built in Part 1, cracking the hashes a second time with a different tool to confirm the results:
```bash
hashcat -m 1800 hashes3.txt mylist.txt
```
![Step 15](s15.png)
![Step 16](s16.png)
![Step 17](s17.png)
![Step 18](s18.png)
![Step 19](s19.png)
![Step 20](s20.png)
![Step 21](s21.png)

# Key Takeaways
* I learned that CeWL is a useful reconnaissance tool for building target-specific wordlists, since people and organizations often base passwords on words tied to their own websites, branding, or names
* Crunch showed me how quickly a brute-force wordlist can grow — even a small character set and length range produced tens of millions of possible passwords
* I also learned that /etc/shadow stores password hashes with salts, and how unshadow combines it with /etc/passwd to create a file that cracking tools can actually work with
* John the Ripper's default wordlist alone was enough to crack both test passwords almost instantly, reinforcing how dangerous weak, common passwords like "123456" and "password" really are
* Hashcat requires a stricter input format than John, so I learned the importance of correctly formatting hash files before running a cracking tool against them
* Cracking the same hashes with two different tools (John and Hashcat) reinforced how consistent and reproducible password auditing results are, and why organizations perform these audits to catch weak credentials before attackers do
