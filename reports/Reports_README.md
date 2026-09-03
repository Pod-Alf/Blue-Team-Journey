# Reports

Documentation of security labs and incident analysis throughout my Blue Team learning journey.

---

## 🧪 Technical Labs

| # | Lab Report | What's Inside | Tools |
|:-:|------------|---------------|-------|
| **01** | **[Network Reconnaissance](./01-nmap-reconnaissance.md)** | Port scanning and service enumeration from attacker's perspective on Rocky Linux victim server | `nmap` `ssh` |
| **02** | **[Wazuh SIEM Setup](./02-wazuh-setup.md)** | Complete Wazuh SIEM installation, configuration, and vulnerability assessment | `Wazuh 4.14` `Ubuntu 24 LTS` `VirtualBox` |
| **03** | [SSH Bruteforce Detection](./03-ssh-bruteforce-detection.md) | SSH brute force simulation and custom Wazuh detection rule (ID: 100002) | `Kali Linux` `Wazuh` `Custom XML Rules` |
| **04** | **[Windows Sysmon Setup](./04-windows-sysmon-setup.md)** | Sysmon deployment and configuration with Wazuh integration + MITRE ATT&CK T1087 analysis | `Sysmon` `SwiftOnSecurity Config` `Wazuh Agent` `PowerShell` |

---

## 🚨 Professional Incident Reports

SOC-style incident analysis with complete forensic timelines, IOCs, and MITRE ATT&CK mapping.

| Report ID | Title | Attack Type | Severity Level |
|:---------:|-------|-------------|:--------------:|
| **INC-001** | **[SSH Bruteforce Attack](./INC-001-SSH-Bruteforce.md)** | Credential Access via Brute Force (T1110.001) | 🟡 **HIGH** |
| **INC-002** | **[QakBot Malware & C2 Beacon](./INC-002-QakBot-SOCSimulator.md)** | Malware Infection + Command & Control (T1566, T1071) | 🔴 **CRITICAL** |
| **INC-003** | **[Ransomware Attack](./INC-003-Ransomware_Attack.md)** | Data Encryption for Impact (T1486, T1490) | 🔴 **CRITICAL** |

---

## 📋 What Each Type Contains

### Technical Labs Include:
- Objective and scope
- Tools and configurations used
- Step-by-step procedures
- Results and observations
- Lessons learned

### Incident Reports Include:
- **Incident Summary** — Metadata and affected systems
- **Timeline of Events** — Chronological reconstruction
- **Technical Analysis** — Attack chain breakdown
- **MITRE ATT&CK Mapping** — Tactics and techniques
- **IOCs** — Indicators of Compromise (IPs, hashes, file paths)
- **Lessons Learned** — Root cause analysis
- **Recommendations** — Remediation and prevention measures

---

**📊 Total Reports:** 7 | **🧪 Labs:** 4 | **🚨 Incidents:** 3

[← Back to Main Repository](../README.md)
