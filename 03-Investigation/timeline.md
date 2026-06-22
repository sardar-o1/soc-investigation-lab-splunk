# Attack Timeline

## Overview

The following timeline summarises the attack progression observed during the investigation.


| Time | Event |	Evidence |
| :--- | :--- | :--- |
| 16:08 |	RDP Brute Force	| Windows Event ID 4625 - Multiple failed logon attempts from 192.168.31.63 |
| 16:10 |	Successful RDP Login	| Windows Event ID 4624 (Logon Type 10) using account admin11 |
| 16:14 |	User Discovery	| Sysmon Event ID 1 - whoami /all |
| 16:14 |	Network Discovery	| Sysmon Event ID 1 - ipconfig /all |
| 16:15 |	Process Discovery	| Sysmon Event ID 1 - tasklist |
| 16:15 |	System Discovery	| Sysmon Event ID 1 - systeminfo |
| 16:22 |	Payload Download	| Sysmon Event ID 11 - payload.bat created on disk |
| 16:22 |	HTTP Connection	| Sysmon Event ID 3 - PowerShell connected to 192.168.31.63:80 |
| 16:25 |	Payload Execution	| Sysmon Event ID 1 - payload.bat executed via PowerShell |
