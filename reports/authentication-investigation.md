# Investigation 1 — Controlled Windows authentication failure

**Date:** October 18, 2026  
**System:** Windows 11 lab endpoint monitored by Wazuh Cloud  
**Classification:** Authorized test; no confirmed security incident

## Objective
Observe whether Wazuh detects a failed Windows logon and interpret the alert's evidence.

## Test and observations
A single `runas` attempt was made with an intentionally incorrect password. Windows displayed a login failure. Wazuh subsequently recorded a matching event at the expected time.

- Windows Event ID: `4625` (`An account failed to log on`)
- Wazuh rule: `60122`, level `5`, description `Logon Failure - Unknown user or bad password`
- Logon Type: `2` (interactive)
- Status: `0xC000006D` (authentication failure)
- Substatus: `0xC000006A` (incorrect password)
- Process name shown: `C:\Windows\System32\svchost.exe`

## Analysis and disposition
The event matched the deliberately generated authentication failure. Because this was an authorized test, I classify this alert as benign test activity. In an unexplained real-world case, a single failure would not be sufficient to prove either an attack or harmless user error. I would review frequency, source, targeted accounts, and any successful logons or other events that followed.

**Recommended disposition:** Document and close this known test alert; continue routine monitoring.

## Evidence
- [`Alert Overview.png`](../evidence/authentication/Alert%20Overview.png)
- [`Authentication Details.png`](../evidence/authentication/Authentication%20Details.png)
