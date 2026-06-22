# MITRE ATT&CK Mapping – Timeline View

This document maps the observed attacker activities to the corresponding MITRE ATT&CK tactics and techniques.


| Time   | Event                | Evidence                                                   | MITRE Technique |
|--------|----------------------|------------------------------------------------------------|-----------------|
| 16:08  | RDP Brute Force      | Windows Event ID 4625 – Multiple failed logon attempts     | T1110.001 – Password Guessing |
| 16:10  | Successful RDP Login | Windows Event ID 4624 (Logon Type 10) using account admin11 | T1021.001 – Remote Desktop Protocol |
| 16:14  | User Discovery       | Sysmon Event ID 1 – whoami /all                            | T1033 – System Owner/User Discovery |
| 16:14  | Network Discovery    | Sysmon Event ID 1 – ipconfig /all                          | T1016 – Network Configuration Discovery |
| 16:15  | Process Discovery    | Sysmon Event ID 1 – tasklist                               | T1057 – Process Discovery |
| 16:15  | System Discovery     | Sysmon Event ID 1 – systeminfo                             | T1082 – System Information Discovery |
| 16:22  | Payload Download     | Sysmon Event ID 11 – payload.bat created on disk           | T1105 – Ingress Tool Transfer |
| 16:22  | HTTP Connection      | Sysmon Event ID 3 – PowerShell connected to 192.168.31.63:80 | T1071.001 – Web Protocols |
| 16:25  | Payload Execution    | Sysmon Event ID 1 – payload.bat executed via PowerShell    | T1059.001 – PowerShell |

