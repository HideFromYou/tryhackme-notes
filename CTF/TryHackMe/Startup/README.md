# Startup - TryHackMe Walkthrough

## Difficulty
Easy

## Skills Practiced

- Nmap Enumeration
- FTP Enumeration
- Anonymous FTP Access
- Web Enumeration
- Gobuster
- File Upload
- Reverse Shell
- Linux Enumeration
- Privilege Escalation

---

## Enumeration

### Open Ports

- 21 - FTP
- 22 - SSH
- 80 - HTTP

### Initial Findings

- Anonymous FTP login enabled
- Writable FTP directory
- Uploaded files accessible through the web server
- Hidden `/files` directory discovered

---

## Initial Access

- Uploaded a PHP reverse shell
- Started a listener
- Triggered the shell through the browser
- Obtained an initial foothold

---

## Privilege Escalation

- Performed local enumeration
- Identified the privilege escalation vector
- Escalated to root

---

## Lessons Learned

- Always enumerate every exposed service.
- Writable FTP directories may map to a web root.
- Verify whether uploaded files are executable before attempting exploitation.
- Enumeration is usually more valuable than guessing passwords.
- Choose payloads based on the technologies discovered during enumeration.

---

## Tools Used

- Nmap
- FTP
- Gobuster
- Netcat
- PHP Reverse Shell
- LinPEAS (optional)

---

## MITRE ATT&CK

- T1046 – Network Service Discovery
- T1078 – Valid Accounts (if applicable)
- T1105 – Ingress Tool Transfer
- T1059 – Command and Scripting Interpreter
- T1068 / T1548 – Privilege Escalation (depending on technique)
