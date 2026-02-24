# Findings

## Nmap Service Scan Summary (10.0.0.200)
Command:
- nmap -sV 10.0.0.200

Key results:
- Host up with low latency (~7 ms) → local network.
- 996 closed TCP ports (RST) → typical.
- Open:
  - 3306/tcp: MySQL (unauthorized)
  - 5000/tcp: RTSP / AirTunes rtspd 775.3.1
  - 7000/tcp: RTSP / AirTunes rtspd 775.3.1
- Filtered:
  - 5432/tcp: PostgreSQL (filtered)
- MAC vendor: Apple

Interpretation:
- MySQL is reachable on the network but requires auth (“unauthorized”).
- AirTunes/RTSP ports are consistent with AirPlay-related services.
- “filtered” suggests firewalling or packet dropping for 5432 (uncertain service presence).

## Expected Packet-Level Artifacts (tcpdump/Wireshark)
During scanning, you should observe:
- bursts of TCP SYN packets from Kali → target on many ports
- predictable patterns in destination ports
- responses:
  - SYN/ACK for open ports
  - RST for closed ports
  - no response (or ICMP unreachable) for filtered behavior, depending on device and network controls
