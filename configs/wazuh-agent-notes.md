# Wazuh Deployment Notes

## Server Setup
- OS: Ubuntu Server 26.04 LTS
- Wazuh Version: 4.12.0
- Installation: Quickstart script

## Installation Command
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
sudo bash wazuh-install.sh -a -i

## Agent Setup (Windows 10)
- Wazuh Agent installed on Windows 10 Enterprise
- Agent ID: 001
- Agent IP: 192.168.245.137
- Manager IP: 192.168.245.1

## Key Wazuh Rules Triggered
| Rule ID | Description | MITRE ID |
|---------|-------------|----------|
| 92027 | PowerShell process spawned | T1059.001 |
| 100010 | Sysmon: Network Connection | T1071 |
| 100011 | Sysmon: DNS Query | T1071.004 |
