# Concepts

## Packets vs Flows vs Logs
- Packets: raw network units (e.g., TCP SYN, DNS query).
- Flows: summaries of conversations (5-tuple: src IP, dst IP, src port, dst port, protocol).
- Logs: interpreted/recorded events from systems or sensors (e.g., "connection allowed", "process created").

## Port States (Nmap)
- open: service is reachable and responded.
- closed: no service; host responded with reset/refusal.
- filtered: a firewall/ACL dropped or blocked probes; uncertain if service exists.

## Why Baselines Matter
You can’t spot anomalies if you don’t know what's normal for the environment.
