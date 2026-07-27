# Saving Output

## Overview

Saving scan results allows findings to be reviewed later, shared with teammates, or included in penetration testing reports.

---

## Learning Objectives

- Save scan results
- Choose output formats
- Organize scan data

---

## Normal Output

```bash
nmap -oN scan.txt <TARGET>
```

---

## XML Output

```bash
nmap -oX scan.xml <TARGET>
```

---

## Grepable Output

```bash
nmap -oG scan.grep <TARGET>
```

---

## Save All Formats

```bash
nmap -oA results <TARGET>
```

Produces:

```
results.nmap
results.xml
results.gnmap
```

---

## Skills Practiced

- Documentation
- Reporting
- Result Management

## Key Takeaways

- Always save important scans.
- Different formats support different tools.
- `-oA` is the most convenient option.