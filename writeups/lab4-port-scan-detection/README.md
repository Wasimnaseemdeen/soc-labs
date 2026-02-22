# 🛡 SOC Lab 4 – Port Scan Detection (SYN Scan)

## 🎯 Objective
To detect and analyze network reconnaissance activity using Wireshark.

---

## 🖥 Lab Environment
- OS: Kali Linux
- Tool: Wireshark
- Scan Tool: Nmap
- Scan Type: SYN Scan (-sS)
- Target: 127.0.0.1

---

## 🔍 Scenario

A SYN scan was performed against the local machine using:

nmap -sS 127.0.0.1

Network traffic was captured using Wireshark on the loopback interface.

---

## 📜 Evidence Observed

Display filter used:

tcp.flags.syn == 1 && tcp.flags.ack == 0

Observed behavior:
- Multiple SYN packets
- Single source IP
- Multiple destination ports
- Rapid execution
- No completed handshake

Example ports scanned:
443, 587, 554, 110, 3306, 23, 53, 5900, 8888

---

## 🧠 Analysis

The traffic pattern indicates a TCP SYN scan.  
The attacker sends SYN packets to multiple ports to identify open services without completing the TCP handshake.

This behavior is consistent with reconnaissance and service discovery activity.

---

## 🛡 MITRE ATT&CK Mapping

T1046 – Network Service Discovery

---

## 🚦 Severity Assessment

Lab: Informational  
Enterprise (Internal Host): Medium  
Enterprise (External IP): High

---

## 🔎 Detection Logic Example

Alert if:
- One source IP sends SYN packets to more than 20 different destination ports within 10 seconds

Pseudo-rule:

IF unique_destination_ports > 20  
AND time_window < 10 seconds  
THEN trigger Recon Alert

---

## 🧰 Skills Demonstrated

- Packet capture analysis
- SYN flag filtering
- Network reconnaissance detection
- MITRE mapping
- Detection rule logic writing
- Incident documentation

---

## 📌 Key Learning

Port scanning is often the first phase of an attack. Detecting reconnaissance early allows defenders to prevent exploitation stages.
