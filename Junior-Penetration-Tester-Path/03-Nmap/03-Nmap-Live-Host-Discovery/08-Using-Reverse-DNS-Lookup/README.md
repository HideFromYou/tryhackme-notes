# Using Reverse DNS Lookup

## Overview

Reverse DNS (rDNS) resolves an IP address back to a hostname. During reconnaissance, this can reveal server names, roles, or naming conventions that provide additional context about the target environment.

---

## Learning Objectives

- Understand Reverse DNS
- Perform hostname lookups
- Interpret DNS results

---

## Reverse Lookup

Force reverse DNS for all hosts:

```bash
nmap -R <TARGET>
```

Disable DNS lookups:

```bash
nmap -n <TARGET>
```

Use a custom DNS server:

```bash
nmap --dns-servers <DNS_SERVER> <TARGET>
```

---

## Benefits

- Identifies server names
- Reveals infrastructure details
- Improves reconnaissance

---

## Limitations

- Records may not exist
- Names may be outdated
- Additional lookups increase scan time

---

## Skills Practiced

- DNS Enumeration
- Host Identification
- Reconnaissance

## Key Takeaways

- Reverse DNS maps IP addresses to hostnames.
- `-R` forces lookups for all hosts.
- `-n` disables DNS resolution for faster scans.