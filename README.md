# Ethical Hacking Cheat Sheet
A cheat sheet for ethical hacking made by Alan Shiah.


![9d9bd13afce1a798d22ecfd9897730ed](https://github.com/shiahalan/Ethical-Hacking-Cheat-Sheet/assets/102575877/ce271435-83a5-492f-b7d2-394d1a33d1f1)
## Enumeration 🌐
### Network Enumeration
#### Ping: Does an ICMP echo to target IP to checks if target is up. Also provides TTL (Time to live) info, revealing OS information.
```
ping <target_ip>
```
##### -=TTL=-
ttl 64 = Linux, ttl 128 = Windows, ttl 255 = Network device
#### nmap: Network mapper. Can be used to enumerate a target's ports and much more. By default, it scans the top 1000 most common ports.
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
-F = Top 100 ports,
--source-port <port> = Send requests from this port (some firewalls block all traffic except for whitelisted ports, try port 53),
--scripts <name/category> = Execute a specific script or scripts from a certain category
### Port Enumeration
#### Port 21: FTP
FTP or File Transfer Protocol is commonly hosted on port 21. It allows the transfer of computer files following a client to server model.
```
ftp <target IP>
```
##### -=Anonymous Login=-
You may login to ftp using a guest account without a password under the username anonymous. anonymous:NONE

## Miscellaneous 🛠️
### JavaScript and Node.JS
#### Read Local Files
```
require('fs').readFileSync('</path>');
```
##### Convert output to string
```
require('fs').readFileSync('</path>').toString();
```
```
new String(require('fs').readFileSync('</path>'));
```
