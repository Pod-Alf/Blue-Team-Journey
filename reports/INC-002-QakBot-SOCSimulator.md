# INC-002 - QakBot

## Incident Summary

| Field | Details |
| --- | --- |
| Incident ID | INC-002 |
| Date Detected | August 27th 2026 |
| Time Detected | 11:30 AM |
| Severity | High |
| Status | Escalated |
| Analyst | Alfonso Podadera |
| Affected System | HALDREN\dorian.haskell |
| Attacker IP | 185.177.34.91:443 |
| Victim IP | 10.137.30.42 |

## Executive Summary

Attacker sent a mail using mail spoofing technique and phishing so the user (dorian.haskell) downloaded and executed a malicious file.
Once executed a bot started working, locating itself on E:\ as "qbot.cmd" silently with /c option on cmd.
Once this was executed the bot executed regsvr32.exe in silent (/s) to change and delete the temp files for the installation.
Now with the bot all setup it constantly began to emit a C2 beacon signal to the list it had until it received a response.
Later during the day a connection was stablished to download info.
Requires escalation to further investigation.

## Timeline of Events

| Time | Event | Notes |
| --- | --- | --- |
| April 23 2026 08:34 | User received mail from invoices@sapplus.net about 'outstanding invoince' | Password was on the body of the message. Filename: Orig1510220021.zip |
| April 23 2026 09:01 | User downloads the file 'Orig1510220021.zip' | |
| April 23 2026 09:04:00 | User de-compress the file 'Orig1510220021.zip' and creates file 'Orig1510220021.iso' in user's Download | |
| April 23 2026 09:04:40 | Process explorer.exe mounted 'Orig1510220021.iso' as removable drive E:| Process executed itself without user knowledged | |
| April 23 2026 09:05 | System executed 'cmd.exe /c E:\qbot.cmd without user knowledge | The /c argument caused the execution to open and close the window so user couldn't be aware |
| April 23 2026 09:06 | System executed regsvr32.exe /s C:\Users\dorian.haskell\AppData\Local\Temp\tdfasdf.dat to delete and modify the temporary installation files | The /s argument makes it so the execution of regsvr32.exe is silent |
| April 23 2026 09:06:20 | System executed regsvr32.exe to register tdfasdf.dat as a DLL |
| April 23 2026 09:07 | regsvr32.exe tries to make outbound connection with embedded C2 list. Many refused |
| April 23 2026 09:08 | C2 connection stablished successfully with IP 185.177.34.91 |
| April 23 2026 11:48 | Attacker extracted (~2.86 MB) of data from host using encrypted C2 connection. Beacon kept working | Unknown data extracted |

## Technical Analysis

### Attack Description

 - The attacker sent a mail to the user dorian.haskell of a supposed invoice.

 - Once the user decompressed the file the bot began to work.

 - Bot executed silently in front of user and hid the installation files.

 - Bot used C2 beacon to inform attacker.

 - Attacker connected later using C2 Encryption channel and downloaded information from host.


### Evidence

- A purchasing coordinator followed a phishing link and downloaded a password-protected archive (Orig1510220021.zip) from sapplus.net; the password was supplied in the message body to defeat gateway scanning.

- A decoy shortcut (Document.lnk) on the mounted ISO drive E: launched cmd.exe, a hallmark of ISO-delivered loader execution via user interaction.
cmd.exe, PID: 5984, cmd.exe /c E:\qbot.cmd

- cmd.exe executed a batch script (qbot.cmd) staged on the removable ISO drive, chaining user execution into a scripted loader

- cmd.exe invoked the signed system utility regsvr32.exe to register and execute a DLL written to the user Temp directory with a misleading .dat extension (tdfasdf.dat), proxying execution through a trusted binary.

- regsvr32.exe opened outbound TLS sessions on 443, cycling a list of candidate command-and-control endpoints that refused the connection before settling on 185.177.34.91 as its primary beacon.

- The command-and-control channel was wrapped in TLS presenting a throwaway certificate subject CN (sxeuiqecowj.net), an encrypted channel that defeated outbound content inspection.

- Host survey data (~2.86 MB) was exfiltrated over the existing encrypted C2 channel to 185.177.34.91:443, riding the beacon rather than a separate drop host. 

### MITRE ATT&CK Mapping

| Tactic | Technique | ID |
| --- | --- | --- |
| Initial Access |  | TA0001 |
| | Phishing | T1566 |
| | Spearphishing Attachment | T1566.001 |
| Execution | | TA0002 |
| | User Execution | T1204 |
| | Malicious File | T1204.002 |
| | Command and Scripting Interpreter | T1059 |
| | Windows Command Shell | T1059.003 |
| Stealth | | TA0005 |
| | System Binary Proxy Execution | T1218 |
| | Regsvr32 | T1218.010 |
| Command and Control | | TA0011 |
| | Application Layer Protocol | T1071 |
| | Web Protocol | T1071.001 |
| | Encrypted Channel | T1573 |
| | Asymmetric Cryptography | T1573.002 |
| Exfiltration | | TA0010 |
| | Exfiltration over C2 Channel | T1041 |

### Indicators of Compromise (IOCs)

| Type | Value | Notes |
| --- | --- | --- |
| Attacker IP |  185.177.34.91 | |
| Attacker Mail | invoices@sapplus.net | |
| Ports affected | 50335, 50361, 50612 | Ports were opened |
| Protocol Used | TCP | |
| Compromised user | dorian.haskell | |
| Affected IP | 10.137.30.42 | |

### Lesson Learned

SOC team should have detected the Regsvr32.exe and raise an alarm before the connection was established so the user's laptop could have been isolated and no info were taken

## Impact and Response

### Potential Impact

Loss of information, classified info, reputation loss for the company, system compromised, leak of information, lateral movement, privilege escalation, defense evasion and info extraction.

### Actions taken

After thorough investigation we proceed to escalate this incident for further investigation and actions.

### Recommendations

Isolate endpoint, re-image laptop, block any execution of /c on CMD or /s on regsvr32.exe, enroll user in phishing prevention courses, block attacker known IPs.
