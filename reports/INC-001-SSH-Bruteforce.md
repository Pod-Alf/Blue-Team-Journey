# INC-001 - SSH Bruteforce Attack

## Incident Summary

| Field | Details |
| --- | --- |
| Incident ID | INC-001 |
| Date Detected | August 3rd 2026 |
| Time Detected | 10:12:47 AM |
| Severity | High |
| Status | Contained |
| Analyst | Alfonso Podadera |
| Affected System | Production Server Rocky Linux |
| Attacker IP | 172.16.0.14 |
| Victim IP | 172.16.0.2 |

## Executive Summary

The attacker tried and succeeded to access to the production server by executing a bruteforce attack on it (trying
random credentials to check if one works). The attacker gained access to the admin account (user a) that has sudo
privileges.

To contain this incident after the incident was raised and escalated a new firewall rule was created to reject
connections from the attacker IP.

Also we've contacted systems team and security engineer to check on the server, change password and username for the
compromised user to follow security policies about complexity and to further check the extent of the attack
consequences.

## Timeline of Events

| Time | Event | Notes |
| --- | --- | --- |
| Aug 3rd 10:03:47 | SSH Connection successful from IP 172.16.0.14 | Part of the attack, the IP address was unkown to us before, but is the same address as the unsuccessful connections |
| Aug 3rd 10:11:05 | SSH Session connection closed | |
| Aug 3rd 10:11:27 | Unsuccessful connection from same IP address | |
| Aug 3rd 10:11:41 to 10:12:45 | Constant unsuccessful connections from same IP address | |
| Aug 3rd 10:12:47 | Bruteforce attack identified by SIEM | |
| Aug 3rd 10:13 | Analyst raises and escalates incident | |
| Aug 3rd 10:15 | Analyst tries to contain further connection from Attacker IP | |
| Aug 4th (post-incident discovery | Port scan activity identified on victim prior to bruteforce attack | Issue discovered during INC-001 investigation. Failed to detect it in real time due to lack of SIEM monitorization. |

## Technical Analysis

### Attack Description

- The attacker performed a first successful connection (10:03:47) as a test, but he accessed the root account (username a)

- The attacker performed several tries to connect to non-existent users for 90 seconds (10:11:27 to 10:12:45)

- Wazuh detected the brute force pattern.

### Evidence

Wazuh rules triggered:

- 5715: Authentication success 

- 5501: Login session opened

- 5502: Login session closed

- 5710: Tried to login to a non-existing user

- 5503: Login failed

- 2502: System - User missed password multiple times

- 5557: Password failed

- 5760: Authentication failed

- 5712: Brute force attack detected

### MITRE ATT&CK Mapping

| Tactic | Technique | ID |
| --- | --- | --- |
| Credential Access | Brute Force - Password Guessing | T1110.001 |
 
### Indicators of Compromise (IOCs)

| Type | Value | Notes |
| --- | --- | --- |
| Attacker IP | 172.16.0.14 | |
| Targeted port | 22/TCP | |
| Protocol Used | SSH | |
| Compromised user | a | |
| Wazuh rule triggered | 5712 | Created custom rule 100002 in consequence to verify this attack easier |

### Lesson Learned

The installation of SIEM is almost as important as the network itself and has to be prepared prior to get a server working so everything can be checked and monitorized.

## Impact and Response

### Potential Impact

Loss of information, classified info, possibility of monetary loss in case production server were to be stopped or
the root user were used to tamper with processes.

### Actions taken

- Added firewall rule to block traffict from IP 172.16.0.14

- Escalated the incident to L2.

### Recommendations

Recomendation to systems team to change username and password for user a, recommended change of ssh port and
check processes started and working (in case attacker has created any form of backdoor).

Recommendations to Network team to check the vlan the production server is connected and if it's visible from the
outside.
