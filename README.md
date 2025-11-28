SafeLine WAF Deployment, Configuration & Web Attack Detection Lab

This repository documents a complete, production-style deployment and evaluation of the SafeLine Web Application Firewall (WAF) on Kali Linux.
The objective of this lab is to demonstrate the ability to deploy security controls, configure reverse-proxy protections, and detect/triage real web-based attacks—skills essential for SOC Analysts, Incident Responders, and Blue-Team engineers.

The project includes WAF setup, backend application hosting, controlled adversarial testing (XSS, SQLi, Path Traversal), event analysis, and security logging walkthroughs.

📌 Project Objectives

This lab was created to simulate a real-world SOC workflow:

Deploy and operationalize a WAF in a Linux environment

Configure reverse-proxy traffic inspection

Host a vulnerable static web application to generate attack telemetry

Execute controlled attacks representing common OWASP Top 10 vectors

Observe, analyze, and document WAF detections and block events

Build repeatable steps for students and analysts learning defensive security

🏗️ Architecture Overview

The following high-level architecture represents the traffic flow in this environment:

Attacker → SafeLine WAF (Reverse Proxy) → Backend Web Server (Python)  


A detailed diagram is provided in:

docs/architecture.png


The WAF sits in front of the application, intercepting and inspecting all inbound traffic, applying rule-based detection to identify and block malicious payloads.

📂 Repository Structure
safeline-waf-lab/
│
├── docs/
│   ├── architecture.png               # Network & traffic flow diagram
│   ├── screenshots/                   # Evidence of attacks, logs, UI
│   │   ├── waf-dashboard.png
│   │   ├── attack-logs.png
│   │   └── test-app.png
│   └── notes.md                       # Optional research notes
│
├── testweb/
│   └── index.html                     # Static demo web application
│
└── README.md                          # Project documentation

🛠️ Platform & Tools
Component	Description
OS	Kali Linux
WAF	SafeLine (Docker-based deployment)
Backend	Python http.server (static site)
Traffic Mode	Reverse Proxy
Attack Types Tested	XSS, SQLi, Path Traversal
🚀 Deployment & Configuration Procedure
1. Install Docker Engine

SafeLine runs via Docker containers, so Docker is required:

sudo apt update
sudo apt install docker.io docker-compose-plugin -y
sudo systemctl enable --now docker

2. Install SafeLine WAF (Official Script)
sudo bash -c "$(curl -fsSLk https://waf.chaitin.com/release/latest/install.sh)"


Upon completion, SafeLine provides administrative credentials:

URL      : https://127.0.0.1:9443/
Username : admin
Password : ********


Login using the provided URL.

3. Deploy the Backend Web Application

Hosted on a lightweight Python HTTP server:

mkdir ~/testweb
cd ~/testweb
python3 -m http.server 8000


The application contains a simple form to test injection payloads.

Accessible via:

http://127.0.0.1:8000

4. Configure the WAF as a Reverse Proxy

Inside the SafeLine Web UI:

Applications → Add Application

Field	Value
Domain	*
Listening Port	80
Mode	Reverse Proxy
Upstream Protocol	HTTP
Upstream Host	127.0.0.1
Upstream Port	8000

This configuration forces all inbound HTTP traffic to pass through the WAF for inspection.

⚔️ Adversarial Testing (Attack Simulation)

This lab includes safe, controlled tests representing common web attack vectors.

1. Cross-Site Scripting (XSS)
http://localhost/?q=<script>alert(1)</script>

2. SQL Injection (SQLi)
http://localhost/?id=1' OR '1'='1

3. Path Traversal
http://localhost/../../etc/passwd


Each attack is intentionally crafted to trigger the WAF’s detection engine.

📊 Security Event Analysis

All alerts and blocked attack attempts are visible in:

SafeLine Dashboard → Events → Security

Captured information includes:

Attack category (XSS, SQLi, LFI, traversal, etc.)

Detection rule triggered

Source IP

Payload

Risk classification

Timestamp

HTTP request context

Screenshots of blocked events are stored in:

docs/screenshots/

🧠 Key Learning Outcomes

This hands-on project covers essential SOC skills:

✔ WAF Deployment & Administration

Understanding real defensive perimeter technology.

✔ Reverse Proxy Traffic Inspection

Ensuring all inbound traffic flows through security controls.

✔ Web Attack Simulation

Executing controlled adversarial behaviour for logging and analysis.

✔ Log Analysis & Incident Triage

Reading WAF telemetry and identifying malicious patterns.

✔ Documentation & Reporting

Collecting screenshots, building diagrams, and publishing a structured defensive security lab.

📦 Use Cases

This project is ideal for:

SOC Analyst Training

Blue Team Portfolio Building

Web Security Demonstration

SIEM/WAF Integration Experiments

Cybersecurity Academic Projects

🏁 Conclusion

This lab provides an end-to-end demonstration of deploying, securing, and analyzing a web application using SafeLine WAF. Through realistic attack scenarios and detailed log analysis, the project showcases technical competence in Web Security, Blue Teaming, and SOC Operations.

It serves as a professional-grade defensive security project suitable for resumes, cybersecurity portfolios, and
