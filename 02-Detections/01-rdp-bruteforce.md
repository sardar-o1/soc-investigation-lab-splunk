# RDP Brute Force Detection

Detects potential RDP brute-force activity by identifying Windows failed logon events (Event ID 4625) from the same source IP address against a user account.

## SPL Query:

```bash
index=windows10 eventcode=4625
| stats count by account_name source_network_address failure_reason
| where count > 10
| search account_name!="-"
```

## Detection Methodology
- Monitor Windows Security Event ID 4625 (Failed Logon).
- Aggregate failed authentication attempts by account name and source IP address.
- Count the number of failed logons for each account.
- Filter results where failed attempts exceed 10.
- Exclude events with invalid account names.

## Detection Result

The query identified 37 failed logon attempts against the account admin11 from the source IP address 192.168.31.63. The failure reason was "Unknown user name or bad password", indicating a likely password-guessing or brute-force attack against the RDP service.

## Screenshot
![img](https://github.com/sardar-o1/soc-investigation-lab-splunk/blob/37a7e1a551437be18797b9bdeaa40a8e8e9dfe34/Screenshots/splunk_query1.png)
