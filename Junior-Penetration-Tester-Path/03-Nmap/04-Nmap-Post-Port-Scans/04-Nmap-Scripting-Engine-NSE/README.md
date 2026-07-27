# Nmap Scripting Engine (NSE)

## Overview

The Nmap Scripting Engine (NSE) extends Nmap with hundreds of Lua scripts for enumeration, security checks, authentication testing, vulnerability detection, and information gathering.

---

## Learning Objectives

- Understand NSE
- Run default scripts
- Execute individual scripts
- Explore script categories

---

## Default Scripts

```bash
sudo nmap -sC <TARGET>
```

Equivalent:

```bash
sudo nmap --script=default <TARGET>
```

---

## Run a Specific Script

```bash
sudo nmap --script http-title <TARGET>
```

Example:

```bash
sudo nmap --script ssh2-enum-algos <TARGET>
```

---

## Common Script Categories

| Category | Purpose |
|----------|---------|
| default | Default safe scripts |
| discovery | Information gathering |
| auth | Authentication checks |
| brute | Brute-force testing |
| vuln | Vulnerability detection |
| safe | Non-intrusive scripts |
| exploit | Exploitation scripts |
| malware | Malware detection |

---

## Script Location

```
/usr/share/nmap/scripts
```

---

## Skills Practiced

- Automated Enumeration
- Service Analysis
- Vulnerability Discovery

## Key Takeaways

- NSE greatly expands Nmap functionality.
- Scripts automate common reconnaissance tasks.
- Always understand a script before executing it.