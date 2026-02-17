# Port Scan Detection Investigation

## Scenario
A firewall alert detected multiple connection attempts from a single external IP address targeting sequential ports on a web server.

## Initial Alert
High number of connection attempts across multiple ports within a short time frame.

## Investigation Steps
- Reviewed firewall logs
- Identified source IP address
- Analyzed port sequence patterns
- Checked IDS/IPS alerts

## Findings
- Sequential port attempts (e.g., 21, 22, 23, 80, 443)
- Over 50 connection attempts within 2 minutes
- No successful authentication attempts
- Behavior consistent with reconnaissance activity

## MITRE ATT&CK Mapping
- T1046 – Network Service Scanning

## Risk Assessment
Potential reconnaissance phase of an attack.

## Recommended Actions
- Block or rate-limit source IP
- Monitor for repeated scanning attempts
- Review exposed services
- Harden unnecessary open ports

## Lessons Learned
Early detection of reconnaissance activity helps prevent exploitation.
