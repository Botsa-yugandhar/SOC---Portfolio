# Phishing Email Malware Investigation

## Incident Summary

A phishing email containing a malicious attachment was delivered to the user. The attachment was executed, leading to PowerShell-based malware activity and external network communication.

---

## Investigation Evidence

### Phishing Email
![Email](screenshots/phishing_email.png)

### Attachment Execution
![Attachment](screenshots/attachment_execution.png)

### Malware Execution
![Malware](screenshots/malware_execution.png)

### External Network Connection
![C2](screenshots/c2_connection.png)

### Antivirus Detection
![AV](screenshots/antivirus_detection.png)

---

## Attack Chain Analysis

1. A phishing email with a macro-enabled attachment (.docm) was delivered to the user.
2. The user opened the attachment using Microsoft Word (winword.exe).
3. The document triggered PowerShell execution with encoded commands (-enc).
4. PowerShell established an external network connection to a suspicious IP address.
5. Antivirus detected a Trojan related to the executed file.

This sequence confirms a full phishing attack leading to malware execution and potential system compromise.

## Key Findings

- Phishing email delivered with macro-enabled attachment (.docm)
- User execution of attachment triggered Word process
- Word process spawned PowerShell with encoded commands (-enc)
- Encoded PowerShell indicates obfuscated malicious activity
- External network connection suggests possible command & control (C2)
- Antivirus detection confirms presence of Trojan malware

---

## MITRE ATT&CK Mapping

- T1566 — Phishing  
- T1059 — Command and Scripting Interpreter  

---

## Severity

Critical

---

## Detection Logic

Trigger alert if:

- Email contains macro-enabled attachment
- Attachment execution followed by PowerShell activity
- External network connection after execution

---

## Recommended Response

- Block sender email
- Quarantine affected system
- Disable macros
- Monitor network traffic

---

## What I Learned

- How phishing attacks deliver malware
- Importance of correlating multiple logs
- Understanding full attack chain
