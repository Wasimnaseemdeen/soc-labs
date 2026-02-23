# SOC LAB 5 — SPLUNK SIEM ALERTING (FAILED AUTHENTICATION)

## OBJECTIVE
Ingest Linux authentication logs into Splunk and create a scheduled alert to detect repeated failed authentication attempts (threshold-based detection).

## ENVIRONMENT
- OS: Kali Linux (VMware)
- Log source: `/var/log/auth.log` (generated via rsyslog)
- SIEM: Splunk Enterprise (local install)
- Index: `main`

## DATA INGESTION SUMMARY
1. Enabled auth logging to `/var/log/auth.log` (rsyslog).
2. Configured Splunk to monitor: `/var/log/auth.log`
3. Fixed permissions so Splunk could read auth logs (added Splunk user to `adm` group).

## ATTACK SIMULATION
- Generated multiple authentication failures using `su testuser` with incorrect passwords.
- Verified events exist in `/var/log/auth.log` using:
  - `tail -n 20 /var/log/auth.log`

## DETECTION QUERY (SPL)
Detect users with 3 or more failures within the search window:

```spl
index=main source="/var/log/auth.log" ("authentication failure" OR "FAILED SU")
| stats count as fails, values(host) as host by user
| where fails >= 3
