# Reports

Documentation of security labs and incident analysis throughout my Blue Team learning journey.

---

## 🧪 Technical Labs

| # | Lab Report | What's Inside | Tools |
|:-:|------------|---------------|-------|
| **01** | **[Network Reconnaissance](./01-nmap-reconnaissance.md)** | Port scanning and service enumeration from attacker's perspective on Rocky Linux victim server | `nmap` |
| **02** | **[Wazuh SIEM Setup](./02-wazuh-setup.md)** | Complete Wazuh SIEM installation, configuration, and vulnerability assessment | `Wazuh` `OpenVAS` |
| **03** | **[SSH Bruteforce Detection](./03-ssh-bruteforce-detection.md)** | Simulated SSH brute force attack with custom Wazuh detection rule creation | `Wazuh` `Hydra` |
| **04** | **[Windows Sysmon Setup](./04-windows-sysmon-setup.md)** | Sysmon deployment and configuration with MITRE ATT&CK Account Discovery detection | `Sysmon` `Windows Event Logs` |

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

**Technical Labs:**
- Objective and methodology
- Tool configuration and commands
- Execution steps with screenshots
- Results analysis
- Key takeaways

**Incident Reports:**
- Executive summary
- Complete timeline (timestamps + PIDs)
- MITRE ATT&CK tactics/techniques
- Full IOC list (IPs, hashes, file paths)
- Root cause analysis
- Remediation recommendations

---

**📊 Total Reports:** 7 | **🧪 Labs:** 4 | **🚨 Incidents:** 3

[← Back to Main Repository](../README.md)
