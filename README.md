# Ethical Hacking Cheat Sheet
A cheat sheet for ethical hacking.

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
```
nmap -sV <target_ip>
```
```
nmap -p- <target_ip>
```
```
nmap -sU <target_ip>
```
```
nmap -sT <target_ip>
```
```
nmap -sS <target_ip>
```
```
nmap -sA <target_ip>
```
```
nmap --source-port=<port> <target_ip>
```
