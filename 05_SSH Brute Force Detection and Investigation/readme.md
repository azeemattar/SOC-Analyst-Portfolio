# SSH Brute Force Detection and Investigation

## Overview

This project simulates an SSH brute-force attack against an Ubuntu Linux server from a Kali Linux attacker machine. The objective is to generate authentication events, analyze Linux authentication logs, identify Indicators of Compromise (IoCs), and document the investigation process from a SOC analyst's perspective.

---

## Objective

- Simulate an SSH brute-force attack using Hydra
- Monitor authentication logs in real time
- Identify failed and successful login attempts
- Extract attacker IP address
- Count authentication failures
- Practice Linux log analysis for SOC investigations

---

## Lab Architecture

```
                VirtualBox Host-Only Network
                     192.168.56.0/24

        Kali Linux (Attacker)
        192.168.56.101
              │
      SSH Brute Force (Hydra)
              │
              ▼
        Ubuntu Server (Victim)
        192.168.56.102
              │
        OpenSSH Service
              │
        /var/log/auth.log
```

---

## Lab Environment

| Component | Details |
|----------|---------|
| Hypervisor | Oracle VirtualBox |
| Attacker Machine | Kali Linux |
| Victim Machine | Ubuntu Server |
| Target Service | OpenSSH |
| Attack Tool | Hydra |
| Log Source | /var/log/auth.log |

---

## Tools Used

- Kali Linux
- Ubuntu Server
- Hydra
- OpenSSH
- grep
- tail
- wc
- VirtualBox

---

## Attack Scenario

The attacker attempts to gain unauthorized access to the Ubuntu server by repeatedly guessing the SSH password using Hydra.

This activity generates multiple failed authentication events that are recorded in the Linux authentication log.

---

## Attack Command

```bash
hydra -l vboxuser -P passwords.txt ssh://192.168.56.102
```

---

## Monitoring Authentication Logs

Real-time monitoring:

```bash
sudo tail -f /var/log/auth.log
```

---

## Investigation Commands

View failed login attempts

```bash
grep "Failed password" /var/log/auth.log
```

View attempts for a specific user

```bash
grep "Failed password for vboxuser" /var/log/auth.log
```

Find attacker IP address

```bash
grep "192.168.56" /var/log/auth.log
```

Count failed login attempts

```bash
grep "Failed password" /var/log/auth.log | wc -l
```

---

## Indicators of Compromise (IoCs)

- Multiple failed SSH login attempts
- Repeated authentication failures
- Single source IP generating numerous login attempts
- Brute-force activity against a valid user account
- High volume of SSH authentication requests within a short time

---

## Log Evidence

Example authentication log:

```
Failed password for vboxuser from 192.168.56.xxx port 50244 ssh2
```

This log entry indicates:

- Target user account
- Attacker IP address
- Source port
- Authentication protocol
- Failed login attempt

---

## MITRE ATT&CK Mapping

| Technique | ID |
|----------|------|
| Brute Force | T1110 |
| Valid Accounts | T1078 |

---

## Detection Opportunities

SOC analysts can detect this attack by monitoring:

- Excessive failed SSH logins
- Authentication anomalies
- Repeated login attempts from the same IP
- Login attempts outside normal working hours
- Sudden spikes in authentication failures

---

## Skills Demonstrated

- Linux Administration
- SSH Service Management
- Authentication Log Analysis
- Threat Hunting
- Incident Investigation
- IOC Identification
- Command Line Investigation
- Hydra Attack Simulation
- SOC Alert Investigation

---

## Screenshots

Include the following screenshots:

1. Home Lab Architecture
2. SSH service running
3. Successful SSH connection
4. Hydra brute-force attack
5. Live authentication logs
6. Failed password log entries
7. Attacker IP extraction
8. Failed login count
9. Investigation commands

---

## Key Learning Outcomes

- Understood how SSH brute-force attacks are performed
- Learned where Linux stores authentication logs
- Investigated failed login attempts using Linux commands
- Identified attacker IP addresses
- Practiced SOC investigation techniques
- Mapped attack activity to MITRE ATT&CK
- Improved Linux log analysis skills

---
# Designed By
Azeem Attar

## Disclaimer

This project was performed in an isolated home lab for educational and defensive cybersecurity purposes only. No attacks were conducted against systems without authorization.
