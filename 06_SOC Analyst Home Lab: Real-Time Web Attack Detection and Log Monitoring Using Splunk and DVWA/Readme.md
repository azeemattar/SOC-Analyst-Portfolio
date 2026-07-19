# SOC Analyst Home Lab: Real-Time Web Attack Detection and Log Monitoring Using Splunk and DVWA

## Project Overview

This project simulates a small Security Operations Center (SOC) environment where web attacks are generated against a vulnerable web application and monitored using Splunk SIEM.

The objective of this lab is to understand how a SOC analyst collects security logs, investigates suspicious activity, and creates detection logic from security events.

The environment consists of:
- Kali Linux as the attacker machine
- Ubuntu Linux hosting Apache Web Server and DVWA
- Splunk Enterprise as the SIEM platform

Apache web server logs are continuously monitored by Splunk to provide real-time visibility into suspicious HTTP activity.

---

## Lab Architecture

```
                 Kali Linux
              (Attack Machine)
              192.168.56.101
                     |
                     |
        Nmap Scans / Web Attacks
                     |
                     ↓

              Ubuntu Server
              192.168.56.102

        Apache Web Server + DVWA
                     |
                     |
        /var/log/apache2/access.log
                     |
                     ↓

              Splunk Enterprise
                   SIEM

        Log Collection & Investigation
```

---

## Tools and Technologies Used

| Component | Technology |
|-----------|------------|
| Attacker Machine | Kali Linux |
| Target Machine | Ubuntu Linux |
| Vulnerable Application | DVWA |
| Web Server | Apache |
| SIEM Platform | Splunk Enterprise |
| Virtualization | Oracle VirtualBox |
| Log Source | Apache Access Logs |

---

## Project Objectives

- Build a simulated SOC environment
- Generate web attack activity in a controlled lab
- Collect Apache web server logs
- Perform real-time log monitoring using Splunk
- Analyze suspicious HTTP requests
- Create detection searches using Splunk SPL
- Understand SOC Level 1 investigation workflow

---

# Environment Setup

## DVWA Setup

Installed and configured DVWA on Ubuntu Linux.

Configuration performed:

- Installed Apache Web Server
- Installed PHP dependencies
- Configured MySQL database
- Enabled DVWA vulnerable modules
- Configured DVWA security settings for testing

DVWA URL:

```
http://192.168.56.102/DVWA
```

---

## Splunk Configuration

Configured Splunk Enterprise to continuously monitor Apache web server logs.

Monitored log file:

```
/var/log/apache2/access.log
```

Splunk Input Configuration:

```
Input Type:
File Monitor

Source Type:
access_combined

Host:
ubuntu

Index:
main
```

This configuration allows Splunk to automatically collect new Apache events in real time without manually uploading log files.

---

# Attack Simulation

## 1. Web Application Activity

Performed normal user activity:

- DVWA login
- Accessed vulnerability modules
- Browsed application pages

Example HTTP requests:

```
GET /DVWA/index.php

POST /DVWA/login.php
```

---

## 2. Command Injection Testing

Accessed DVWA Command Injection module.

Endpoint:

```
/DVWA/vulnerabilities/exec/
```

Observed Splunk event:

```
POST /DVWA/vulnerabilities/exec/
```

---

## 3. SQL Injection Testing

Accessed DVWA SQL Injection module.

Endpoint:

```
/DVWA/vulnerabilities/sqli/
```

Observed Splunk event:

```
GET /DVWA/vulnerabilities/sqli/
```

---

## 4. File Upload Testing

Tested DVWA file upload functionality.

Endpoint:

```
/DVWA/vulnerabilities/upload/
```

Observed Splunk event:

```
POST /DVWA/vulnerabilities/upload/
```

---

# Splunk Investigation Queries (SPL)

## Monitor DVWA Vulnerability Access

```spl
index=main sourcetype=access_combined
uri="/DVWA/vulnerabilities/*"
| stats count by clientip uri method
```

Purpose:

Identifies access to sensitive application modules.

---

## Detect POST Requests

```spl
index=main sourcetype=access_combined method=POST
| stats count by clientip uri
```

Purpose:

Finds HTTP POST activity that may require investigation.

---

## Analyze Web Activity by Source IP

```spl
index=main sourcetype=access_combined
| stats count by clientip
```

Purpose:

Identifies clients generating web traffic.

---

## View HTTP Status Codes

```spl
index=main sourcetype=access_combined
| stats count by status
```

Purpose:

Helps identify failed requests and possible attack activity.

---

# Sample Event Investigation

Example Splunk event:

```
Client IP:
192.168.56.101

Request:
POST /DVWA/vulnerabilities/exec/

Status:
200

Source:
/var/log/apache2/access.log
```

Investigation steps:

- Identified source IP
- Reviewed requested endpoint
- Analyzed HTTP method
- Classified activity based on context

---

# Skills Demonstrated

- Splunk SIEM configuration
- Real-time log monitoring
- Apache log analysis
- HTTP request investigation
- Web attack simulation
- Security event analysis
- SOC Level 1 investigation workflow
- SPL query creation

---

# Future Improvements

Planned enhancements:

- Create Splunk alerts for suspicious activity
- Detect brute-force login attempts
- Detect Nmap reconnaissance scans
- Build SOC dashboards
- Add Windows endpoint monitoring using Sysmon
- Configure Splunk Universal Forwarder architecture
- Perform incident response investigations

---

# Project Status
Completed:

✅ DVWA vulnerable application deployed  
✅ Kali attacker environment configured  
✅ Apache logging enabled  
✅ Splunk Enterprise configured  
✅ Real-time Apache log monitoring implemented  
✅ Security events successfully analyzed
