# ELEVATE-LABS-PROJECTS
Task Title:
Network Scanning using Nmap

Objective:
To perform network scanning on a local network using Nmap and identify open ports, services, and host availability.

Tools Used:
Nmap 7.98
Windows OS
Local Network (192.168.1.0/24)

Command Used:
nmap -sS 192.168.1.0/24

Scan Summary:
Host: 192.168.1.1
Host is up

Open Ports:
53/tcp → DNS (domain)
80/tcp → HTTP
443/tcp → HTTPS
Filtered Port:
23/tcp → Telnet
996 ports closed

🔎 Host: 192.168.1.2
*Host is up
*All 1000 scanned ports are closed

Host: 192.168.1.4
* Host is up
*All 1000 scanned ports are closed

Observations:
*The main router (192.168.1.1) has active web services (HTTP/HTTPS).
*Telnet port is filtered, indicating firewall protection.
*Other devices in the network have no open ports.
*Most ports are closed, indicating limited exposure.

Conclusion:
*The Nmap scan successfully identified active hosts and open p
