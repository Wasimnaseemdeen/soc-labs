# Suspicious Login Investigation

## Scenario
A user account triggered multiple failed login attempts followed by a successful login from an unfamiliar IP address.

## Initial Alert
Multiple failed authentication attempts detected within a short time window.

## Investigation Steps
- Reviewed authentication logs
- Checked source IP address
- Checked login timestamps
- Compared against normal user behavior

## Findings
- 12 failed login attempts within 3 minutes
- Successful login immediately after failures
- Source IP not previously associated with the user
- Login occurred outside normal working hours

## MITRE ATT&CK Mapping
- T1110 – Brute Force

## Risk Assessment
Possible credential compromise.

## Recommended Actions
- Force password reset
- Enable MFA for the account
- Block suspicious IP address
- Monitor account activity for 48 hours

## Lessons Learned
Early detection of brute force attempts can prevent account compromise.

