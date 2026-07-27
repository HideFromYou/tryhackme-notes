# Conclusion

## Topics Covered

- Service Detection (`-sV`)
- Version Intensity
- OS Detection (`-O`)
- Traceroute (`--traceroute`)
- Nmap Scripting Engine (`-sC`)
- NSE Categories
- Saving Scan Results

---

## Typical Workflow

```bash
sudo nmap -sS TARGET
sudo nmap -sS -sV TARGET
sudo nmap -sS -sV -O TARGET
sudo nmap -sS -sV -O -sC TARGET
sudo nmap -oA results TARGET
```

---

## Skills Developed

- Service Enumeration
- OS Fingerprinting
- Automated Reconnaissance
- Reporting

## Final Takeaways

- Service detection identifies software versions.
- OS fingerprinting improves target profiling.
- NSE automates powerful reconnaissance tasks.
- Saving scan results supports professional reporting and future analysis.