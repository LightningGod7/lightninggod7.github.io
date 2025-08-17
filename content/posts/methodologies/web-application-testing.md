+++
title = "Web Application Testing Methodology"
date = "2023-08-17"
author = "Zeus"
cover = ""
tags = ["web", "methodology", "penetration-testing"]
description = "A comprehensive methodology for testing web applications during penetration tests."
showFullContent = false
+++

# Web Application Testing Methodology

This post outlines my methodology for testing web applications during penetration tests. Following a structured approach ensures thorough coverage and minimizes the chance of missing critical vulnerabilities.

## 1. Reconnaissance

### Information Gathering
- Identify the target scope (domains, subdomains, IP ranges)
- Gather publicly available information (WHOIS, DNS records)
- Identify technologies used (web server, frameworks, CMS)
- Check for exposed source code repositories

### Subdomain Enumeration
```bash
# Subfinder
subfinder -d example.com -o subdomains.txt

# Amass
amass enum -d example.com -o amass_results.txt

# Certificate Transparency
curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value' | sort -u
```

## 2. Scanning and Enumeration

### Port Scanning
```bash
# Quick scan
nmap -sV -sC -p 80,443,8080,8443 example.com

# Full port scan
nmap -p- --min-rate 5000 -T4 example.com
```

### Directory Enumeration
```bash
# Gobuster
gobuster dir -u https://example.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50

# Ffuf
ffuf -u https://example.com/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -c
```

### Technology Identification
- Use Wappalyzer browser extension
- Check HTTP headers and cookies
- Inspect source code for framework signatures
- Use whatweb or builtwith

## 3. Vulnerability Assessment

### Common Web Vulnerabilities to Check
1. Injection Flaws
   - SQL Injection
   - Command Injection
   - LDAP Injection
   - XPath Injection

2. Broken Authentication
   - Weak password policies
   - Session management issues
   - Account lockout bypass

3. Sensitive Data Exposure
   - Cleartext transmission
   - Weak encryption
   - Sensitive information in source code

4. XML External Entities (XXE)
   - File disclosure via XXE
   - Server-Side Request Forgery via XXE

5. Broken Access Control
   - Horizontal privilege escalation
   - Vertical privilege escalation
   - IDOR vulnerabilities

6. Security Misconfigurations
   - Default credentials
   - Error messages revealing too much
   - Unnecessary services enabled

7. Cross-Site Scripting (XSS)
   - Reflected XSS
   - Stored XSS
   - DOM-based XSS

8. Insecure Deserialization
   - Java deserialization
   - PHP deserialization
   - .NET deserialization

9. Using Components with Known Vulnerabilities
   - Outdated libraries
   - Unpatched systems

10. Insufficient Logging & Monitoring
    - Missing audit logs
    - Ineffective monitoring

## 4. Exploitation

### Manual Testing
- Use Burp Suite for intercepting and modifying requests
- Test for parameter tampering
- Attempt authentication bypass
- Check for business logic flaws

### Automated Testing
```bash
# OWASP ZAP
zap-cli quick-scan --self-contained --start-options '-config api.disablekey=true' https://example.com

# Nikto
nikto -h https://example.com
```

## 5. Post-Exploitation

### Privilege Escalation
- Attempt to elevate privileges within the application
- Look for ways to access admin functionality
- Extract sensitive data from the application

### Lateral Movement
- Use compromised credentials on other services
- Pivot to internal networks if possible
- Attempt to compromise other users

## 6. Documentation

### Evidence Collection
- Take screenshots of vulnerabilities
- Save HTTP requests/responses
- Document exploitation steps

### Reporting
- Clearly describe vulnerabilities
- Include steps to reproduce
- Provide remediation recommendations
- Assign severity ratings

## Conclusion

Web application testing requires a methodical approach to ensure comprehensive coverage. This methodology provides a framework, but always adapt it to the specific application you're testing. Remember that the goal is to identify security issues that could impact the organization, not just to find as many vulnerabilities as possible.

---

*Disclaimer: Only perform testing on systems you have explicit permission to test.*
