# Methodology

## Environment
- Attacker: Kali Linux
- Target: 10.0.0.200 (Apple host identified by Nmap MAC vendor)
- Tools: nmap, tcpdump (optional Wireshark for analysis)

## Step 0 — Identify interfaces (target or sensor host)
Command:
- ip a
Goal:
- find active interface name (e.g., eth0, en0, wlan0)

## Step 1 — Baseline capture (no scanning)
On sensor/target host:
- sudo tcpdump -i <iface> -nn -w labs/lab-01-network-observation/pcaps/baseline.pcap

Capture ~2–3 minutes of normal traffic, then stop with Ctrl+C.

## Step 2 — Generate controlled recon traffic from Kali
On Kali:
- nmap -sV 10.0.0.200
Optional extra recon:
- nmap -sn 10.0.0.0/24
- nmap -sS -p- 10.0.0.200

## Step 3 — Capture scan traffic
On sensor/target host:
- sudo tcpdump -i <iface> -nn -w labs/lab-01-network-observation/pcaps/scan_activity.pcap

Run scans while tcpdump is capturing, then Ctrl+C.

## Step 4 — Quick validation checks
- sudo tcpdump -nn -r <pcap> | head
or open in Wireshark:
- look for TCP SYN patterns, repeated port attempts, and timing regularity.
