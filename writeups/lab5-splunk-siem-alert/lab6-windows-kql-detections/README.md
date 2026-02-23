
---

# Lab 6 Writeup (paste this)

**File:** `writeups/lab6-windows-kql-detections/README.md`

```md
# SOC LAB 6 — WINDOWS AUTH DETECTIONS (KQL PACK)

## OBJECTIVE
Demonstrate SOC Tier-1 detection logic using KQL for Windows authentication activity and common attack patterns.

## KEY WINDOWS EVENTS
- 4625: Failed Logon
- 4624: Successful Logon
- 4688: Process Creation
- 4672: Special Privileges Assigned

## BRUTE FORCE (4625 THRESHOLD)
```kql
SecurityEvent
| where EventID == 4625
| summarize FailCount=count() by Account, bin(TimeGenerated, 10m)
| where FailCount >= 5
| order by TimeGenerated desc
