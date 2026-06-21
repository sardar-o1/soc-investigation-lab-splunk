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

A simulated attacker attempted to gain access to a Windows 10 host through an RDP brute-force attack against a valid user account. Following successful authentication, the attacker performed basic host discovery activities, accessed an attacker-controlled HTTP server, downloaded a batch file to the victim system, and executed the downloaded file, resulting in the creation of a command prompt (cmd.exe) process.

## Key Detections

- RDP Brute Force Activity (Windows Security Event ID 4625)
- Successful RDP Authentication (Windows Security Event ID 4624)
- Discovery Command Execution (Sysmon Event ID 1)
- Outbound Connection to Attacker HTTP Server (Sysmon Event ID 3)
- Payload File Creation - payload.bat (Sysmon Event ID 11)
- Payload Execution (Sysmon Event ID 1)
- PowerShell Process Creation (Sysmon Event ID 1)


## Learning Outcomes

Through this project, I gained practical experience in:

- Security monitoring and investigation using Splunk Enterprise.
- Analyzing Windows Security Logs and Sysmon telemetry.
- Detecting brute-force attacks, unauthorized access, and suspicious process activity.
- Building SPL-based detections for multiple stages of an attack chain.
- Correlating events to create an attack timeline and identify attacker actions.
- Mapping adversary behavior to the MITRE ATT&CK framework.
- Documenting findings and remediation recommendations in a structured incident report.
