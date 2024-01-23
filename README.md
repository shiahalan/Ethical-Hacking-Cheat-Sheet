# Ethical Hacking Cheat Sheet
A cheat sheet for ethical hacking created by Alan Shiah.


![9d9bd13afce1a798d22ecfd9897730ed](https://github.com/shiahalan/Ethical-Hacking-Cheat-Sheet/assets/102575877/ce271435-83a5-492f-b7d2-394d1a33d1f1)
## OSINT (Open-Source Intelligence) 🔎

## Linux Commands 📜
#### sudo: Run the following command as a super-user.
```
sudo <command>
```
##### -=Switch To Root=-
```
sudo su
```

#### su: Used to switch users.
```
su <username>
```

#### ls: Used to list out directories.
```
ls <optional, /path>
```
##### -=Flags=-
-l = Long List Formatting (show more information),
-a = All (list all files/directories, including hidden ones)

#### pwd: Used to print the working directory.
```
pwd
```

#### cd: Used to change directories.
```
cd <directory name, /path>
```

#### mkdir: Used to make a new directory.
```
mkdir <name>
```

#### mv: Used to either move a file/directory or rename a file.
```
mv <filename/directory name> </path>
```
```
mv <filename> <new filename>
```

#### cp: Used to copy a file to another file/destination.
```
cp <filename> <destination file name>
```
```
cp <filename> <directory name>
```

#### rm: Used to remove files or directories.
```
rm <filename>
```
```
rm -r <directory name>
```
##### -=Flags=-
-r = recursive (deletes a directory and all files/directories inside)

#### touch: Creates a blank empty file.
```
touch <filename>
```

#### cat: Displays the contents of a file onto the terminal output.
```
cat <filename>
```

#### clear: Clears the terminal display.
```
clear
```

#### echo: Prints out any text following the command.
```
echo <text>
```

#### man: Used to access the manual for a certain command.
```
man <command name>
```

#### whoami: Outputs the username of the active user. Beware, as this command is usually marked as suspicious to IDS/IPS.
```
whoami
```

#### zip: Used to zip and compress a file.
```
zip <filename>
```

#### unzip: Used to unzip and extract .zip files.
```
unzip <filename>
```

#### grep: Used to search for a specified string.
```
grep <string>
```
```
grep <string> <filename>
```
##### -=Flags=-
-r = Recursive (looks through all directories and files starting from current directory), -f File (lists out files containing the string)

#### chmod: Used to change file permissions for a specified file.
```
chmod <flags> <filename>
```
##### -=Flags=-
-x = Not Executable, -r = Not Readable, -w = Not Writable, +x = Executable, +r Readable, +w Writable, 600 = (No one else can access the file except owner, use on RSA keys when SSH)

#### wget: Used to directly download files from the internet.
```
wget <url>
```

#### scp: Also known as secure copy, is used to copy files securely between servers.
```
scp <user@host>:</path> </destination path>
```
```
scp <user1@host1>:</path> <user2@host2>:</destination path>
```

#### file: Checks a file's type and lists relevant file content information.
```
file <filename>
```

#### nano: Opens a basic terminal based text editor that can be used to edit files.
```
nano <filename>
```

#### find: Outputs the location of a specified file/directory.
```
find <filename/directory name>
```

#### |: Also known as pipe, this command takes the output of one command and then puts it into the input of another.
```
<first command> | <second command>
```


## Windows Commands 📜

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
##### -=Convert Output To String=-
```
require('fs').readFileSync('</path>').toString();
```
```
new String(require('fs').readFileSync('</path>'));
```
