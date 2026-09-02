# INC-003 - Ransomware Attack

## Incident Summary

| Field | Details |
| --- | --- |
| Incident ID | INC-003 |
| Date of Incident | Sept 2nd |
| Time of Incident | 09:20 AM |
| Date Detected | Sept 2nd |
| Time Detected | 09:35 AM |
| Severity | High |
| Status | Escalated |
| Analyst | Alfonso Podadera |
| Affected User | laura.jimenez |
| Affected System | WKST-CONT-014 |
| Attacker IP | 185.220.101.47:443 |
| Victim IP | 192.168.10.47 |

## Executive Summary

Attacker sent a mail using mail spoofing technique and phishing so the user (laura.jimenez) open a malicious word document directly from the received mail.
Once the document was open user accepted the use of macros. Those macros opened shell windows to start executing the attack and downloaded and executed a malicious file.
The malicious file created a service on the systems to further the attack, tried to read the domain and local accounts to further the attack or escalate privileges and disabled Windows Spyware.
Once this was done attacker encrypted the user files before login out to emite a C2 beacon signal.
Requires escalation to further investigation.
Incident High since it's somewhat contained and it has only affected one user from financial team.

## Timeline of Events

| Time | Event | Notes |
| --- | --- | --- |
| Sept 2nd 08:26:55 | Mail arrived to user's inbox | sender: facturacion@proveedor-es.net. Subject: Factura pendiente octubre. Attached file size: 48KB |
| Sept 2nd 08:27:03 | User opened file attached to mail and allowed Macros to execute manually after opening | Filename "Factura_Pendiente_octubre.docm", PID: 4412 |
| Sept 2nd 08:28:10 | Macros executed opened command line directly from Office 365 Word | Process cmd.exe PID: 5030 |
| Sept 2nd 08:28:51 | Macros executed called powershell with hidden window and encrypted use to download a file with bypass proxy | process powershell.exe PID: 6821, arguments: -NoProfile -WindowStyle Hidden -ExecutionPolicy Bypass -enc [base64], file downloaded: sv32.exe from http://185.220.101.47 |
| Sept 2nd 08:29:38 | Attacker executed vssadmin to delete all snapshot of files and backups | command executed: vssadmin delete shadows /all /quiet |
| Sept 2nd 08:29:55 | Attacker disabled anti Spyware on registry | command executed: reg.exe line written: HKLM\SOFTWARE\Policies\Microsoft\Windows Defender — DisableAntiSpyware=1 |
| Sept 2nd 08:30:02 | Attacker executed the creation of a new service to start automatically | command executed: sc create WinSvc32 binpath= "C:\Windows\Temp\svchost32.exe" start= auto. PID: 7204 |
| Sept 2nd 08:30:44 | Attacker used svchost32.exe process to access the system and tried to read the access token from the system | process tried to read lsass.exe PID: 756 |
| Sept 2nd 08:31:07 | Attacker changed all files under C:\Users\laura.jimenez\Documents extension. pattern behaviour similar to Ransomware attack | 347 files renamed to .docx.locked extension. Process svchost.exe |
| Sept 2nd 08:31:50 | Attacker left C2 beaconing and connection performed | |

## Technical Analysis

### Attack Description

 - Attacker sent file to user over mail from sender facturacion@proveedor-es.net

 - User opened the word file Factura_Pendiente_octubre.docm and manually accepted macros execution.

 - Macros execution opened cmd and powershell on silent mode, downloaded file, deleted backup.

 - Attacker disabled anti Spyware on Registry.

 - Attacker tried to read credentials from lsass to try and escalate privileges on perform lateral movement.

 - Attacker performed ransomware attack on all documents under C:\Users\laura.jimenez\Documents to encrypt them.

 - Attacker left C2 beacon channel opened.

### Evidence

- Attacker posed as a supplier and sent an attached file (Factura_Pendiente_octubre.docm) causing an urgency feeling on the user.

- File was a word document with macros to be executed. User opened the file from the mail directly and accepted manually the execution of macros, opening cmd, then powershell to bypass
proxy and therefore executing all the following process automatically without user's knowledged.
cmd.exe PID: 5030, powershell.exe -NoProfile -WindowStyle Hidden -ExecutionPolicy Bypass -enc [base64] PID: 6821

- powershell downloaded file sv32.exe from http://185.220.101.47/drop/sv32.exe Sha-256:f1e2d3c4b5a6978869504132deadbeef1234567890abcdef1234567890abcdef12 and changed the name to sc.exe 

- Attacker executed vssadmin.exe to delete all snapshots so it couldn't be possible to restore the files or the drive system. vssadmin delete shadows /all /quiet

- Attacker changed the Windows Defender Anti Spyware from the registry with reg.exe command HKLM\SOFTWARE\Policies\Microsoft\Windows Defender — DisableAntiSpyware=1. Event ID: 4657

- Attacker executed sc.exe to register a svchost.exe service and make it automatic. sc.exe sha256: f1e2d3c4b5a6978869504132deadbeef1234567890abcdef1234567890abcdef12,
command: sc create WinSvc32 binpath= "C:\Windows\Temp\svchost32.exe" start= auto

- Attacker tried to read access token to try and get elevated credentials or perform lateral movement reading lsass.exe. PID: 756

- Finally attacker performed an encryption on all files under users C:\Users\laura.jimenez\Documents to docx.locked, changing over 347files at a rate of 87 files per minute lasting 4 minutes.

- Attacker left open a C2 encryption channel with an outbound connection to their IP as a beacon.

### MITRE ATT&CK Mapping

| Tactic | Technique | ID |
| --- | --- | --- |
| Initial Access | | TA0001 |
| | Phishing | T1566 |
| | Spearphishing Attachment | T1566.001 |
| Execution | | TA0002 |
| | Command and Scripting Interpreter | T1059 |
| | Windows Command Shell | T1059.003 |
| | Powershell | T1059.001 |
| Stealth | | TA0005 |
| | Obfuscated Files or Information | T1027 |
| Command And Control | | TA0011 |
| | Ingress Tool Transfer | T1105 |
| | Encrypted Channel | T1573 |
| | Assymetric Cryptography | T1573.002 |
| | Application Layer Protocol | T1071 |
| | Web Protocls | T1071.001 |
| | Mail Protocols | T1071.003 |
| | Proxy | T1090 |
| | Multi-hop Proxy | T1090.003 |
| Persistence | | TA0003 |
| | Create or Modify System Process | T1543 |
| | Windows Service | T1543.003 |
| Credential Access | | TA0006 |
| | OS Credential Dumping | T1003 |
| | LSASS Memory | T1003.001 |
| Impact | | TA0040 |
| | Inhibit System Recovery | T1490 |
| | Data Encrypted for Impact | T1486 |
| Discovery | | TA0007 |
| | Account Discovery | T1087 |
| | Local Account | T1087.001 |
| | Domain Account | T1087.002 |
| Defense Impairments | | TA0112 |
| | Impair Defenses | T1562 |
| | Disable or Modify Tools | T1562.001 |

### Indicators of Compromise (IOCs)

| Type | Value | Notes |
| --- | --- | --- |
| Attacker IP |  185.220.101.47 | Port 443 |
| Attacker Mail | facturacion@proveedor-es.net | |
| Compromised user | laura.jimenez | |
| Affected IP | 192.168.10.47 | |
| Affected Hostname | WKST-CONT-014 | |
| Downloaded file | sv32.exe | later renamed to sc.exe |
| Hash | f1e2d3c4b5a6978869504132deadbeef1234567890abcdef1234567890abcdef12 | sv32.exe |
| | f1e2d3c4b5a6978869504132deadbeef1234567890abcdef1234567890abcdef12 | sc.exe |
| Attack Starter | Factura_Pendiente_octubre.docm | |
| Hash | b7e2d1a9f0c3e8b4d5f6a7c8e9d0b1a2c3f4e5d6a7b8c9d0e1f2a3b4c5d6e7f8 | 
| Encrypted files hash | a3f8c1d2e9b047ac5e6f8d0c3a1b2e9f4c7d8a0b1e2f3c4d5e6f7a8b9c0d1e2 |

### Lesson Learned

SOC team could not be able to act faster (Issue ocurred in the span of 4 minutes), but should have detected this issue faster, isolated the file and got the laptop isolated before further actions.
When a process has opened another one and it has not done so for 90 days (0 instances in 90 days) that should have raised our alarm and at least look further into it to prevent the action.

## Impact and Response

### Potential Impact

Loss of information, classified info, system compromised, leak of information, lateral movement, privilege escalation, defense evasion and info encryption, also possible issues if there are no backups of encrypted files in case they're needed for financial audits.
Incident resulted in ransomware attack, severity high, only one user and system affected and is somewhat contained, 

### Actions taken

Laptop isolated, firewall rules to block connections from 185.220.101.47 either inbound or outbound.
After thorough investigation we proceed to escalate this incident for further investigation and actions. 

### Recommendations

Isolate endpoint, re-image laptop, change SIEM Rules to show CRITICAL on the execution of a process when no execution was started after 90 days and another one starts suddenly, block macros
from all files downloaded, block registry so it can't be changed from non-admin accounts, block encryption executions of powershell
check for online backups of user's system to recover encrypted affected files.
