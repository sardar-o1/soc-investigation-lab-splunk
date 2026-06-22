# Alert Configuration

## Alert 1: RDP Brute Force Detected

**Purpose:** Detect excessive failed RDP logon attempts.

**Data Source:** Windows Security Logs 

**Event ID:** 4625

**Severity:** Medium

**Trigger Condition:** More than 10 failed logon attempts from the same source IP.

## Alert 2: Successful Login Following Brute Force

**Purpose:** Detect successful authentication after repeated failed logon attempts.

**Data Source:** Windows Security Logs

**Event IDs:** 4625, 4624

**Severity:** High

**Trigger Condition:** More than 10 failed logon attempts followed by at least one successful login from the same source IP.
