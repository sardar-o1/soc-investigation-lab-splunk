# Discovery Commands Detection

Detects common host discovery and reconnaissance commands executed after successful access to a Windows system. These commands are frequently used by attackers to gather information about the current user, system configuration, running processes, and network settings.

## SPL Query

```bash
index=windows10 source=Sysmon EventCode=1
| rex field=_raw "Image:\s+(?<Image>[^\r\n]+)"
| rex field=_raw "CommandLine:\s+(?<CommandLine>[^\r\n]+)"
| rex field=_raw "User:\s+(?<User>[^\r\n]+)"
| search User="*admin11*"
| search CommandLine="*whoami*" OR CommandLine="*ipconfig*" OR CommandLine="*tasklist*" OR CommandLine="*systeminfo*"
| table _time User Image CommandLine
| sort _time
```

## Detection Methodology

- Monitor Sysmon Event ID 1 (Process Creation).
- Extract process image, command line, and user information.
- Identify execution of common discovery commands such as whoami, ipconfig, tasklist, and systeminfo.
- Review commands executed after successful RDP authentication.

## Detection Result

The query identified the execution of multiple discovery commands by WINDOWS-VM\admin11, including: whoami /all, ipconfig /all, tasklist, systeminfo.

These commands were executed shortly after the successful RDP login and are consistent with attacker reconnaissance activity performed to gather information about the compromised host.

## Screenshot
![img](https://github.com/sardar-o1/soc-investigation-lab-splunk/blob/37a7e1a551437be18797b9bdeaa40a8e8e9dfe34/Screenshots/splunk_query3.png)



