# Command Injection Detection using DVWA and Apache Logs

## Project Summary

This project demonstrates how a command injection vulnerability in Damn Vulnerable Web Application (DVWA) can be exploited in a controlled lab environment and how the resulting activity can be investigated from a SOC Analyst perspective.

The lab involved executing operating system commands through a vulnerable web application by injecting additional commands into an input field. Apache access logs were monitored to observe the HTTP requests generated during the attack, identify indicators of compromise (IOCs), and understand how command injection attempts can be detected through web server log analysis.

This project focuses on defensive analysis rather than exploitation by documenting attacker behavior, analyzing log evidence, mapping the activity to the MITRE ATT&CK framework, and recommending detection and mitigation strategies relevant to Security Operations Center (SOC) analysts.

## Skills Demonstrated

- Linux Administration
- Apache Web Server Log Analysis
- Command Injection Fundamentals
- HTTP Request Analysis
- Indicator of Compromise (IOC) Identification
- MITRE ATT&CK Mapping
- Incident Investigation
- SOC Analyst Methodology
