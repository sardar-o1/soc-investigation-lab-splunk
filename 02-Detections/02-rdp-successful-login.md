# Successful RDP Login Detection

Detects successful Remote Desktop Protocol (RDP) logins by monitoring Windows Security Event ID 4624 with Logon Type 10 (Remote Interactive).

## SPL Query
```bash
index=windows10 EventCode=4624 Logon_Type=10
| table _time Account_Name Source_Network_Address Logon_Type
| sort _time
```

## Detection Methodology
- Monitor Windows Security Event ID 4624 (Successful Logon).
- Filter for Logon Type 10 (RDP).
- Identify the authenticated account and source IP address.
- Correlate with previous failed logon attempts to identify successful brute-force activity.

## Detection Result

The query identified a successful RDP login from source IP 192.168.31.63 using the account admin11. The successful authentication occurred after multiple failed logon attempts, indicating a successful brute-force attack.
