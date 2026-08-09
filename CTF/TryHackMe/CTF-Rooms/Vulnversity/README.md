# Vulnversity

## Objective

The objective of the room is to compromise the Vulnversity web server, obtain the user flag, and escalate privileges to root to retrieve the final flag.

---

# 1. Reconnaissance

Started with an Nmap scan:

```bash
nmap -sV -A -Pn -v <IP>
```

### Important Flags

- `-sV` — Service/version detection
- `-A` — Aggressive scan, including OS/version detection and default scripts
- `-Pn` — Disable host discovery and scan the target directly
- `-v` — Verbose output

### Results

The scan identified:

```text
6 open ports
```

The Squid proxy was running:

```text
3.5.12
```

The Squid proxy was identified on:

```text
3128/tcp
```

The most likely operating system was:

```text
Ubuntu
```

The web server was running on:

```text
3333/tcp
```

The web service was therefore accessed through:

```text
http://<IP>:3333
```

---

# 2. Nmap Questions / Findings

### How many ports are open?

```text
6
```

### What version of Squid is running?

```text
3.5.12
```

### What does `-p-400` scan?

```text
400 ports
```

### What does `-n` prevent Nmap from resolving?

```text
DNS
```

### Most likely operating system?

```text
Ubuntu
```

### Web server port?

```text
3333
```

---

# 3. Directory Enumeration

After identifying the web server, Gobuster was used to enumerate directories.

Example:

```bash
gobuster dir -u http://<IP>:<PORT> -w <wordlist.txt>
```

An interesting directory was discovered:

```text
/internal/
```

This directory contained an upload form.

---

# 4. Web Server Enumeration

The discovered upload functionality was accessed through:

```text
http://<IP>:3333/internal
```

Burp Suite was used to proxy the connection and inspect the upload functionality.

The application allowed files to be uploaded to the server.

---

# 5. File Upload Restriction

Different file extensions were tested against the upload form.

The following extension was blocked:

```text
.php
```

An alternative PHP extension was tested.

The following extension was accepted:

```text
.phtml
```

This provided a way to upload PHP code despite the `.php` restriction.

---

# 6. Initial Access

A PHP reverse shell was uploaded using the allowed `.phtml` extension.

A Netcat listener was started on the attacking machine.

Once the uploaded reverse shell was executed, a reverse shell connection was received.

The attack chain was:

```text
Web Server
    ↓
/internal/
    ↓
Upload Form
    ↓
.php blocked
    ↓
.phtml allowed
    ↓
PHP Reverse Shell
    ↓
Shell Access
```

---

# 7. User Enumeration

After obtaining a shell, the user managing the web server was identified as:

```text
bill
```

The user flag was then retrieved from the user's environment.

### User Flag

```text
8bd7992fbe8a6ad22a63361004cfcedb
```

---

# 8. Privilege Escalation

The next objective was to obtain root privileges.

The system was searched for SUID binaries using:

```bash
find / -user root -perm -4000 -exec ls -ldb {} \;
```

The command searches for files:

- Owned by `root`
- With the SUID permission set

Several standard SUID binaries were identified, including:

```text
/bin/mount
/bin/ping
```

However, one unusual binary stood out:

```text
/bin/systemctl
```

---

# 9. Identifying systemctl as the Escalation Vector

`systemctl` is used to examine and control the `systemd` system and service manager.

Normally, having the SUID bit set on `systemctl` would be highly unusual.

The binary was therefore investigated as a potential privilege escalation vector.

GTFOBins was used to research known abuse techniques for `systemctl`.

---

# 10. systemctl Privilege Escalation

The escalation technique involved creating a temporary systemd service unit.

First, an environment variable was created containing a temporary file path.

The temporary service was configured to execute a command as root.

The service was designed to read:

```text
/root/root.txt
```

and redirect its contents to:

```text
/tmp/output
```

The general concept was:

```text
SUID systemctl
      ↓
Create systemd service
      ↓
Service executes with elevated privileges
      ↓
Read /root/root.txt
      ↓
Write output to /tmp/output
      ↓
Read flag
```

A symbolic link was then created so that the service unit could be accessed by `systemctl`.

The service was enabled and started.

The resulting output became available in:

```text
/tmp/output
```

The root flag could then be read from the output file.

---

# 11. Root Flag

The final flag obtained through the `systemctl` privilege escalation was:

```text
a58ff8579f0a9270368d33a9966c7fd5
```

---

# Tools Used

- Nmap
- Gobuster
- Burp Suite
- Netcat
- GTFOBins
- systemctl

---

# Attack Chain

```text
Nmap
  ↓
6 Open Ports
  ↓
Web Server :3333
  ↓
Gobuster
  ↓
/internal/
  ↓
File Upload
  ↓
.php Blocked
  ↓
.phtml Allowed
  ↓
PHP Reverse Shell
  ↓
bill
  ↓
User Flag
  ↓
SUID Enumeration
  ↓
/bin/systemctl
  ↓
GTFOBins
  ↓
systemd Service
  ↓
Root
  ↓
Root Flag
```

---

# Key Takeaways

- Nmap provides the initial overview of the target's attack surface.
- Non-standard web ports should always be investigated.
- Gobuster can identify hidden directories and functionality.
- File upload restrictions based only on extensions can sometimes be bypassed using alternative extensions.
- Burp Suite is useful for inspecting web requests and upload functionality.
- SUID enumeration is an important Linux privilege escalation technique.
- Unusual SUID binaries deserve additional investigation.
- `systemctl` with SUID permissions can provide a powerful privilege escalation vector.
- GTFOBins is useful for researching known abuse techniques for Unix/Linux binaries.

---

# Final Methodology

```text
Reconnaissance
      ↓
Nmap
      ↓
Web Enumeration
      ↓
Gobuster
      ↓
/internal/
      ↓
File Upload Analysis
      ↓
Extension Bypass
      ↓
Reverse Shell
      ↓
User Access
      ↓
SUID Enumeration
      ↓
systemctl
      ↓
Privilege Escalation
      ↓
Root
      ↓
Root Flag
```