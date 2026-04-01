# Wireshark Filters & Methodology

## Key Display Filters Used

- **C2 Traffic:** `ip.addr == 153.92.1.49`
- **Infected Host:** `ip.addr == 10.1.21.58`
- **C2 Domain Query:** `dns contains "whitepepper"`
- **Hostname Discovery:** `nbns`
- **User Details:** `samba` or `samr`
- **Critical Time Window:** `frame.time_relative >= 92 && frame.time_relative <= 93`
- **MAC Address:** Filter on Ethernet II → Source

## Analysis Steps
1. Filter on the external C2 IP to isolate malicious traffic.
2. Identify the internal source IP with highest conversation volume.
3. Locate DNS query for suspicious domain.
4. Use NBNS to extract hostname.
5. Use kerberos to extract user account and full name.
6. Inspect Ethernet headers for MAC address.

These filters enabled quick attribution during the investigation.
