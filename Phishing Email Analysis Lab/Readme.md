# Phishing Email Analysis Lab

## Project Overview

This project demonstrates a SOC Level 1 phishing email investigation workflow.

A suspicious email sample was collected and analyzed in an isolated Ubuntu virtual machine environment. The investigation focused on identifying phishing indicators, extracting IOCs, and documenting findings in a SOC-style report.

---

## Objectives

- Analyze email headers
- Identify suspicious sender information
- Extract malicious URLs
- Identify social engineering techniques
- Document investigation findings

---

## Tools Used

- Ubuntu Linux
- grep
- file
- Linux command line tools

---

## Investigation Process

### 1. Email Header Analysis

Analyzed:

- Sender address
- Return-Path
- Received headers
- Source IP information
- Email subject

---

### 2. IOC Extraction

Extracted:

- Sender email address
- Suspicious URLs
- Source IP addresses

---

### 3. Content Analysis

Checked for:

- Suspicious keywords
- Social engineering techniques
- HTML-based email content

---

## Findings

### Email Details

Subject:

Life Insurance - Why Pay More?

Sender:

12a1mailbot1@web.de


### Suspicious Indicators

URL:

http://website.e365.cc/savequote/

Source IP:

210.97.77.167


Additional Mail Server:

203.122.2.197


### Observed Techniques

- Unsolicited financial offer
- HTML email content
- Call-to-action links
- Unknown sender identity

---

## Final Verdict

Classification:

Spam / Potential Phishing

Severity:

Medium


---

## Recommendations

- Block suspicious URL
- Monitor sender domain
- Add indicators to security monitoring tools
- Educate users about suspicious emails
