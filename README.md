# soc-investigation-lab-splunk

## Overview

This project demonstrates a host-based Security Operations Center (SOC) investigation conducted using Splunk within a controlled VirtualBox lab environment.

The objective of this project was to simulate a realistic attack chain, collect endpoint telemetry, develop detections, investigate attacker activity, and document findings through a structured incident response workflow.

The attack was performed in an isolated lab environment using Kali Linux as the attacker machine and Windows 10 as the victim machine.

To focus on fundamental SOC investigation techniques, this project utilizes a simple attack chain consisting of RDP brute-force attempts, successful authentication, host discovery, PowerShell-based file download activity, and execution of a downloaded batch file.

## Lab Environment

| Component | Role |
| :--- | :--- |
| **Kali Linux** | Attack | 
| **Windows 10** | Victim | 
| **Sysmon** | Endpoint Telemetry |
| **Ubuntu Server** | Splunk Enterprise (SIEM) |  


## Attack Scenario

A simulated attacker attempted to gain access to a Windows 10 host through an RDP brute-force attack. Following successful authentication, the attacker performed basic host discovery activities, used PowerShell to download a batch file from an attacker-controlled HTTP server, and executed the downloaded file on the victim system.

## Key Detections

- RDP Brute Force Activity (Windows Security Event ID 4625)
- Successful RDP Authentication (Windows Security Event ID 4624)
- Discovery Command Execution (Sysmon Event ID 1)
- PowerShell Invoke-WebRequest Activity (PowerShell Event ID 4104)
- Payload File Creation - payload.bat (Sysmon Event ID 11)
- PowerShell Execution of Downloaded Payload (Sysmon Event ID 1)

## MITRE ATT&CK Mapping

| Attack Stage | Technique | ATT&CK ID |
| :--- | :--- | :--- |
| RDP Brute Force	| Brute Force |	T1110 |
| Successful RDP Login	| Remote Services: Remote Desktop Protocol	| T1021.001 | 
| Host Discovery	| System Information Discovery	| T1082 | 
| PowerShell Execution	| Command and Scripting Interpreter: PowerShell	| T1059.001 | 
| File Download via Invoke-WebRequest	| Ingress Tool Transfer	| T1105 | 
| Batch File Execution	| User Execution	| T1204 |

## Learning Outcomes

Coming Soon... This project is currently under development.
