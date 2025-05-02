# Cybersecurity notes & resources
## 📚 Table of Contents

- [Cybersecurity notes \& resources](#cybersecurity-notes--resources)
  - [📚 Table of Contents](#-table-of-contents)
- [Websites](#websites)
  - [Search Engines \& DBs](#search-engines--dbs)
  - [Documentation](#documentation)
  - [Others](#others)
- [Linux \& Shell Resources](#linux--shell-resources)
- [Tools \& Packages](#tools--packages)
  - [Package Management Concepts](#package-management-concepts)
- [Cyptography](#cyptography)
- [Cybersecurity Terms](#cybersecurity-terms)
  - [Industry Terms and Systems](#industry-terms-and-systems)
  - [Adversarial Techniques](#adversarial-techniques)
  - [Security Assessment Methods](#security-assessment-methods)
- [Computer Terms \& System Basics](#computer-terms--system-basics)

# Websites

## Search Engines & DBs

- **Shodan**: for devices connected to the Internet
    - https://www.shodan.io/
    - allows search for specific types and versions of *servers*; networking equipment; industrial control systems; and IoT devices (in specific areas / cities)
    - offers API
    - Query Cases: https://www.shodan.io/search/examples

- **Censys**: for internet-connected *hosts, websites, certificates*, and other Internet assets
    - https://search.censys.io/
    - offers API
    - Docs: https://docs.censys.com/docs/ls-quick-start#/

- **Virustotal**: website that provides virus-scanning service for files using antivirus engines
    - https://www.virustotal.com/gui/home/upload
    - allows users to scan files via url, IP, domain, upload, or file hash

- **Have I Been Pwned (HIBP)**: tells you if an *email address* has appeared in a leaked data breach
    - https://haveibeenpwned.com/
    - see if email address has been pwned, and if info has been *pasted* (to a publicly facing website designed to share content such as Pastebin)

- **Common Vulnerabilities and Exposures (CVE)**:  a dictionary of vulnerabilities for quick bug lookups
    - https://www.cve.org/
    - provides a standardized identifier for vulnerabilities and security issues in software and hardware products (e.g. CVE-2024-29988)
    - simple id and description

- **National Vulnerability Database (NVD)**: government-hosted vulnerability database for risk analysis & policy decisions
    - https://nvd.nist.gov/#
    - run by NIST (National Institute of Standards and Technology)
    - enriches CVEs; adds CVSS scores (severity ratings), Impact metrics (confidentiality, integrity, availability), Affected products, Mitigation/remediation advice, References and patch links

- **Exploit Database**: publicly archive of exploit code
    - http://exploit-db.com/
    - has exploits and proof-of-concept (PoC) code for known software vulnerabilities
    - searchable by CVE id, software name, or platform

## Documentation

- **Linux Documentation Searchup**:
  - linux.die.net

- **Microsoft Documentation**: official technical documentation for all Microsoft products
    - https://learn.microsoft.com/zh-cn/

- **Apache Documentation**: official Apache http server documentation
    - https://httpd.apache.org/docs/

- **PHP Documentation**: official PHP documentation
    - https://www.php.net/manual/en/index.php

- **Node.js Documentation**: official Node.js documentation
    - https://nodejs.org/docs/latest/api/


## Others

- **PasteBin**: temporary text/code storage and sharing platform with password and burn-after-read features, etc.
    - https://pastebin.com/


# Linux & Shell Resources

- **DigitalOcean Community Tutorials**  
  - https://www.digitalocean.com/community/tutorials  
  - Practical, high-quality guides for Linux, servers, networking, and sysadmin tasks

- **Linuxize**  
  - https://linuxize.com  
  - Clear explanations of Linux commands, tools, and scripting

- **How-To Geek (Linux)**  
  - https://www.howtogeek.com/tag/linux/  
  - Beginner-friendly articles with real examples of command usage

- **OverTheWire: Bandit Game**  
  - https://overthewire.org/wargames/bandit/  
  - Gamified way to learn Linux basics and shell skills through puzzles

- **TryHackMe: Linux Fundamentals & Labs**  
  - https://tryhackme.com  
  - Interactive cybersecurity platform with beginner-friendly Linux labs


# Tools & Packages

- gobuster: https://github.com/OJ/gobuster
    - *tool for bruteforcing websites Directory/File, DNS and VHost written in Go*
    - e.g.          gobuster dns -d google.com -w ~/wordlists/subdomains.txt -i
    - e.g.          gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt

- **WireShark**
  - an open-source cross-platform network packet analyser tool capable of investigating live traffic and inspecting packet captures (PCAP)
  - can detect & troubleshoot network problems, detect security anomalies, investigate & learn protocol details
  - not an IDS (Intrusion Detection System)
  - https://tryhackme.com/room/wiresharkthebasics
  - each packet consists of 5~7 layers (OSI Model)
  - searching packets:
    - need to know input type (Display filter, Hex, String, Regex) (case sensitivity can be toggled) & search field (packet list, packet details, packet bytes)

## Package Management Concepts

- **APT (Advanced Package Tool)**
  - package management system used by Debian-based Linux distributions
  - allows users to install, update, and remove software while resolving dependencies automatically
  - fetches packages from online repositories defined in system config files
  - see related commands in [linux_notes.md – apt](linux_notes.md#package-management)
  - **GPG Keys (GNU Privacy Guard)**
    - cryptographic keys used to verify the authenticity of software packages and repositories
    - APT checks repository signatures against trusted GPG keys before allowing installations
    - missing or invalid GPG keys can cause APT to reject package updates with errors like `NO_PUBKEY`
  
- **Adding a package from a third-party repository (APT workflow):**
  1. **Add GPG key** to trust the source  
     `wget -qO - <key-url> | sudo apt-key add -`
  2. **Add repository** to `/etc/apt/sources.list.d/`  
     (e.g., write a `deb https://...` line to a new `.list` file)
  3. **Update package index**  
     `sudo apt update` — fetches the latest package info from the new repo
  4. **Install the package**  
     `sudo apt install <package-name>`
  - `apt update` only refreshes package info — it does **not install** anything.


# Cyptography

- **AES (Advanced Encryption System)**: ==TODO==

# Cybersecurity Terms

## Industry Terms and Systems

- **Security Operations Center (SOC)**: 
    - a team that monitors the networks and its systemts to detect malicious cybersecurity events

- **DFIR (Digital Forensics and Incident Response)**:
    - covers:
    - **Digital Forensics**: analyzing evidence of an attack and its perpetrators
      - file systems, system memory, system logs, network logs, etc.
    - **Incident Response**: the methodology that should be followed to handle cyber attacks
      - Preparation -> Detection and Analysis -> Containment, Eradication, and Recovery -> Post-Incident Activity

- **SIEM (Security Information and Event Management)**:
  - a system that collects, aggregates, and analyzes log data from across systems and apps
  - helps identify abnormal or sus behavior and supports alerting and forensics analysis
    

## Adversarial Techniques

- **Malware**: malicious software, has many types:
  - **Virus**: a piece of code that attaches itself to a program
    - designed to spread from one computer to another and works by altering, overwriting and deleting files once it infects
  - **Trojan Horse**: a program that shows a desirable function but hides a malicious function underneath
  - **Ransomware**: encrypts user's files, making the files unreadable without knowing the encryption password
    - attacker offers to unlock with a ransom
  
## Security Assessment Methods

- **Static Analysis**: a security assessment of inspecting the malware without running it
- **Dynamic Analysis**: runs the malware in a controlled environment and monitors its activities

# Computer Terms & System Basics

- **Processes**
  - OS uses namespaces to split up resources (CPU, RAM, priority)
  - only processes that are in the same namespace can see each other
  - for linux see [linux process commands](linux_notes.md#processes)
  - **PID**: unique identifier assigned to each running process in a system
    - usually sequential order but can be recycled
  - e.g. `systemd` command (system's init on Ubuntu) has PID 1; every thing that starts is a child process of `systemd`
  - *when executing scripts, `Ctrl+Z` can background a process.*
  - **flags**: 
    -  Main States:
       - `R`: **Running** – process is on the CPU or ready to run  
       - `S`: **Sleeping** – waiting for an event (e.g., I/O)  
       - `D`: **Uninterruptible sleep** – waiting for disk/I/O, can't be killed  
       - `T`: **Stopped** – paused by job control or debugger  
       - `Z`: **Zombie** – finished but not cleaned up by parent  
       - `X`: **Dead** – defunct (very rare)
    - Additional Flags:
      - `+`: **Foreground** process group  
      - `<`: **High priority** (negative nice value)  
      - `N`: **Low priority** (positive nice value)  
      - `L`: **Pages locked** into memory  
      - `s`: **Session leader** (e.g., shell)  
      - `l`: **Multi-threaded** process  
      - `E`: **Being debugged** (traced)

- **cron / crontab**
  - `cron`: a time-based job scheduler daemon that runs tasks automatically at specified times or intervals
  - `crontab` (cron table): the *config file* where recurring tasks are defined using a *5-field time format followed by the command*
  - Fields (in order): minute, hour, day of month, month, day of week
  - See command details and formatting in [linux cron section](linux_notes.md#crontab)
