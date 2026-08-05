# Using Hydra

## Overview

This lesson demonstrates how to use **Hydra** to perform online password brute-force attacks against live authentication services. You will learn the basic syntax of Hydra, understand the required command-line options, and practice attacking both **SSH** and **HTTP POST** login forms.

The practical lab reinforces how weak passwords can be discovered quickly using wordlists while emphasizing that Hydra should only be used during authorized penetration tests. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Install and launch Hydra
- Understand Hydra's command syntax
- Perform SSH brute-force attacks
- Perform HTTP POST form brute-force attacks
- Identify the required parameters for different services
- Use Hydra responsibly during penetration tests

---

## Main Content

### Preparing the Environment

Hydra is pre-installed on the TryHackMe AttackBox.

Before beginning the practical exercise:

- Start the AttackBox
- Deploy the target machine
- Connect to the target service

Hydra can also be installed on Linux distributions such as Ubuntu and Fedora using the system package manager or by downloading it from its official repository.

---

### Hydra Command Structure

Hydra commands vary depending on the protocol being attacked.

A basic command requires:

- Target service
- Username
- Password wordlist
- Protocol

Example:

```bash
hydra -l user -P passlist.txt ftp://MACHINE_IP
```

This command attempts to authenticate to an FTP service using a single username and multiple passwords. :contentReference[oaicite:1]{index=1}

---

### Brute Forcing SSH

The lesson demonstrates the following syntax for attacking an SSH service:

```bash
hydra -l <username> -P <password_list> MACHINE_IP -t 4 ssh
```

Important options include:

| Option | Description |
|---------|-------------|
| `-l` | Username |
| `-P` | Password wordlist |
| `-t` | Number of concurrent threads |

Increasing the thread count allows Hydra to perform multiple authentication attempts simultaneously. :contentReference[oaicite:2]{index=2}

---

### Brute Forcing HTTP POST Forms

Hydra can also attack web application login forms.

General syntax:

```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "<path>:<parameters>:<failure_string>" -V
```

Important components include:

| Parameter | Purpose |
|-----------|---------|
| `<path>` | Login page path |
| `^USER^` | Username placeholder |
| `^PASS^` | Password placeholder |
| `F=` | Text indicating failed authentication |
| `-V` | Verbose output |

Hydra replaces the placeholders with each username and password combination during the attack. :contentReference[oaicite:3]{index=3}

---

### Non-Default Ports

If a web application runs on a non-standard port, Hydra allows the port to be specified manually using:

```bash
-s <port>
```

This ensures Hydra connects to the correct service during the brute-force attack. :contentReference[oaicite:4]{index=4}

---

### Practical Exercise

The lab demonstrates two common online password attacks:

- Brute forcing a web application's POST login form
- Brute forcing an SSH service

These exercises highlight how weak passwords can be discovered efficiently using password wordlists and automated authentication attempts.

---

## Skills Practiced

- Hydra
- Online Password Attacks
- SSH Brute Force
- HTTP POST Form Attacks
- Authentication Testing
- Wordlist Usage
- Penetration Testing

---

## Key Takeaways

- Hydra supports multiple authentication protocols and uses protocol-specific syntax.
- SSH attacks require a username, password list, target, and optional thread count.
- HTTP POST attacks require knowledge of the login form fields and the application's failure response.
- Verbose mode and custom ports improve visibility and flexibility during testing.
- Hydra should only be used against systems where explicit authorization has been granted. :contentReference[oaicite:5]{index=5}