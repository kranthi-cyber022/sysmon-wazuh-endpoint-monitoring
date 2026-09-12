# Basic Endpoint Security Monitoring Using Sysmon & Wazuh

## Project Overview
Deployed a Windows 10 endpoint with Sysmon and a Wazuh agent, forwarding telemetry to a Wazuh Manager on Ubuntu Server. Successfully detected and investigated simulated Living-off-the-Land (LotL) activity using PowerShell.

## Objective
To bridge the Windows default logging visibility gap and build a SOC-ready detection pipeline that maps endpoint telemetry to the MITRE ATT&CK framework.

## Architecture
- **Endpoint:** Windows 10 Enterprise (VMware)
- **Monitoring Server:** Ubuntu Server (Wazuh Manager + Indexer + Dashboard)
- **Tools:** Sysmon v15.21, SwiftOnSecurity Config, Wazuh 4.12.0
- **Virtualization:** VMware Workstation Pro

![Architecture Diagram](architecture/architecture-diagram.png)

## Key Event IDs Monitored
| Event ID | Description | MITRE ATT&CK |
|----------|-------------|--------------|
| 1 | Process Creation | T1059.001 (PowerShell) |
| 3 | Network Connection | T1071 (Application Layer Protocol) |
| 22 | DNS Query | T1071.004 (DNS) |

## Investigation Summary
Simulated a PowerShell execution chain:
1. **Stage 1:** `powershell.exe -ExecutionPolicy Bypass -NoProfile` → Sysmon Event ID 1 → T1059.001
2. **Stage 2:** DNS lookup for `raw.githubusercontent.com` → Sysmon Event ID 22 → T1071.004
3. **Stage 3:** Outbound connection to `8.8.8.8:53` → Sysmon Event ID 3 → T1071

All events were correlated by **Process ID 5052** in Wazuh.

## Skills Demonstrated
- SIEM deployment and configuration (Wazuh)
- Endpoint telemetry collection (Sysmon)
- Log analysis and alert triage
- MITRE ATT&CK mapping
- Incident documentation

## Full Report
See [Investigation Report](investigation-report/incident-report.md) for detailed analysis.
