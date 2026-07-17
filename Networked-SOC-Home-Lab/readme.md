# Project 01 - Networked SOC Home Lab Setup (Attacker & Victim)

## Overview

This project documents the creation of a basic SOC home lab consisting of an attacker machine (Kali Linux) and a victim server (Ubuntu Server). The goal was to simulate a realistic network environment where security testing and log analysis can be performed safely.

Unlike a localhost DVWA setup, this lab separates the attacker and victim into different virtual machines connected through a private virtual network.

---

## Objectives

- Build a networked cybersecurity lab
- Configure communication between two virtual machines
- Perform reconnaissance using Nmap
- Host a vulnerable web application on Ubuntu
- Generate realistic web attack traffic for future SIEM analysis

---

## Lab Architecture

```
                   Windows Host
                         │
                  VirtualBox Host-Only Network
                         │
        ┌────────────────┴────────────────┐
        │                                 │
        ▼                                 ▼
 Kali Linux VM                     Ubuntu Server VM
 (Attacker)                        (Victim)
 192.168.56.x                      192.168.56.102
 ├── Nmap                          ├── Apache2
 ├── Hydra                         ├── OpenSSH
 ├── Nikto                         ├── MariaDB
 ├── Burp Suite                    └── DVWA
```

---

## Tools Used

- VirtualBox
- Kali Linux
- Ubuntu Server
- Apache2
- OpenSSH
- MariaDB
- DVWA
- Nmap

---

## Network Configuration

| Machine | Role | IP Address |
|----------|------|------------|
| Kali Linux | Attacker | 192.168.56.x |
| Ubuntu Server | Victim | 192.168.56.102 |

Network Mode:
- Adapter 1: NAT (Internet Access)
- Adapter 2: Host-Only Adapter (Lab Communication)

---

## Steps Performed

### 1. Configured VirtualBox Networking

- Created a Host-Only Network
- Connected both virtual machines
- Verified connectivity using ping

---

### 2. Enabled SSH

Installed and configured OpenSSH on Ubuntu.

Verified remote access from Kali using SSH.

---

### 3. Installed Apache Web Server

Installed Apache2 on Ubuntu.

Verified service status.

Confirmed the Apache default webpage could be accessed from Kali.

---

### 4. Installed DVWA

Configured:

- Apache
- PHP
- MariaDB
- DVWA

Successfully accessed:

http://192.168.56.102/DVWA

from the Kali attacker machine.

---

### 5. Reconnaissance

Performed service discovery using Nmap.

Command:

```bash
nmap -sV 192.168.56.102
```

Results:

- SSH (22)
- Apache HTTP (80)

This simulates the reconnaissance phase of an attack.

---

## Findings

The attacker successfully identified:

- Target operating system
- Running services
- Apache version
- SSH availability

This information could be used during later attack stages.

---

## Skills Demonstrated

- VirtualBox Networking
- Linux Administration
- SSH
- Apache Configuration
- Network Reconnaissance
- Nmap Enumeration
- Web Server Deployment
- Home Lab Design

---

## Screenshots

Include the following screenshots:

- Network Topology
- Successful Ping Between VMs
- SSH Connection from Kali
- Apache Default Page
- DVWA Login Page
- Nmap Scan Results
- Apache Service Status

---

## Lessons Learned

- Configured a realistic attacker-victim lab environment.
- Learned how private virtual networks work.
- Performed reconnaissance using Nmap.
- Verified remote web application access.
- Prepared the lab for future SOC investigations and SIEM integration.

---

## Future Improvements

- Install Splunk Enterprise
- Collect Apache access logs
- Detect web attacks
- Add SafeLine WAF
- Deploy Windows VM with Sysmon
- Integrate Wazuh
- Deploy Snort IDS

---

## MITRE ATT&CK Mapping

| Technique | ATT&CK ID |
|-----------|-----------|
| Active Scanning | T1595 |
| Network Service Discovery | T1046 |

---

## Author

**Azeem Attar**

SOC Analyst Home Lab Portfolio
