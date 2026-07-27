# Enumerating Targets

## Overview

Before discovering live hosts, Nmap needs to know which IP addresses to scan. It supports multiple ways of specifying targets, making it easy to scan individual hosts, ranges, or entire subnets.

---

## Learning Objectives

- Specify scan targets
- Scan ranges and subnets
- Exclude unwanted hosts

---

## Single Host

```bash
nmap 10.10.10.5
```

---

## Multiple Hosts

```bash
nmap 10.10.10.5 10.10.10.10
```

---

## IP Range

```bash
nmap 10.10.10.1-100
```

---

## Entire Subnet

```bash
nmap 10.10.10.0/24
```

---

## Input from File

```bash
nmap -iL targets.txt
```

---

## Excluding Hosts

```bash
nmap --exclude 10.10.10.5 10.10.10.0/24
```

Multiple exclusions:

```bash
nmap --exclude 10.10.10.5,10.10.10.20
```

---

## Skills Practiced

- Target Enumeration
- Reconnaissance
- Scan Planning

## Key Takeaways

- Nmap accepts hosts, ranges, subnets, and files.
- Proper targeting reduces scan time.
- Excluding unnecessary hosts improves efficiency.