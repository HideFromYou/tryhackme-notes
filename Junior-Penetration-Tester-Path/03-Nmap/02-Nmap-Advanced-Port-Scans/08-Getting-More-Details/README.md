# Getting More Details

## Overview

Nmap provides several options that increase output verbosity and explain how scan results are determined, making troubleshooting and analysis easier.

---

## Learning Objectives

- Interpret Nmap results
- Increase scan verbosity
- Enable debugging
- Understand scan reasoning

---

## Explain Results

```bash
nmap --reason <TARGET_IP>
```

Shows why Nmap considers a host or port open, closed, or filtered.

---

## Verbose Output

```bash
nmap -v <TARGET_IP>
```

Very Verbose

```bash
nmap -vv <TARGET_IP>
```

---

## Debug Output

```bash
nmap -d <TARGET_IP>
```

More debugging

```bash
nmap -dd <TARGET_IP>
```

---

## Useful Information

- Scan progress
- Packet responses
- Discovery process
- Service detection reasoning

---

## Skills Practiced

- Scan Analysis
- Troubleshooting
- Enumeration

## Key Takeaways

- `--reason` explains Nmap's conclusions.
- `-v` and `-vv` increase output detail.
- `-d` provides debugging information.