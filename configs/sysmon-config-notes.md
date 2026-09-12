# Sysmon Configuration Notes

## Tool Version
- Sysmon v15.21 (Microsoft Sysinternals)

## Configuration Used
- SwiftOnSecurity Sysmon Config (v4.50)
- Source: https://github.com/SwiftOnSecurity/sysmon-config

## Key Events Enabled
- Event ID 1: Process Creation (with command line + hashes)
- Event ID 3: Network Connection
- Event ID 22: DNS Query

## Installation Command
sysmon64.exe -i sysmonconfig-export.xml

## Verification Command
sysmon64.exe -c
