# Lumma Stealer Incident Report

**Title:** Lumma Stealer Infection – Suspicious C2 Beaconing Detected  
**Report ID:** https://www.malware-traffic-analysis.net/2026/01/31/index.html  
**Analyst:** Djibril  
**Date of Report:** March 30, 2026  
**Incident Date/Time:** 2026-01-27 23:05 UTC (Suricata alert trigger)  
**PCAP Analyzed:** 2026-01-31-traffic-analysis-exercise.pcap

## 1. Executive Summary

A Suricata signature (`ET MALWARE Lumma Stealer Victim Fingerprinting Activity`) triggered on outbound HTTP traffic to external IP 153.92.1.49 over TCP port 80.  

Using Wireshark, I performed detailed packet-level analysis and confirmed a Lumma Stealer infection on an internal Windows client in the 10.1.21.0/24 LAN segment.  

The infected host performed a DNS query for its C2 domain `whitepepper.su` immediately before initiating beaconing to the C2 IP. The traffic pattern matches Lumma Stealer’s lightweight victim fingerprinting behavior.

**Key outcome:** The compromised endpoint has been fully identified, enabling immediate containment.

## 2. Network Environment
- **LAN Segment:** 10.1.21.0/24  
- **Domain:** win11office.com  
- **Active Directory Domain:** WIN11OFFICE  
- **Domain Controller:** 10.1.21.2 (WIN-LU4L24X3UB7)  
- **Default Gateway:** 10.1.21.1  
- **Broadcast Address:** 10.1.21.255  

## 3. Methodology

1. Opened the PCAP in Wireshark on a Kali Linux VM.  
2. Applied targeted display filters to isolate the Suricata-triggered traffic.  
3. Used protocol analysis (DNS, NBNS, SAMR, Ethernet II) to extract host and user details.  
4. Reviewed Conversations, Protocol Hierarchy, and IO Graph for traffic patterns.  
5. Mapped findings to IBM Cybersecurity Fundamentals concepts.

**Key Wireshark Filters Used:**
- `ip.addr == 153.92.1.49`
- `ip.addr == 10.1.21.58`
- `dns contains "whitepepper"`
- `nbns`
- `samba` or `samr`
- `frame.time_relative >= 92 && frame.time_relative <= 93`
- Ethernet II header for MAC address

## 4. Analysis & Findings

**Infected Windows Client Details:**

1. **IP Address:** 10.1.21.58  
   — Identified as the host performing the DNS query and HTTP beaconing.

2. **MAC Address:** 00:21:5d:c8:0e:f2  
   — Extracted from Ethernet II Source field.

3. **Hostname:** DESKTOP-ES9F3ML  
   — Discovered via NBNS registration packets.

4. **User Account Name:** Wyatt  
   — Extracted from SAMR authentication packets.

5. **Full Name of the User:** Gabriel Wyatt  
   — Appeared in SAMR user account information.

**Evidence of Compromise:**
- DNS query for `whitepepper.su` at ~92.344s relative time, followed by TCP connection to 153.92.1.49:80.
- Short HTTP beaconing consistent with Lumma Stealer behavior.
- Anomalous outbound traffic visible in Wireshark statistics.

*(Insert screenshots here from the screenshots/ folder)*

## 5. Mapping to IBM Cybersecurity Fundamentals
- **Types of Attacks:** Information stealer malware using HTTP C2 beaconing.
- **Detection:** Suricata signature validation through manual Wireshark analysis.
- **Incident Response:** Rapid asset identification supports containment and eradication.
- **Risk Management:** Highlights risks of information stealers and the need for DNS/HTTP monitoring.

## 6. Recommendations

**Immediate Actions:**
- Isolate host 10.1.21.58 from the network.
- Block 153.92.1.49 and domain `whitepepper.su`.
- Reset credentials for user "Wyatt".

**Long-term Prevention:**
- Strengthen DNS monitoring and sinkholing.
- Deploy EDR with behavioral detection for stealers.
- Keep Suricata rules updated.
- Conduct regular phishing awareness training.

## 7. Lessons Learned
- Protocol filters (DNS, NBNS, SAMR) greatly speed up triage.
- Combining Suricata alerts with Wireshark provides strong validation.
- Behavioral analysis is critical for detecting living-off-the-land stealers.

## References
- IBM SkillsBuild: Cybersecurity Fundamentals
- Malware-Traffic-Analysis.net – 2026-01-31 Exercise
- Wireshark Documentation
