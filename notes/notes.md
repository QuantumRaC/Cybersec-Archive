# Cybersecurity notes & resources
## 📚 Table of Contents

- [Websites](#websites)
  - [Search Engines & DBs](#search-engines--dbs)
  - [Documentation](#documentation)
  - [Others](#others)

- [Tools & Packages](#tools--packages)
  - [Gobuster](#gobuster)

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
    - e.g.      gobuster dns -d google.com -w ~/wordlists/subdomains.txt -i
    - e.g.      gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt

# Terms
