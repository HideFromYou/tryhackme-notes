# TryHackMe — TakeOver

## Room

**TakeOver**

**Difficulty:** Easy

**Room Link:** https://tryhackme.com/room/takeover

---

## Objective

The objective of this room is to identify a **subdomain takeover** caused by a DNS/cloud configuration issue.

The attack path involves:

- Reconnaissance
- Port scanning
- Subdomain discovery
- `/etc/hosts` configuration
- SSL certificate inspection
- Subject Alternative Name (SAN) enumeration
- AWS S3 identification
- Identifying a non-existent S3 bucket
- Subdomain takeover

---

# 1. Reconnaissance

The target domain is:

```text
futurevera.thm
```

Start with a basic Nmap scan to identify the available services:

```bash
nmap futurevera.thm
```

The scan identifies three relevant open ports:

```text
22/tcp   SSH
80/tcp   HTTP
443/tcp  HTTPS
```

The presence of HTTP and HTTPS indicates that the web application should be investigated further.

The main website is:

```text
https://futurevera.thm/
```

---

# 2. Discovering the First Subdomain

The room provides a clue that the company is rebuilding its support infrastructure.

This suggests investigating a possible `support` subdomain:

```text
support.futurevera.thm
```

Before accessing the hostname, it needs to be mapped to the target IP address through the local `/etc/hosts` file.

Edit the hosts file:

```bash
sudo nano /etc/hosts
```

Add the target IP together with:

```text
support.futurevera.thm
```

After configuring `/etc/hosts`, access:

```text
https://support.futurevera.thm/
```

The subdomain loads a website with an SSL certificate.

---

# 3. SSL Certificate Inspection

Inspect the certificate presented by:

```text
https://support.futurevera.thm/
```

Open the certificate information and inspect the listed names.

The certificate contains an **Alternative Name**.

The **Subject Alternative Name (SAN)** reveals another subdomain associated with the target.

This provides another hostname to investigate.

Add the newly discovered hostname to `/etc/hosts`:

```bash
sudo nano /etc/hosts
```

---

# 4. Discovering the Second Subdomain

Access the newly discovered subdomain.

An important detail is that the hostname should be accessed through:

```text
Port 80
```

rather than:

```text
Port 443
```

When accessed over HTTP, the subdomain redirects to an:

```text
AWS S3 static website
```

Instead of displaying the expected website, the AWS endpoint returns a:

```text
Not Found
```

response.

This indicates that the subdomain is pointing toward an AWS S3 bucket that no longer exists.

---

# 5. Identifying the Subdomain Takeover

The discovered subdomain is configured to point toward an AWS S3 resource.

However, the referenced S3 bucket does not exist.

This creates a **subdomain takeover** condition.

The attack path is:

```text
futurevera.thm
        ↓
support.futurevera.thm
        ↓
SSL Certificate
        ↓
Alternative Name / SAN
        ↓
Second Subdomain
        ↓
Port 80
        ↓
AWS S3 Static Website
        ↓
S3 Bucket Does Not Exist
        ↓
Subdomain Takeover
```

This is an example of a dangling cloud resource where a subdomain continues to reference an external cloud service after the associated resource has been removed.

---

# 6. Retrieving the Flag

The AWS redirection contains the flag directly in the URL.

The URL follows the format:

```text
flag{*******************************}.s3-website-us-west-3.amazonaws.com
```

The flag can therefore be obtained directly from the AWS S3 redirection URL.

---

# Attack Chain

```text
Nmap
  ↓
futurevera.thm
  ↓
support.futurevera.thm
  ↓
SSL Certificate Inspection
  ↓
Subject Alternative Name
  ↓
Hidden Subdomain
  ↓
Port 80
  ↓
AWS S3 Static Website
  ↓
Non-existent S3 Bucket
  ↓
Subdomain Takeover
  ↓
Flag in URL
```

---

# Commands Used

## Nmap

```bash
nmap futurevera.thm
```

## Edit /etc/hosts

```bash
sudo nano /etc/hosts
```

The discovered hostnames are mapped to the target IP in `/etc/hosts`.

---

# Key Findings

| Stage | Finding |
|---|---|
| Initial target | `futurevera.thm` |
| SSH | Port `22` |
| HTTP | Port `80` |
| HTTPS | Port `443` |
| First subdomain | `support.futurevera.thm` |
| Discovery method | SSL certificate |
| Certificate field | Alternative Name / SAN |
| Second subdomain | Discovered through certificate |
| Important port | `80` |
| Cloud service | AWS S3 |
| Problem | Referenced S3 bucket does not exist |
| Vulnerability | Subdomain takeover |
| Flag location | AWS S3 redirection URL |

---

# Tools Used

- Nmap
- Browser
- `/etc/hosts`
- SSL Certificate Inspection
- AWS S3

---

# Key Takeaways

- Basic Nmap reconnaissance is enough to establish the initial attack surface.
- Web services on ports `80` and `443` should be investigated during reconnaissance.
- `/etc/hosts` can be used to resolve custom hostnames to the target machine.
- SSL certificates can expose additional hostnames through their **Subject Alternative Names (SANs)**.
- Discovered subdomains should be tested on both HTTP and HTTPS where applicable.
- A subdomain may point to an external cloud service even when the underlying resource no longer exists.
- AWS S3 static website endpoints can reveal dangling cloud resources.
- A subdomain pointing to a non-existent cloud resource can result in a **subdomain takeover**.
- Redirect URLs can sometimes expose sensitive information directly.

---

# Methodology

```text
Reconnaissance
      ↓
Nmap
      ↓
Identify Open Services
      ↓
Web Application
      ↓
Subdomain Discovery
      ↓
SSL Certificate Inspection
      ↓
SAN Enumeration
      ↓
Discover Additional Hostname
      ↓
Update /etc/hosts
      ↓
Test HTTP / HTTPS
      ↓
Identify AWS S3 Endpoint
      ↓
Identify Missing S3 Bucket
      ↓
Confirm Subdomain Takeover
      ↓
Retrieve Flag
```