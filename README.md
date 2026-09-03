# Blue-Team-Journey
Repository to document my Journey from Helpdesk support/system support to Blue Team technician/DFIR

Hi, my name is **Alfonso**.

I've been working in **IT Support and System Administration for over 7 years** before starting this project. Throughout my career, I've always felt there was much more beyond the positions I held—especially when it came to understanding **what happens to a system after an attack**.

This repository documents my **transition into cybersecurity**, specifically focusing on:
- **Blue Team operations**
- **Digital Forensics & Incident Response (DFIR)**
- **Security Operations Center (SOC) analysis**

After several years on the IT ector, I decided to commit myself to cybersecurity, driven by curiosity about **incident investigation, threat detection, and response**.

---

## What can you find here?

This project is organized into four key areas:

### **The Beginning**

My initial setup: lab configuration, tools, versions, packages, and first conclusions.

### **Incident Reports**

Real-world style analysis of simulated attacks, including findings, IOCs, and response actions.

### **Tool Expansion**

Continuous learning with new security tools and technologies.

---

## Repository Index

### **Lab Setup & Configuration**

- [Design Decisions](./00-design-decisions.md) — Architecture, tools selection, and methodology

### **Technical Labs**

| Lab | Topic | Tool/Technology |
|-----|-------|-----------------|
| [01 - Network Reconnaissance](./reports/01-nmap-reconnaissance.md) | Port scanning and service enumeration | Nmap |
| [02 - SIEM Installation](./reports/02-wazuh-setup.md) | SIEM deployment and configuration | Wazuh |
| [03 - SSH Attack Detection](./reports/03-ssh-bruteforce-detection.md) | Custom detection rules for brute force | Wazuh |
| [04 - Windows Telemetry](./reports/04-windows-sysmon-setup.md) | Endpoint monitoring with MITRE ATT&CK | Sysmon |

### **Professional Incident Reports**

| ID | Incident Type | Report |
|----|---------------|--------|
| INC-001 | SSH Brute Force Attack | [View Report](./reports/INC-001-SSH-Bruteforce.md) |
| INC-002 | QakBot Malware & C2 Beacon | [View Report](./reports/INC-002-QakBot-SOCSimulator.md) |
| INC-003 | Ransomware Attack | [View Report](./reports/INC-003-Ransomware_Attack.md) |

---

## Technology Stack

Based on my professional experience and hands-on practice, I've worked with:

**Infrastructure & Systems:**
- AD
- Windows Server
- Linux Rhel
- Microsoft 365

**Security & Operations:**
- ServiceNow (Incident Management)
- Wazuh (SIEM)
- Sysmon (Endpoint Monitoring)
- Grafana (Monitoring & Visualization)

**Endpoint Management:**
-Intune
-Nexthink

---

## Certifications
| Certificate | Issuer | Date | Credentials |
| --- | --- | --- | --- |
| [Certified Cybersecurity Foundations (CORE)](https://hackviser.com/verify?id=HV-CORE-KNTWRQ8J) | Hackviser | August 2026 | Verify Online |

## Contact Info

- **LinkedIn:** [Alfonso Podadera López](https://www.linkedin.com/in/alfonso-podadera-lopez-0b41ab177)


- **Email:** [alfonsopodadera@gmail.com](mailto:alfonsopodadera@gmail.com)

---

## Project Status

🟢**Active project** — Updated regularly with new labs and incident analyses.

**Focus areas for 2026:**
- Advanced SIEM analysis and detection engineering
- Malware analysis and reverse engineering fundamentals
- Additional certifications

---

*Sometimes one must know how to defend before one can understand*
