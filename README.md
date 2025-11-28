SafeLine WAF Deployment & Web Attack Detection Lab

This project demonstrates the deployment and configuration of SafeLine Web Application Firewall (WAF) on Kali Linux, along with a simple static web application used to simulate and analyze common web attacks such as XSS, SQL Injection, and Path Traversal.
It is designed as a practical SOC Analyst / Blue Team lab project.

🔧 Environment Setup

OS: Kali Linux

WAF: SafeLine by Chaitin

Backend Web App: Python http.server

Mode: Reverse Proxy

Purpose: Observe WAF blocking & logging behaviors during simulated attacks

📁 Project Structure
safeline-waf-lab/
│
├── docs/
│   ├── architecture.png
│   ├── screenshots/
│   │   ├── <your-screenshots>.png
│   └── notes.md
│
├── testweb/
│   └── index.html
│
└── README.md

🚀 1. Install Docker
sudo apt update
sudo apt install docker.io docker-compose-plugin -y
sudo systemctl enable --now docker

🚀 2. Install SafeLine WAF
sudo bash -c "$(curl -fsSLk https://waf.chaitin.com/release/latest/install.sh)"


After installation, SafeLine provides:

URL: https://127.0.0.1:9443/
Username: admin
Password: ********


Log in to the dashboard.

🌐 3. Create the Demo Web Application
mkdir ~/testweb
cd ~/testweb
python3 -m http.server 8000


The static HTML file (index.html) contains a simple search form used to test injection payloads.

Your app runs at:

http://127.0.0.1:8000

🔄 4. Configure SafeLine Reverse Proxy

Inside SafeLine UI:

Applications → Add Application

Setting	Value
Domain	*
Listening Port	80
Mode	Reverse Proxy
Upstream Protocol	HTTP
Upstream Host	127.0.0.1
Upstream Port	8000

Traffic Flow:
Client → SafeLine WAF → Test Web App

⚔️ 5. Simulate Web Attacks

Test the WAF by sending common attack payloads.

🔹 XSS
http://localhost/?q=<script>alert(1)</script>

🔹 SQL Injection
http://localhost/?id=1' OR '1'='1

🔹 Path Traversal
http://localhost/../../etc/passwd


SafeLine will detect and block these malicious requests.

📊 6. View WAF Logs

In SafeLine dashboard:

Navigate to Events → Security

Review:

Attack type

Payload

Timestamp

Source IP

Risk level

Screenshots are included in docs/screenshots/.

🖼️ Architecture Diagram

Located at:

docs/architecture.png


This diagram visualizes the WAF, reverse proxy, backend server, and attack flow.

📝 Summary

This lab demonstrates:

✔ Deployment of SafeLine WAF on Kali Linux

✔ Reverse proxy configuration

✔ Static web app setup using Python

✔ Real attack simulations (XSS, SQLi, Path Traversal)

✔ WAF detection & log analysis

✔ Practical SOC/Blue Team workflow

This project is ideal to showcase WAF understanding, attack analysis, and defensive security skills in your portfolio or CV.


