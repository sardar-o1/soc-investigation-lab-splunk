# Payload Execution Detection

Detects execution of downloaded payloads by monitoring Sysmon process creation events and identifying batch files launched through PowerShell.

## SPL Query

```bash
index=windows10 source=Sysmon EventCode=1
| rex field=_raw "User:\s+(?<User>[^\r\n]+)"
| rex field=_raw "ParentCommandLine:\s+(?<ParentCommandLine>[^\r\n]+)"
| rex field=_raw "Image:\s+(?<Image>[^\r\n]+)"
| rex field=_raw "CommandLine:\s+(?<CommandLine>[^\r\n]+)"
| search CommandLine="*payload.bat*"
| table _time User ParentCommandLine Image CommandLine
```

## Detection Methodology

- Monitor Sysmon Event ID 1 (Process Creation).
- Identify execution of batch files.
- Detect PowerShell-initiated payload execution.

## Detection Result

The investigation identified PowerShell executing the downloaded file payload.bat, which subsequently launched cmd.exe. This activity confirms successful payload execution on the victim host.
