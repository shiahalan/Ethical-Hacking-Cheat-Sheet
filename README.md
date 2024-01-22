# Ethical Hacking Cheat Sheet
A cheat sheet for ethical hacking made by Alan Shiah.

## Enumeration 🌐
### Network Enumeration
#### Ping: Does an ICMP echo to target IP to checks if target is up. Also provides TTL (Time to live) info, revealing OS information.
```
ping <target_ip>
```
#### nmap: Network mapper. Can be used to enumerate a target's ports and much more.
```
nmap <target_ip>
``` 
##### -=Flags=-
-sV = Service Scan,
-sS = SYN Scan,
-sA = ACK Scan,
-sT = TCP Scan,
-sU = UDP Scan (some services run on UDP connections),
-sC = Run Default Scripts,
-Pn = Don't send ping probes,
-p = Port (-p- scans all ports),
-T = Speed, 1-5 with 5 being the fastest (3 is default),
--source-port <port> = Send requests from this port (some firewalls block all traffic except for whitelisted ports, try port 53),
--scripts <name/category> = Execute a specific script or scripts from a certain category


