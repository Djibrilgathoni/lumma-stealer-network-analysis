# Incident Response Runbook - Lumma Stealer

## Immediate Containment
1. Isolate the infected host (10.1.21.58) — disconnect from network.
2. Block outbound connections to:
   - IP: 153.92.1.49
   - Domain: whitepepper.su
3. Reset password for user account "Wyatt".

## Investigation Steps
- Preserve the system for full disk and memory forensics.
- Review Active Directory logs for lateral movement.
- Scan endpoint with updated EDR/antivirus.

## Remediation
- Reimage or rebuild the affected workstation.
- Force password reset across potentially affected accounts.
- Update Suricata rules and monitor for similar .su domains.

## Prevention
- Enable DNS logging and sinkholing.
- Deploy behavioral-based EDR.
- Conduct regular user awareness training on phishing.

**Reference:** Full details in report.md
