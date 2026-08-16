# 07 - Practical: Cloud Attack Chain

## Overview

This practical combines the main cloud concepts from the previous lessons into one attack chain.

The scenario demonstrates how several individual weaknesses can be chained together:

    Network Exposure
        ↓
    Public Storage
        ↓
    Information Discovery
        ↓
    SSRF
        ↓
    Instance Metadata
        ↓
    Temporary Credentials
        ↓
    IAM Permissions
        ↓
    Protected Resource

---

## 1. Network Reconnaissance

Start with a port scan:

    nmap <TARGET_IP>

Identify exposed services and investigate the HTTP services first.

The important concept is:

    What is exposed?
    ↓
    What service is running?
    ↓
    What functionality can we interact with?

---

## 2. Enumerate Cloud Storage

Once an object-storage service is identified, check whether buckets can be accessed without authentication.

Example:

    curl http://<TARGET_IP>:9000/

If bucket names are returned, enumerate them.

Example:

    curl http://<TARGET_IP>:9000/<BUCKET>/

Look for files containing useful information such as:

    Configuration files
    Development notes
    Credentials
    Application information
    Internal URLs

---

## 3. Information Discovery

A public file may reveal information about another service.

For example:

    Public Storage
          ↓
    Development Notes
          ↓
    Image Fetcher
          ↓
    /fetch?url=

The important point is that the first vulnerability does not necessarily provide direct access to the final target.

Instead, it provides information that enables the next step.

---

## 4. Identify SSRF

If an application allows the user to supply a URL that the server fetches, investigate it for SSRF.

Generic example:

    http://<TARGET_IP>:8080/fetch?url=<URL>

The vulnerability exists when:

    User controls URL
          ↓
    Server makes the request
          ↓
    Server returns the response

The attacker can potentially make the server request internal resources that are not directly accessible from the Internet.

---

## 5. SSRF Against Metadata

Cloud environments commonly expose an internal metadata service.

The important AWS/Azure metadata address is:

    169.254.169.254

The attack concept is:

    SSRF
      ↓
    169.254.169.254
      ↓
    Instance Metadata
      ↓
    IAM Role Information

AWS IAM role credentials can be associated with:

    /latest/meta-data/iam/security-credentials/<ROLE_NAME>

A successful response may contain:

    AccessKeyId
    SecretAccessKey
    Token
    Expiration

These are temporary cloud credentials.

---

## 6. Enumerate IAM Permissions

Obtaining credentials is not the end of the attack.

The next question is:

    What can these credentials do?

Determine the permissions associated with the compromised identity.

Look specifically for:

    Wildcard Actions
    Wildcard Resources
    Access to sensitive storage
    Ability to assume additional roles

A dangerous policy may contain:

    Action: *

or:

    Resource: *

The more permissive the policy, the greater the potential impact.

---

## 7. Access the Protected Resource

If the compromised identity has permissions over another cloud resource, use those permissions to access it.

The attack chain becomes:

    Public Storage
          ↓
    Information Disclosure
          ↓
    SSRF
          ↓
    Metadata
          ↓
    Temporary Credentials
          ↓
    IAM Enumeration
          ↓
    Excessive Permissions
          ↓
    Protected Resource

---

# Complete Attack Chain

    1. Scan the target
             ↓
    2. Identify exposed cloud services
             ↓
    3. Enumerate public storage
             ↓
    4. Read useful files
             ↓
    5. Discover SSRF functionality
             ↓
    6. Access cloud metadata
             ↓
    7. Obtain temporary credentials
             ↓
    8. Enumerate IAM permissions
             ↓
    9. Identify excessive permissions
             ↓
    10. Access the protected resource

---

# Tools

The practical relies primarily on familiar tools:

    nmap
    curl

The important lesson is that cloud penetration testing does not require completely different tools.

The main difference is understanding the cloud-specific attack surface.

---

# Pentester Mindset

Do not treat each finding as an isolated vulnerability.

Instead ask:

    Can this finding give me information
    for the next step?

Then:

    Can the next step give me credentials?

Then:

    What can those credentials access?

This produces an attack-path mindset rather than a checklist-only approach.

---

# Key Takeaways

- Cloud compromises can be chains of individually simple weaknesses.
- Public storage can provide reconnaissance information.
- SSRF can provide access to internal cloud services.
- Metadata services can expose temporary credentials.
- Temporary credentials must always be mapped to their permissions.
- IAM misconfigurations can turn limited access into broader cloud access.
- The final impact depends on how far the attack chain can be extended.

## Core Pattern

    Exposure
        ↓
    Information
        ↓
    SSRF
        ↓
    Metadata
        ↓
    Credentials
        ↓
    IAM
        ↓
    Cloud Resources