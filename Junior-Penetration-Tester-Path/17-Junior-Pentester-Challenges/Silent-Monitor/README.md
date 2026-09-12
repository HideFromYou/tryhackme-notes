# TryHackMe - Silent Monitor

## Overview

This room focused on chaining multiple vulnerabilities to move from an exposed web application to user access and eventually obtain the root flag.

My attack path was:

1. Port and service enumeration
2. Web directory enumeration
3. SQL Injection authentication bypass
4. Command Injection → RCE
5. Credential discovery
6. KeePass database discovery
7. KeePass password cracking
8. Credential reuse
9. Root access and flag collection

The main vulnerabilities I encountered were **SQL Injection** and **Command Injection**, followed by the recovery of credentials from a KeePass database.

---

## 1. Reconnaissance

I started by scanning all TCP ports to identify the available services and their versions.

```bash
nmap -sS -sV -T4 -p- [target_ip]
```

The scan revealed a web service running on port `5050`, so I moved on to web enumeration.

---

## 2. Web Enumeration

I used GoBuster to enumerate directories on the web server.

```bash
gobuster dir -u [target_ip]:5050 -w /usr/share/wordlists/dirb/common.txt
```

This revealed an internal login page at:

```text
/internal
```

I then focused on testing the authentication mechanism.

---

## 3. SQL Injection Authentication Bypass

The login form was vulnerable to SQL Injection.

I tested the following payload:

```text
' OR 1=1 -- -
```

The payload altered the SQL query logic and allowed me to bypass the authentication mechanism.

This confirmed that user-controlled input was being incorporated into a SQL query without proper parameterization.

### Finding

**SQL Injection**

The application should have used parameterized queries or prepared statements instead of directly inserting user input into SQL statements.

---

## 4. Command Injection → RCE

After logging in, I found a connectivity probe tool.

I intercepted the request using Burp Suite and tested whether I could manipulate the command executed by the application.

I used:

```text
10.0.0.1%0als
```

The `%0a` represented a newline character and allowed me to inject an additional command.

The `ls` command executed successfully, confirming that I had achieved command execution on the server.

### Finding

**Command Injection / Remote Code Execution**

The application was passing user-controlled input into an operating system command without properly preventing command injection.

---

## 5. Credential Discovery

With command execution available, I started enumerating the filesystem.

Running `ls` exposed:

```text
secret.config
```

I inspected the file and found a password for a backup agent named:

```text
sysadmin
```

The credentials allowed me to access the `sysadmin` user's environment.

I then found the user flag in:

```text
/home/sysadmin/user.txt
```

The flag was:

```text
THM{sQli_4nd_cMd_1nj3ct10n_l3D_y0u_h3re!}
```

At this point, the initial web vulnerabilities had successfully led to local user access.

---

## 6. Discovering the KeePass Database

While continuing to enumerate the system, I found a `backups` directory containing a KeePass database:

```text
infrastructure.kdbx
```

I transferred the database to my attacking machine so I could perform an offline password-cracking attack.

The important part here was that I did not need to attack the KeePass application itself. Once I obtained the database file, I could work against its password hash offline.

---

## 7. Cracking the KeePass Password

I first converted the KeePass database into a format that John the Ripper could process:

```bash
keepass2john infrastructure.kdbx > hash.txt
```

I then used the `rockyou.txt` wordlist:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

The KeePass master password was successfully recovered:

```text
spring
```

I could then open the password database and inspect the stored credentials.

---

## 8. Recovering Administrator Credentials

Inside the KeePass database, I found an administrator username and password.

I used those credentials to authenticate as the administrator and obtain root-level access.

The root flag was:

```text
THM{KDBx_V4ul7_H4s_b33n_cr4ck3d_0peN}
```

---

## 9. Attack Chain

The complete attack chain was:

```text
Port Scan
    ↓
Web Enumeration
    ↓
/internal Login
    ↓
SQL Injection
    ↓
Authentication Bypass
    ↓
Connectivity Probe
    ↓
Command Injection
    ↓
Remote Code Execution
    ↓
secret.config
    ↓
sysadmin Credentials
    ↓
User Flag
    ↓
backups/
    ↓
infrastructure.kdbx
    ↓
keepass2john
    ↓
John the Ripper
    ↓
KeePass Password: spring
    ↓
Administrator Credentials
    ↓
Root Access
    ↓
Root Flag
```

---

## Key Findings

### SQL Injection

The login functionality was vulnerable to SQL Injection, allowing authentication to be bypassed.

```text
' OR 1=1 -- -
```

**Impact:** Unauthorized access to the internal application.

---

### Command Injection

The connectivity probe accepted user-controlled input that was passed to a system command.

```text
10.0.0.1%0als
```

**Impact:** Arbitrary command execution on the server.

---

### Sensitive Credential Storage

Credentials were stored in a configuration file accessible after obtaining command execution.

```text
secret.config
```

**Impact:** Credentials could be recovered and used to access another local account.

---

### Exposed KeePass Database

A KeePass database was stored inside the backups directory.

```text
infrastructure.kdbx
```

Once obtained, it could be attacked offline.

**Impact:** Recovery of the KeePass master password exposed additional privileged credentials.

---

### Weak KeePass Password

The KeePass master password was successfully cracked using a common password wordlist:

```text
spring
```

This demonstrated the importance of using strong, unique master passwords for password managers.

---

## What I Learned

The main lesson from this room was how several different weaknesses can be chained together to achieve full compromise.

The SQL Injection gave me access to the internal application, while the Command Injection turned that application access into arbitrary command execution. From there, basic filesystem enumeration exposed credentials that led to a local user.

The KeePass database then provided another escalation path. Instead of trying to attack the administrator account directly, I obtained the password database and performed an offline cracking attack against its master password.

This room reinforced the importance of thinking about the **entire attack chain** rather than treating each vulnerability as an isolated issue.

```text
SQL Injection
      ↓
Application Access
      ↓
Command Injection / RCE
      ↓
Credential Discovery
      ↓
Local User Access
      ↓
KeePass Database
      ↓
Offline Password Cracking
      ↓
Administrator Credentials
      ↓
Root Access
```

## Final Flags

### User Flag

```text
THM{sQli_4nd_cMd_1nj3ct10n_l3D_y0u_h3re!}
```

### Root Flag

```text
THM{KDBx_V4ul7_H4s_b33n_cr4ck3d_0peN}
```