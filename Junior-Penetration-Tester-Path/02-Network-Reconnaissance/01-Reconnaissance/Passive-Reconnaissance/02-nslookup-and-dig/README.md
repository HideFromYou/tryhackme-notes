# nslookup & dig

## Overview

`nslookup` and `dig` are DNS query tools used to retrieve public DNS records such as A, AAAA, MX, TXT, CNAME and SOA records.

## Learning Objectives

- Query DNS records
- Understand common DNS record types
- Compare nslookup and dig

## Common Record Types

- A
- AAAA
- MX
- TXT
- CNAME
- SOA

## Common Commands

```bash
nslookup example.com
dig example.com
dig example.com MX
dig example.com TXT
```

## Skills Practiced

- DNS Enumeration
- Infrastructure Discovery

## Key Takeaways

- `dig` provides more detailed output than `nslookup`.
- DNS records reveal valuable infrastructure information.
- TXT records often contain SPF, DKIM and verification data.