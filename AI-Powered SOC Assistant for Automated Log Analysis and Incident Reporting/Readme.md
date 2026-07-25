# AI-Powered SOC Assistant for Automated Log Analysis and Incident Reporting
## Overview

AI SOC Assistant is a Python-based cybersecurity project that automates the analysis of Apache web server logs using a locally hosted Large Language Model (LLM).

The project continuously monitors Apache access logs, detects common web attacks, sends suspicious events to a local AI model (Gemma running with Ollama), and automatically generates incident reports with attack details, severity, MITRE ATT&CK mapping, and remediation recommendations.

The entire solution runs locally without relying on cloud AI services.

---

# Features

- Real-time Apache log monitoring
- Automatic log parsing
- Detection of common web attacks
- Local AI-powered security analysis using Ollama
- Automatic Markdown incident report generation
- Works completely offline
- Lightweight home lab implementation

---

# Attack Detection

The project currently detects:

- Nmap Scan
- Command Injection
- SQL Injection
- File Upload Attempts
- Login Attempts
- Normal Web Traffic

---

# Technologies Used

## Programming

- Python 3

## Operating Systems

- Ubuntu Server
- Kali Linux

## Web Server

- Apache2

## AI

- Ollama
- Gemma 3 1B (Local LLM)

## Security Lab

- DVWA (Damn Vulnerable Web Application)

---

# Project Architecture

```
                    Kali Linux
                  (Attack Machine)
                         │
                         │
                         ▼
                 Apache Web Server
                  Ubuntu Machine
                         │
                         ▼
                 Apache Access Logs
                         │
                         ▼
                  Log Reader (Python)
                         │
                         ▼
                 Attack Detection Engine
                         │
                         ▼
             Local AI (Gemma via Ollama)
                         │
                         ▼
              Incident Report Generator
                         │
                         ▼
              Markdown Security Report
```

---

# Project Workflow

1. Attacker generates traffic from Kali Linux.
2. Apache stores requests in access.log.
3. Python monitors the latest log entry.
4. Event details are extracted.
5. Attack type is identified.
6. Suspicious events are sent to the local LLM.
7. AI analyzes the event.
8. Incident report is automatically generated.

---

# Folder Structure

```
AI-SOC-Assistant/

│── src/
│     ├── monitor.py
│     ├── log_reader.py
│     ├── ai_analyzer.py
│     └── report_generator.py
│
│── logs/
│     └── access.log
│
│── reports/
│     └── report.md
│
│── screenshots/
│
│── README.md
│
└── requirements.txt
```

---

# Example AI Output

```
Attack: Command Injection

Severity: Critical

MITRE ATT&CK:
T1059 - Command and Scripting Interpreter

Recommendation:
Investigate the source IP immediately, validate user inputs,
block malicious requests, and review server logs for additional
suspicious activity.
```

---

# Example Generated Report

The project automatically creates reports similar to:

```
# Security Incident Report

Source IP:
192.168.56.101

Method:
POST

URL:
/DVWA/vulnerabilities/exec/

Attack:
Command Injection

Severity:
Critical

MITRE ATT&CK:
T1059

Recommendation:
Investigate the source IP and review server activity.
```

---

# Skills Demonstrated

- Linux Administration
- Python Programming
- Log Parsing
- Regular Expressions
- Apache Web Server
- Security Log Analysis
- Threat Detection
- Incident Response
- AI Integration
- Local LLM Deployment
- Home Lab Development

---

# Home Lab

The project was built inside a virtualized cybersecurity lab.

**Attacker Machine**

- Kali Linux

**Target Machine**

- Ubuntu Server
- Apache2
- DVWA

**AI Engine**

- Ollama
- Gemma 3 1B

---

# Future Improvements

- Threat Intelligence Integration (VirusTotal / AbuseIPDB)
- Splunk Integration
- Wazuh Integration
- Email Alerting
- Dashboard for Incident Monitoring
- IOC Extraction
- Multiple Log Source Support

---

# Screenshots

Include screenshots of:

- Project Folder Structure
- Home Lab Architecture
- Apache Running
- Nmap Scan
- Command Injection
- Real-time Monitoring
- AI Analysis
- Generated Incident Report

---

# Learning Outcomes

This project demonstrates how AI can assist SOC analysts by automating the initial analysis of web server logs and generating structured incident reports. It combines traditional log analysis with local LLM inference to simulate a simplified SOC workflow suitable for learning and portfolio demonstration.

---

# Author

Azeem Attar

Cybersecurity Enthusiast | SOC Analyst Aspirant
