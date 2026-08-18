# Team - THM

## Overview

**Type:** Web CTF  
**Difficulty:** Medium  
**Target:** `team.thm`

This room focuses on web enumeration, information disclosure, Local File Inclusion (LFI), SSH key extraction, lateral movement, and Linux privilege escalation.

---

## Attack Path

```text
Nmap
  ↓
HTTP Enumeration
  ↓
Virtual Host Discovery
  ↓
Gobuster
  ↓
robots.txt
  ↓
Information Disclosure
  ↓
FTP Credentials
  ↓
FTP Enumeration
  ↓
Virtual Host: dev.team.thm
  ↓
LFI
  ↓
SSH Private Key
  ↓
SSH Access as dale
  ↓
Lateral Movement to gyles
  ↓
Writable Backup Script
  ↓
Reverse Shell
  ↓
Root


1. Enumeration

Start with Nmap service enumeration:

nmap -sV <TARGET_IP>

The scan reveals:

21/tcp  FTP
22/tcp  SSH
80/tcp  HTTP

The HTTP service on port 80 is the first target.

2. Web Enumeration

Access the web server:

http://<TARGET_IP>

The page does not reveal much information.

Inspect the source code.

The source contains a reference to:

team.thm

Add the hostname to /etc/hosts:

sudo nano /etc/hosts

Add:

<TARGET_IP> team.thm

Then access:

http://team.thm
3. Directory Enumeration

Use Gobuster:

gobuster dir -u http://team.thm -w <WORDLIST>

Interesting results include:

index.html
robots.txt
scripts
4. robots.txt

Inspect:

http://team.thm/robots.txt

A possible username is discovered:

dale

This becomes useful later during authentication.

5. Enumerating /scripts

The /scripts directory itself is forbidden.

Enumerate files using Gobuster with .txt:

gobuster dir -u http://team.thm/scripts/ -w <WORDLIST> -x txt

A file named:

script.txt

is discovered.

Inspect it:

http://team.thm/scripts/script.txt

The note contains information indicating that an older version of the file may be available.

Changing:

script.txt

to:

script.old

results in the file being downloaded.

The file contains credentials that can be used to access FTP.

6. FTP Enumeration

Connect to FTP:

ftp <TARGET_IP>

Use the discovered credentials.

After authentication, enumerate the available files.

A directory named:

workshare

is discovered.

Enter the directory and identify:

New_site.txt

Download it:

mget New_site.txt
7. New_site.txt

The file contains information pointing towards:

.dev

Add the new virtual host to /etc/hosts:

<TARGET_IP> dev.team.thm

Then access:

http://dev.team.thm

The page contains a link using a PHP file parameter.

The parameter can be tested for Local File Inclusion.

8. Local File Inclusion

The application is vulnerable to LFI.

The vulnerable parameter allows local files to be included.

The goal is to read SSH configuration information.

A useful target is:

/etc/ssh/sshd_config

Example:

http://dev.team.thm/?page=/etc/ssh/sshd_config

The SSH configuration reveals information including an SSH private key.

9. SSH Private Key

Copy the discovered private key into a local file:

nano id_rsa

Save the key as:

id_rsa

Remove the # characters that were present as comments in the extracted content where necessary.

Set the correct permissions:

chmod 600 id_rsa

Connect using SSH:

ssh -i id_rsa dale@<TARGET_IP>
10. User Flag

After obtaining SSH access as dale, retrieve the user flag.

THM{6Y0TXHz7c2d}
11. Privilege Escalation / Lateral Movement

Enumerate the system and users.

Another user is identified:

gyles

Check sudo privileges:

sudo -l

The interesting executable is:

/home/gyles/admin_checks

The script can be executed in the context of gyles.

12. Command Injection

Inspect the script:

cat /home/gyles/admin_checks

The script contains several locations where user-controlled input can be interpreted as a system command.

The vulnerable input can therefore be used for command injection.

Execute the script in the context of gyles:

sudo -u gyles /home/gyles/admin_checks

Supply an appropriate error/input value containing a command.

Successful exploitation provides a shell as:

gyles
13. Enumerating gyles

Inspect the home directory:

ls -la /home/gyles

A .bash_history file is available.

Read it:

cat /home/gyles/.bash_history

The history reveals:

main.backup.sh

This script becomes the next privilege-escalation target.

14. Writable Backup Script

Inspect the permissions:

ls -la main.backup.sh

The gyles user belongs to the admin group and has permission to modify and execute the script.

This creates a path to privilege escalation.

15. Root Privilege Escalation

Open the script:

vim main.backup.sh

Modify the script to execute a reverse shell.

Start a listener on the attacker machine:

nc -lvnp 4444

When the backup script is executed with elevated privileges, the reverse shell connects back to the listener.

This provides a root shell.

16. Root Flag

Once root access is obtained, retrieve the root flag:

THM{fhqbznavfonq}
Credentials / Findings
Item	Value
Initial User	dale
Second User	gyles
Initial Access	SSH
Web Vulnerability	LFI
Lateral Movement	Command Injection
Privilege Escalation	Writable backup script
User Flag	THM{6Y0TXHz7c2d}
Root Flag	THM{fhqbznavfonq}
Vulnerabilities Identified
Information Disclosure

robots.txt exposes a potential username.

Sensitive File Exposure

An old script version exposes credentials.

Local File Inclusion

The dev.team.thm application allows local files to be included.

SSH Key Exposure

The SSH configuration response exposes a private key.

Command Injection

The admin_checks script allows attacker-controlled input to reach command execution.

Insecure File Permissions

The main.backup.sh script is writable by a user who can leverage it for privilege escalation.

Attack Chain Summary
21/22/80 Enumeration
        ↓
team.thm
        ↓
robots.txt
        ↓
User: dale
        ↓
/scripts/script.txt
        ↓
script.old
        ↓
FTP Credentials
        ↓
FTP /workshare
        ↓
New_site.txt
        ↓
dev.team.thm
        ↓
LFI
        ↓
/etc/ssh/sshd_config
        ↓
SSH Private Key
        ↓
SSH as dale
        ↓
admin_checks
        ↓
Command Injection
        ↓
gyles
        ↓
.bash_history
        ↓
main.backup.sh
        ↓
Writable Script
        ↓
Reverse Shell
        ↓
ROOT
Key Takeaways
Always perform complete service enumeration.
Inspect source code when the web page appears empty.
robots.txt can disclose useful information.
Enumerate directories and files, not only directories.
Old or backup files can expose sensitive credentials.
FTP can contain information that leads to another virtual host.
Test application parameters for LFI when local file inclusion is suspected.
SSH configuration files can reveal useful authentication information.
After initial access, enumerate users, groups, permissions, history files, and scripts.
Writable scripts executed with higher privileges are a common privilege-escalation path.
Always connect individual findings into a complete attack chain.