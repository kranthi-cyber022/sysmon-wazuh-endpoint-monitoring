# Incident Report: Simulated PowerShell LotL Activity

## Executive Summary
A simulated Living-off-the-Land (LotL) attack was executed on a monitored Windows 10 endpoint. Sysmon and Wazuh successfully captured the full attack chain, including process creation, DNS resolution, and network connection. All events were correlated by Process ID 5052 and mapped to MITRE ATT&CK.

## Timeline of Events

| Time (UTC) | Event ID | Description | MITRE ATT&CK |
|------------|----------|-------------|--------------|
| 11:03:44 | 1 | PowerShell executed with `-ExecutionPolicy Bypass -NoProfile` | T1059.001 |
| 11:07:39 | 22 | DNS query for `raw.githubusercontent.com` | T1071.004 |
| 11:09:35 | 3 | Outbound connection to `8.8.8.8:53` | T1071 |

## Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| Process | `powershell.exe` (PID 5052) |
| Domain | `raw.githubusercontent.com` |
| IP Address | `8.8.8.8` |
| Port | `53` |
| Command Line | `powershell.exe -ExecutionPolicy Bypass -NoProfile` |
| File Hash (SHA256) | `64DD5E1C2373DEDE25C2776F553C632E58C45E56A0E4639DFD54E97E9AB9C19` |

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|--------|-----------|-----|
| Execution | PowerShell | T1059.001 |
| Command and Control | Application Layer Protocol | T1071 |
| Command and Control | DNS | T1071.004 |

## Analysis
The attacker used PowerShell with execution policy bypass to evade detection. Sysmon Event ID 1 captured the full command line and parent process. Subsequent DNS and network events were correlated by Process ID 5052, confirming the same process instance performed all three actions.

## Recommendations
1. Enable PowerShell Script Block Logging (Event ID 4104)
2. Create custom Wazuh rules for encoded PowerShell commands
3. Expand Sysmon config to capture Event IDs 11, 12, 13, 14
4. Implement NTP synchronization for accurate event correlation
