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

## Analytical reflection

Distinguishing Baseline Traffic from Scan Traffic

Baseline traffic appeared sporadic and conversational, consisting primarily of DNS queries,
ARP broadcasts, and occasional established connections with relatively consistent timing between packets. 
The packet flow showed normal client-server behavior with completed TCP handshakes and predictable
protocol use.

In contrast, the scan traffic exhibited a burst-like pattern with rapid
succession of TCP SYN packets originating from a single source and targeting many
destination ports on the host. The port distribution was wide and sequential,
and many connection attempts did not complete full TCP handshakes. 
This created a noticeably higher packet rate and a repetitive structure that clearly differed from
normal background traffic.

Observational Surprise

One surprising aspect was how mechanically patterned the scan appeared on the wire.
Rather than looking chaotic, the traffic was highly structured, with evenly spaced SYN packets
probing ports in a predictable sequence.
This made the scan visually distinct in packet capture analysis and highlighted how
reconnaissance activity can be detected through timing and repetition rather than payload content alone.

Experimental Limitation

This experiment was limited by its narrow scope, as it involved only a single
target host within a small local network and a short capture duration.
The lack of diverse network activity reduced background noise,
making scan patterns easier to identify than they would be in a real enterprise environment.
Additionally, encrypted traffic was not analyzed, which limits visibility into application-layer behavior
and reduces the realism of the dataset.
