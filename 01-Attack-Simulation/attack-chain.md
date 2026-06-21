# Attack Chain Simulation

## Overview

This attack simulation was conducted in a controlled lab environment to emulate a common intrusion scenario and generate telemetry for detection and investigation in Splunk.

The attack was performed from a Kali Linux attacker machine against a Windows 10 victim machine monitored with Sysmon and Windows Security logging.

Before the simulation, the Windows 10 victim machine was configured to support Remote Desktop Protocol (RDP) access. A local user account was created, Remote Desktop was enabled, inbound RDP connections (TCP 3389) were allowed through Windows Firewall, and the local user account was added to the Remote Desktop Users group.

This configuration allowed the attacker to conduct a brute-force attack against a valid user account and establish a remote session upon successful authentication.
#

# Attack Flow
## 1. RDP Brute Force

The attack simulation began with a brute-force attack against the Windows 10 host's Remote Desktop Protocol (RDP) service using Hydra. A password wordlist containing both invalid and valid credentials was used against a known local user account. Multiple failed authentication attempts were generated before Hydra successfully discovered the correct password, resulting in a successful RDP authentication.
### Command Used

```bash
hydra -l LocalUser -P passwdlist.txt rdp://<Windows10-IP> -t 4 -V -f
```

## 2. Successful RDP Authentication



