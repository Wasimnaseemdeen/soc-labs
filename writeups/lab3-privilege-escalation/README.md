# 🛡 SOC Lab 3 – Privilege Escalation Detection (sudo)

## 🎯 Objective
To detect and analyze privilege escalation attempts using sudo logs in a Linux environment.

---

## 🖥 Lab Environment
- OS: Kali Linux (VMware)
- Log Source: systemd journal (journalctl)
- User Account: kali (UID 1000)

---

## 🔍 Scenario

A user attempted to execute privileged commands using sudo.  
Multiple authentication failures were observed before a successful privilege escalation to root.

---

## 📜 Log Evidence

Authentication failure:
```
pam_unix(sudo:auth): authentication failure; user=kali
```

Multiple incorrect attempts:
```
kali : 3 incorrect password attempts ; USER=root ; COMMAND=/usr/bin/ls
```

Successful privilege escalation:
```
pam_unix(sudo:session): session opened for user root(uid=0)
```

---

## 🧠 Analysis

The user `kali` attempted to execute a sudo command.  
Three incorrect password attempts were logged, followed by a successful root session.

This pattern indicates:
- Credential guessing behavior
- Potential brute-force attempt
- Privilege escalation using valid credentials

In an enterprise environment, this sequence would require investigation to determine whether the activity was legitimate or malicious.

---

## 🛡 MITRE ATT&CK Mapping

- **T1110 – Brute Force**
- **T1078 – Valid Accounts**
- **T1068 – Privilege Escalation**

---

## 🚦 Severity Assessment

Lab Environment: Informational  
Enterprise Environment: Medium → High (if unauthorized)

---

## 🔎 Detection Logic Example

Alert if:
- 3 or more failed sudo attempts occur within 2 minutes
- Followed by a successful root session

Pseudo detection rule:

IF failed_sudo_count >= 3  
AND sudo_session_opened = TRUE  
THEN trigger High Severity Alert

---

## 🧰 Skills Demonstrated

- Linux log analysis
- journalctl filtering
- Authentication failure investigation
- Privilege escalation detection
- MITRE ATT&CK mapping
- Incident documentation

---

## 📌 Key Learning

Understanding the sequence of failed authentication attempts followed by a successful privilege escalation is critical for detecting insider threats and compromised accounts.

---
