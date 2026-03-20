# SOC Detection Rules

## Objective

These detection rules are designed to identify common attack patterns such as brute force attacks, PowerShell abuse, and phishing-based malware activity using log analysis in SIEM systems.

---

## Rule 1 — Brute Force Attack Detection

### Condition

- EventCode 4625 (failed login)
- Multiple attempts from same IP
- Short time duration

### Detection Logic

Trigger alert if more than 5 failed login attempts are observed from a single IP within a short timeframe.

### Splunk Query

index=main EventCode=4625 
| stats count by src_ip 
| where count > 5

### Severity

High



---

## Rule 2 — Successful Brute Force Detection

### Condition

- Multiple failed logins (EventCode 4625)
- Followed by successful login (EventCode 4624)
- Same source IP

### Detection Logic

Trigger alert if multiple failed login attempts are followed by a successful login from the same IP.

### Splunk Query

index=main (EventCode=4625 OR EventCode=4624) 
| stats count by src_ip EventCode

### Severity

Critical



---

## Rule 3 — Suspicious PowerShell Execution

### Condition

- PowerShell execution
- Command contains "-enc"

### Detection Logic

Trigger alert when PowerShell is executed with encoded commands, indicating possible obfuscation.

### Splunk Query

index=main powershell "-enc"

### Severity

High



---

## Rule 4 — Office Spawning PowerShell

### Condition

- Office application (winword.exe / excel.exe)
- Followed by PowerShell execution

### Detection Logic

Trigger alert when an Office application spawns PowerShell, which may indicate macro-based attack.

### Splunk Query

index=main process=winword.exe OR process=powershell.exe

### Severity

High



---

## Rule 5 — Phishing-Based Malware Detection

### Condition

- Email with attachment (.docm)
- Attachment execution
- PowerShell execution
- External network connection

### Detection Logic

Trigger alert when phishing email activity leads to execution and external communication, indicating malware infection.

### Splunk Query

index=main (email_from=* OR powershell OR network_connection)

### Severity

Critical


---

## Conclusion

These detection rules demonstrate the ability to identify and correlate multiple attack patterns using log analysis. They focus on real-world attack scenarios such as brute force, PowerShell abuse, and phishing-based malware execution.
