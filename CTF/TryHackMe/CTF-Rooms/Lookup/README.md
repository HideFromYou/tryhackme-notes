# Lookup

## Overview

This room was mainly about enumeration, identifying valid usernames, password brute-forcing, exploiting a vulnerable web application, and Linux privilege escalation.

The main attack chain was:

Enumeration
  ↓
Valid username discovery
  ↓
Password brute-force
  ↓
SSH / Web access as jose
  ↓
Subdomain discovery
  ↓
elFinder enumeration
  ↓
Metasploit exploit
  ↓
www-data
  ↓
SUID enumeration
  ↓
/usr/sbin/pwm
  ↓
PATH Hijacking
  ↓
Read /home/think/.passwords
  ↓
Password brute-force
  ↓
SSH as think
  ↓
sudo -l
  ↓
/usr/bin/look
  ↓
Read root SSH private key
  ↓
SSH as root

---

## 1. Initial Enumeration

I started with port enumeration.

RustScan identified two interesting open ports:

- `22` → SSH
- `80` → HTTP

I also used Nmap to confirm the services and versions.

I searched for known CVEs related to the SSH and HTTP versions, but nothing useful came up.

I also tried additional enumeration such as:

- Subdomain enumeration
- Nikto
- Directory enumeration

The initial results were not particularly useful.

---

## 2. Web Application

After adding the hostname to `/etc/hosts`:

    lookup.thm

I accessed the website and found a login page.

I tested:

- Default credentials
- Basic SQL injection attempts

These did not work.

However, I noticed something important during the login attempts.

The application returned different responses depending on the username.

This suggested that the application was validating whether a username existed.

For example, an invalid username produced a response different from an existing username.

I confirmed that:

    admin

was a valid username.

---

## 3. Username Enumeration

Brute-forcing the password for `admin` with Hydra was not productive.

Instead, I focused on the username validation behavior.

I created a Python script to automate testing a large username wordlist.

The idea was:

    username from wordlist
        ↓
    POST request to /login.php
        ↓
    fixed password
        ↓
    inspect response
        ↓
    "Wrong password" → valid username
    "wrong username" → invalid username

The script used:

    requests.post()

against:

    http://lookup.thm/login.php

The important part was the response comparison.

If the response contained:

    Wrong password

I treated the username as valid.

The script eventually identified:

    jose

as another valid username.

### Key Takeaway

Different responses from a login form can sometimes allow **username enumeration**.

Instead of manually testing thousands of usernames, automation can make this process much faster.

---

## 4. Password Brute-Force

Once I had a valid username, I moved to password discovery.

For `jose`, I used Hydra with `rockyou.txt`:

    hydra -l jose -P /usr/share/wordlists/rockyou.txt lookup.thm http-post-form "/login.php:username=^USER^&password=^PASS^:INcorrect" -V

The important idea was:

    Known username
        +
    Password wordlist
        ↓
    Hydra
        ↓
    Test login requests
        ↓
    Identify valid password

After obtaining the correct password, I was able to continue as `jose`.

---

## 5. Subdomain Discovery

After logging in as `jose`, I discovered another subdomain.

I added the discovered hostname to `/etc/hosts` so that it could be accessed.

The new application exposed a file manager.

---

## 6. elFinder Enumeration

I identified the file manager as:

    elFinder

I checked its version and found:

    elFinder 2.1.47

This was interesting because this version is vulnerable to:

    CVE-2019-9194

I searched for available exploits using Searchsploit.

The relevant exploit was:

    elFinder 2.1.47 - 'PHP connector' Command Injection

Searchsploit:

    searchsploit elFinder 2.1.47

I also used:

    searchsploit -m 46481.py

to copy the exploit locally.

---

## 7. Metasploit Exploitation

Instead of running the Python exploit manually, I used Metasploit.

I started:

    msfconsole

Then selected:

    exploit/unix/webapp/elfinder_php_connector_exiftran_cmd_injection

After configuring the target, the exploit successfully provided a shell.

The resulting shell was running as:

    www-data

### Key Takeaway

The important reasoning here was:

    Identify application
        ↓
    Identify exact version
        ↓
    Search for known vulnerabilities
        ↓
    Find matching exploit
        ↓
    Use Metasploit
        ↓
    Initial shell as www-data

---

## 8. SUID Enumeration

Once I had a shell as `www-data`, I started looking for privilege escalation opportunities.

I searched for SUID binaries:

    find / -perm -u=s -type f 2>/dev/null

This revealed an interesting binary:

    /usr/sbin/pwm

The name alone was not enough to conclude that it was exploitable.

I investigated it further.

---

## 9. Investigating /usr/sbin/pwm

I checked the binary with:

    strings /usr/sbin/pwm

Among the interesting strings were:

    id

and:

    /home/%s/.passwords

This was a major clue.

The binary was executing the `id` command and using the username obtained from it to construct a path.

Conceptually:

    id
    ↓
    username
    ↓
    /home/%s/.passwords

Because `pwm` was a SUID binary, it was running with elevated privileges.

---

## 10. Understanding the PATH Hijacking

The important discovery was that the binary executed:

    id

without using an absolute path such as:

    /usr/bin/id

This meant the command would be searched for using the current `$PATH`.

I created my own fake `id` executable:

    /tmp/id

The fake `id` returned:

    uid=33(think) gid=33(think) groups=(think)

I then placed `/tmp` first in the `$PATH`:

    export PATH=/tmp:$PATH

The important concept is that `$PATH` is searched from left to right.

For example:

    PATH=/tmp:/usr/bin:/bin

When the program executes:

    id

the system checks:

    /tmp/id
    ↓
    /usr/bin/id
    ↓
    /bin/id

Since `/tmp/id` exists, it is executed first.

Therefore:

    pwm
      ↓
    popen("id")
      ↓
    PATH lookup
      ↓
    /tmp/id
      ↓
    fake output: think

---

## 11. Why `think` Was Important

The fake `id` returned the username:

    think

This caused `pwm` to construct:

    /home/think/.passwords

The reason this mattered was that the `www-data` user could not normally read the file.

However, `pwm` was a SUID binary, so it executed with elevated privileges and could access the file.

The resulting password list was printed by `pwm`.

### Important Concept

The attack was not about executing `.passwords`.

We were making the binary **read**:

    /home/think/.passwords

by controlling the username returned by the `id` command.

---

## 12. Password List

The output from:

    /usr/sbin/pwm

gave us a list of possible passwords for `think`.

I copied the list to my AttackBox and saved it as:

    passwords.txt

I then used Hydra against SSH:

    hydra -l think -P passwords.txt -t 4 ssh://<TARGET_IP>

The important difference from the earlier brute-force was that this was a **target-specific password list** obtained from the target itself.

---

## 13. SSH as think

After Hydra identified the correct password, I connected through SSH as:

    think

At this point I had moved from:

    www-data

to:

    think

---

## 14. sudo -l

As `think`, I checked which commands I could execute with elevated privileges:

    sudo -l

The result showed:

    (ALL) /usr/bin/look

This meant that `think` could execute `look` through `sudo` with root privileges.

---

## 15. Using `look` for File Reading

The interesting part about `look` was not that it was SUID.

It was allowed through:

    sudo

Therefore:

    think
      ↓
    sudo look
      ↓
    look runs as root
      ↓
    can read root-only files

I used this to read:

    /root/.ssh/id_rsa

This is the private SSH key belonging to root.

---

## 16. Root SSH Access

I saved the private key locally as:

    id_rsa

Then I restricted its permissions:

    chmod 600 id_rsa

`600` means:

    owner → read + write
    group → no permissions
    others → no permissions

I then used the private key to authenticate as root:

    ssh -i id_rsa root@<TARGET_IP>

This gave me:

    root

The root flag was then accessible.

---

## 17. Complete Attack Chain

    Port Enumeration
        ↓
    22 SSH / 80 HTTP
        ↓
    Login Page
        ↓
    Username Enumeration
        ↓
    Valid username: jose
        ↓
    Hydra
        ↓
    Login as jose
        ↓
    Discover subdomain
        ↓
    elFinder 2.1.47
        ↓
    CVE-2019-9194
        ↓
    Metasploit
        ↓
    www-data
        ↓
    SUID Enumeration
        ↓
    /usr/sbin/pwm
        ↓
    strings
        ↓
    id + /home/%s/.passwords
        ↓
    PATH Hijacking
        ↓
    Fake /tmp/id
        ↓
    pwm reads /home/think/.passwords
        ↓
    Hydra
        ↓
    SSH as think
        ↓
    sudo -l
        ↓
    /usr/bin/look
        ↓
    Read /root/.ssh/id_rsa
        ↓
    chmod 600
        ↓
    SSH as root
        ↓
    Root

---

## Key Takeaways

### Username Enumeration

If a login application returns different responses for valid and invalid usernames, this can be used to enumerate users.

### Automation

A small Python script can automate thousands of username checks instead of testing them manually.

### PATH Hijacking

If a privileged binary executes a command using only its name:

    popen("id")

instead of an absolute path:

    popen("/usr/bin/id")

I should immediately consider whether `$PATH` can be manipulated.

### SUID + PATH Hijacking

The dangerous combination was:

    SUID binary
        +
    command executed without absolute path
        +
    controllable PATH
        =
    potential privilege escalation

### sudo -l

After obtaining a new user, always check:

    sudo -l

It tells me which commands that user can execute with elevated privileges.

### SSH Private Keys

If I can read:

    /root/.ssh/id_rsa

I may be able to authenticate directly as root, provided SSH access is available and the key is valid.

---

## Tools Used

- RustScan
- Nmap
- Gobuster / directory enumeration
- Python
- Hydra
- Searchsploit
- Metasploit
- strings
- Linux `find`
- SSH
- sudo
- look