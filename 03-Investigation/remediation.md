# Remediation Recommendations

## 01. RDP Brute Force

### Contain

Respond to repeated failed RDP authentication attempts.

* Block offending IP addresses at the firewall.
* Disable external RDP exposure if not required.
* Enforce account lockout policies.
* Review logs for additional suspicious authentication activity.

---

## 02. RDP Successful Login

### Investigate

Determine whether the successful login was authorized.

* Verify whether the login followed multiple failed attempts.
* Validate the legitimacy of the user activity.
* Reset credentials for potentially compromised accounts.
* Terminate unauthorized remote sessions.
* Enable Multi-Factor Authentication (MFA) for RDP access.

---

## 03. Discovery Commands

### Monitor

Identify potential reconnaissance activity on the host.

* Review executed discovery commands.
* Correlate activity with the user's expected behavior.
* Investigate additional post-compromise activity.

---

## 04. HTTP File Download

### Block

Prevent further payload delivery and external communication.

* Identify the downloaded file and calculate its hash.
* Block the attacker IP address at the firewall.
* Quarantine the affected endpoint.
* Submit the file to a malware sandbox for analysis.

---

## 05. Payload Execution

### Eradicate

Remove malicious artifacts and restore system integrity.

* Terminate malicious processes.
* Remove malicious files and persistence mechanisms.
* Reimage or restore the system if necessary.
* Apply security updates and hardening measures.
* Monitor for signs of reinfection.
