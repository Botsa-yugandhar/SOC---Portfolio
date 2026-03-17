# Windows Brute Force Attack Investigation

## Incident Summary

Multiple failed login attempts were detected against the Administrator account from a single IP address.

## Log Evidence

Windows Event ID 4625 indicates failed login attempts.

## Investigation Steps

1. Identified repeated failed login attempts
2. Observed same source IP
3. High frequency within short timeframe

## MITRE ATT&CK Mapping

Technique: T1110 - Brute Force

## Detection Rule

If more than 5 failed login attempts occur from the same IP within 5 minutes, trigger an alert.

## Recommended Response

- Block the attacking IP
- Reset affected account passwords
- Enable Multi-Factor Authentication
