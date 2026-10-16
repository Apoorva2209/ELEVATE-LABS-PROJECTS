# Elevate Labs – Cybersecurity Internship Projects

Hands-on cybersecurity lab tasks completed during the Elevate Labs programme, each documented with objective, method, findings and conclusions.

## Tasks

| # | Task | Tools | Folder |
| --- | --- | --- | --- |
| 1 | Network scanning and port analysis | Nmap 7.98, Windows | [task-01-nmap-network-scan](task-01-nmap-network-scan) |

---

## Task 1 – Network Scanning with Nmap

### Objective
Discover live hosts on a local network and identify their open ports and services, to understand the network's exposure.

### Environment
- Nmap 7.98 on Windows
- Local network `192.168.1.0/24` (256 addresses)
- Scan date: 13 Nov 2025

### Method
A TCP SYN (half-open) scan of the whole subnet:

```bash
nmap -sS 192.168.1.0/24
```

Raw output: [`TASK1.nmap`](task-01-nmap-network-scan/TASK1.nmap)

### Results
256 addresses scanned, **4 hosts up**, in 33.46 seconds.

| Host | Role | Open ports | Notes |
| --- | --- | --- | --- |
| 192.168.1.1 | Router / gateway | 53 (DNS), 80 (HTTP), 443 (HTTPS) | 23 (Telnet) is **filtered**; 996 ports closed |
| 192.168.1.2 | Client device | none | All 1000 ports closed |
| 192.168.1.4 | Client device | none | All 1000 ports closed |
| 192.168.1.5 | Windows PC (scanning machine) | 135 (MSRPC), 139 (NetBIOS), 445 (SMB) | Standard Windows file-sharing services |

### Observations
- The router exposes DNS and a web interface over HTTP and HTTPS.
- Telnet on the router is filtered, so a firewall rule is blocking the insecure protocol.
- Two devices expose no services at all, a good minimal attack surface.
- The Windows host runs SMB and NetBIOS, which are common targets and worth restricting on untrusted networks.

### Recommendations
- Serve the router admin page over HTTPS only and disable remote administration.
- Keep Telnet disabled on all devices; use SSH if remote access is needed.
- Turn off NetBIOS/SMB or limit it with the Windows firewall when file sharing isn't needed.
- Re-scan after changes to confirm the exposure shrank.

### Conclusion
The SYN scan found all active hosts and their open services. The network has a small attack surface overall, with the router's web interface and the Windows file-sharing ports as the main items to review.

> Scans were run only on my own home network. Only scan networks you own or have written permission to test.
