# Cybersecurity notes & resources
## 📚 Table of Contents

- [Cybersecurity notes \& resources](#cybersecurity-notes--resources)
  - [📚 Table of Contents](#-table-of-contents)
- [Websites](#websites)
  - [Search Engines \& DBs](#search-engines--dbs)
  - [Documentation](#documentation)
  - [Others](#others)
- [Tools \& Packages](#tools--packages)
- [Terms](#terms)
  - [Industry Terms and Systems](#industry-terms-and-systems)
  - [Adversarial Techniques](#adversarial-techniques)
  - [Security Assessment Methods](#security-assessment-methods)

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
    - allows users to scan files via url, ip, domain, upload, or file hash

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
    - 

# Tools & Packages

- gobuster: https://github.com/OJ/gobuster
    - *tool for bruteforcing websites Directory/File, DNS and VHost written in Go*
    - e.g.          gobuster dns -d google.com -w ~/wordlists/subdomains.txt -i
    - e.g.          gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt

# Terms

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

- **Static Analysis**: inspecting the malware without running it
- **Dynamic Analysis**: runs the malware in a controlled environment and monitors its activities