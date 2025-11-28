🛡️ SOC Analyst Web Attack Detection Project — SafeLine WAF + Python Web App

This project demonstrates my hands-on ability to deploy, configure, and analyze Web Application Firewall (WAF) detections using SafeLine WAF in a realistic SOC environment.
The objective of this lab is to simulate a full Blue Team workflow including WAF deployment, reverse proxy configuration, attack simulation, log analysis, and security event investigation.

🚀 Project Overview

This project replicates real-world SOC & Web Security Operations:

Deployed SafeLine WAF using Docker

Configured Reverse Proxy to inspect all inbound traffic

Hosted a static Python web application as the protected asset

Simulated real OWASP attacks:

XSS

SQL Injection

Path Traversal

Analyzed blocked & detected WAF events

Investigated malicious payloads

Mapped detections to MITRE ATT&CK techniques

Documented the final security findings

This lab aligns with MITRE ATT&CK techniques:

T1190 – Exploit Public-Facing Application

T1059 – Input-Based Script Execution (XSS payloads)

T1505 – Server Component Abuse

T1071 – Application Layer Protocol (HTTP)

T1040 – Traffic Inspection

🏗️ 1. Environment Setup (WAF + Backend App)
✔ Installed Docker Engine (SafeLine requirement)
✔ Deployed SafeLine WAF using official script
✔ Launched a Python static web app:
python3 -m http.server 8000

✔ Configured SafeLine as a Reverse Proxy

All inbound traffic → WAF → Backend App.

🔥 2. Web Attack Simulation (Adversarial Testing)

These controlled attacks were executed against the WAF-protected site.

✔ Attack 1 — Cross-Site Scripting (XSS)

Payload used:

http://localhost/?q=<script>alert(1)</script>

✔ Attack 2 — SQL Injection (SQLi)

Payload used:

http://localhost/?id=1' OR '1'='1

✔ Attack 3 — Path Traversal (LFI)

Payload used:

http://localhost/../../etc/passwd


SafeLine detected and blocked these malicious requests using built-in threat detection rules.

📊 3. WAF Detection & Event Analysis

Analyzed events under:

Events → Security Logs

SafeLine provided the following telemetry:

Malicious payload signatures

Blocked requests & categories

Source IP & HTTP request details

XSS detection events

SQLi pattern matches

LFI / Path Traversal alerts

Timestamps & WAF rule IDs

This allowed a full SOC-style investigation of the attack chain.

🧬 4. Extracted Indicators of Attack (IOAs)
🟥 XSS Payloads

<script>alert(1)</script>
"><img src=x onerror=alert(1)>

🟥 SQL Injection Payloads

' OR '1'='1
" OR 1=1 --

🟥 Traversal Payloads

../../etc/passwd
../..//windows/win.ini

These IOAs represent common web exploitation techniques aligned with OWASP Top 10.

⚙️ 5. Detection Engineering (WAF Rules & Config)

Configured SafeLine to operate as:

Reverse Proxy (HTTP Port 80)

Upstream server: 127.0.0.1:8000

Domain protection: *

Strict inspection mode enabled

The WAF automatically generated detections based on its ruleset:

XSS rule matches

SQL Injection rule matches

LFI / Directory Traversal rule matches

Suspicious request pattern matches

📸 6. Screenshots (Evidence)

Add your screenshots in this section:

WAF Dashboard

Application Configuration

XSS alert detection

SQLi alert detection

Path traversal alert

Request details page

Attack logs timeline

All stored under:

docs/screenshots/

📝 7. Incident Summary (What I Found)

The WAF successfully detected and blocked multiple malicious HTTP requests, including:

XSS attempts using script injection

SQL Injection patterns attempting to bypass logic

Path Traversal payloads aiming to access system files

SafeLine classified these attacks with high severity, preventing them from reaching the backend web server.
This concludes a complete end-to-end WAF security validation and attack detection workflow.

🧰 Skills Demonstrated

Web Application Firewall (WAF) Operation

Reverse Proxy Security Architecture

OWASP Attack Simulation

Web Traffic Analysis

Log Triage & Security Event Investigation

IOC Extraction & Threat Analysis

MITRE ATT&CK Mapping

Defensive Security Engineering

Python Simple Web Hosting

Documentation & Evidence Collection

👨‍💻 Author

Deepak Jadhav
