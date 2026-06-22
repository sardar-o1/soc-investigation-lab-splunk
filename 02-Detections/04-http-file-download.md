# HTTP File Download Detection

Detects payload download activity by identifying PowerShell HTTP connections and the creation of downloaded files on the host.

## Detection 1: HTTP Connection to Attacker Server

## SPL Query

```bash
index=windows10 source=Sysmon EventCode=3
| rex field=_raw "SourceHostname:\s+(?<SourceHostname>[^\r\n]+)"
| rex field=_raw "Image:\s+(?<Image>[^\r\n]+)"
| rex field=_raw "DestinationIp:\s+(?<DestinationIp>[^\r\n]+)"
| rex field=_raw "DestinationPort:\s+(?<DestinationPort>[^\r\n]+)"
| search DestinationIp="192.168.31.63"
| table _time SourceHostname Image DestinationIp DestinationPort
```


## Detection Methodology

- Monitor Sysmon Event ID 3 (Network Connection).
- Identify outbound HTTP connections initiated by PowerShell.
- Review connections to attacker-controlled hosts.
- Correlate network activity with file creation events.

## Detection 2: Payload Downloaded to Disk

## SPL Query

```bash
index=windows10 source=Sysmon EventCode=11
| rex field=_raw "User:\s+(?<User>[^\r\n]+)"
| rex field=_raw "RuleName:\s+(?<RuleName>[^\r\n]+)"
| rex field=_raw "Image:\s+(?<Image>[^\r\n]+)"
| rex field=_raw "TargetFilename:\s+(?<TargetFilename>[^\r\n]+)"
| table _time User RuleName Image TargetFilename
```

## Detection Methodology

- Monitor Sysmon Event ID 11 (File Creation).
- Identify the batch file created by PowerShell.
- Investigate files written to user-accessible directories.

## Detection Result

The investigation identified a PowerShell HTTP connection to 192.168.31.63:80 and the creation of payload.bat on the victim host. These correlated events confirm successful payload delivery to the victim system.

## Screenshots

####  HTTP Connection Detection
![img](https://github.com/sardar-o1/soc-investigation-lab-splunk/blob/37a7e1a551437be18797b9bdeaa40a8e8e9dfe34/Screenshots/splunk_query5.png)

#### Payload Download Detection
![img](https://github.com/sardar-o1/soc-investigation-lab-splunk/blob/37a7e1a551437be18797b9bdeaa40a8e8e9dfe34/Screenshots/splunk_query4.png)

