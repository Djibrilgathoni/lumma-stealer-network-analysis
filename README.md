# Lumma Stealer — Network Forensics Analysis

**Project**: Lumma Stealer Infection – Suspicious C2 Beaconing Detected  
**Author**: Djibril Gathoni
**Date**: 30th March 2026  
**Source**: [Malware-Traffic-Analysis.net (2026-01-31)](https://www.malware-traffic-analysis.net/2026/01/31/index.html)  
**Context**: Practical application IBM SkillsBuild – Cybersecurity 

## Overview
A Suricata signature (`ET MALWARE Lumma Stealer Victim Fingerprinting Activity`) triggered on outbound HTTP traffic to external IP `153.92.1.49` over TCP port 80.  

Detailed packet-level analysis using **Wireshark** confirmed a **Lumma Stealer** (information stealer) infection on an internal Windows client in the `10.1.21.0/24` segment.  

The infected host queried the C2 domain `whitepepper.su` before starting beaconing activity. This project demonstrates core blue team skills in network traffic analysis, IDS alert validation, host/user attribution, and incident response.

## Key Findings

| Item                        | Value                          |
|-----------------------------|--------------------------------|
| Malware Family              | Lumma Stealer                  |
| C2 Server IP                | 153.92.1.49                    |
| C2 Port                     | TCP 80 (HTTP)                  |
| C2 Domain                   | whitepepper.su                 |
| Infected Host IP            | 10.1.21.58                     |
| Infected Host MAC           | 00:21:5d:c8:0e:f2              |
| Hostname                    | DESKTOP-ES9F3ML                |
| Compromised User Account    | Wyatt                          |
| Full User Name              | Gabriel Wyatt                  |
| Detection Trigger           | Suricata ET MALWARE signature  |
| Incident Time               | 2026-01-27 ~23:05 UTC          |

## Repository Contents
- `README.md` — Project overview (this file)
- `report.md` — Full detailed incident report
- `iocs.md` — Extracted Indicators of Compromise
- `wireshark-filters.md` — Methodology and all Wireshark display filters used
- `runbook.md` — Incident response and containment playbook
- `screenshots/` — Supporting Wireshark screenshots and evidence

## Skills Demonstrated
- Network traffic analysis and anomaly detection with Wireshark
- DNS query analysis and C2 domain identification
- Host and user attribution using NBNS and SAMR protocols
- Validation of Suricata IDS signatures through manual packet inspection
- Mapping technical findings to IBM Cybersecurity Fundamentals concepts
- Professional incident reporting and documentation

## Tools Used
- Wireshark
- Kali Linux
- Suricata

---

**Part of my Blue Team Cybersecurity learning journey — March 2026**
