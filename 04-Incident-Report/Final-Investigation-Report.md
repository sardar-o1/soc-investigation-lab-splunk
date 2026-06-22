# Final Investigation Report

## Executive Summary

A simulated attack was conducted in a controlled lab environment to emulate a common intrusion scenario involving Remote Desktop Protocol (RDP) brute-force activity, successful remote access, host reconnaissance, payload delivery, and payload execution - all mapped to MITRE ATT&CK.

Using Windows Security logs and Sysmon telemetry collected in Splunk, the attack was successfully detected and investigated from initial access through execution.

---

## Investigation Findings

The investigation identified multiple failed RDP authentication attempts originating from the attacker host (192.168.31.63), indicating a brute-force attack against a local Windows account.

Following repeated authentication failures, the attacker successfully authenticated to the victim system using valid credentials and established an RDP session.

After gaining access, the attacker executed several discovery commands to gather information about the compromised host, including user, network, process, and operating system details.

PowerShell was then used to connect to an attacker-controlled HTTP server and download a batch file (`payload.bat`) to the victim machine. Subsequent process creation events confirmed execution of the downloaded payload, resulting in the launch of a Windows command shell (`cmd.exe`).

---

## Attack Timeline

1. "16:08 - RDP Brute Force (Windows Event ID 4625)"
2. "16:10 - Successful RDP Login (Windows Event ID 4624)"
3. "16:14 - Host Discovery Commands (Sysmon Event ID 1)"
4. "16:22 - HTTP Connection to Attacker Server (Sysmon Event ID 3)"
5. "16:22 - Payload Downloaded to Disk (Sysmon Event ID 11)"
6. "16:25 - Payload Execution (Sysmon Event ID 1)"

---

## MITRE ATT&CK Techniques Observed

| Technique ID | Technique                              |
| ------------ | -------------------------------------- |
| T1110.001    | Password Guessing                      |
| T1021.001    | Remote Desktop Protocol                |
| T1033        | System Owner/User Discovery            |
| T1016        | System Network Configuration Discovery |
| T1057        | Process Discovery                      |
| T1082        | System Information Discovery           |
| T1105        | Ingress Tool Transfer                  |
| T1071.001    | Web Protocols                          |
| T1059.001    | PowerShell                             |

---

## Conclusion

The attack simulation successfully demonstrated the full attack lifecycle from initial access to payload execution. Splunk detections and Sysmon telemetry provided sufficient visibility to identify each stage of the intrusion and reconstruct the attack timeline.

This project highlights how Windows Security logs and Sysmon can be leveraged to detect brute-force attacks, investigate post-compromise activity, and support incident response workflows within a SOC environment.
