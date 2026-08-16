# 08 - Conclusion

## Overview

Cloud security testing combines traditional penetration-testing techniques with cloud-specific services and identity controls.

The main concepts covered in this room are:

    IAM
    Cloud Storage
    Cloud Networking
    Compute
    Metadata Services
    SSRF
    Temporary Credentials

---

## Shared Responsibility

Cloud security follows a shared-responsibility model.

The cloud provider is responsible for the security of the underlying infrastructure.

The customer is responsible for areas such as:

    Data
    Identities
    Permissions
    Configuration
    Applications

A secure cloud environment therefore depends heavily on correct customer configuration.

---

## IAM

IAM determines what identities are allowed to do.

Important concepts:

    Users
    Roles
    Policies
    Permissions

When credentials are obtained, always determine:

    Which identity do they belong to?
    ↓
    What permissions does it have?
    ↓
    What resources can it access?

Pay particular attention to:

    Action: *
    Resource: *

Overly broad permissions can create privilege-escalation or data-access paths.

---

## Cloud Storage

Publicly accessible storage should always be investigated.

Look for:

    Public Buckets
    Public Objects
    Backups
    Source Code
    Configuration Files
    Credentials
    Logs
    Sensitive Data

A simple public file can also provide information required to continue an attack.

---

## Cloud Networking

Important networking concepts include:

    Virtual Networks
    Subnets
    Security Groups
    Network ACLs

During reconnaissance, identify:

    Internet-facing services
    Open ports
    Database services
    Administrative interfaces
    Internal services

Remember:

    0.0.0.0/0
        ↓
    Entire Internet

After obtaining a foothold, investigate the internal network for lateral-movement opportunities.

---

## Compute and Metadata

Cloud instances still expose traditional attack surfaces:

    Vulnerable Applications
    Open Services
    Weak Credentials
    Unpatched Software

However, cloud instances also have access to metadata services.

The important attack concept is:

    Compromised Instance
          ↓
    Metadata Service
          ↓
    Temporary Credentials
          ↓
    IAM Permissions
          ↓
    Cloud Resources

---

## SSRF in Cloud Environments

SSRF becomes particularly dangerous in cloud environments because the vulnerable server may be able to access internal cloud services.

The key chain is:

    SSRF
      ↓
    Metadata Service
      ↓
    Temporary Credentials
      ↓
    IAM Role
      ↓
    Additional Cloud Access

This is one of the most important cloud-specific attack paths to remember.

---

# Final Pentesting Checklist

When assessing a cloud environment:

    1. Identify the cloud provider.

    2. Enumerate Internet-facing services.

    3. Check public storage.

    4. Search exposed files for useful information.

    5. Enumerate IAM identities and permissions.

    6. Look for excessive or wildcard permissions.

    7. Identify public and private network segments.

    8. Check firewall rules for unnecessary exposure.

    9. After gaining a foothold, investigate internal resources.

    10. Check whether SSRF can reach metadata services.

    11. Identify temporary credentials.

    12. Determine what those credentials can access.

---

# Complete Cloud Attack Pattern

    Internet Exposure
            ↓
    Misconfiguration
            ↓
    Information Disclosure
            ↓
    Initial Access
            ↓
    SSRF / Internal Access
            ↓
    Metadata
            ↓
    Temporary Credentials
            ↓
    IAM Enumeration
            ↓
    Excessive Permissions
            ↓
    Additional Cloud Resources

---

# Key Takeaways

- Cloud security relies heavily on correct configuration and IAM.
- Public storage can expose sensitive information.
- Wide-open firewall rules increase the attack surface.
- Internal cloud networks can enable lateral movement.
- Metadata services can provide temporary credentials.
- SSRF can be chained with metadata access.
- Obtaining credentials is only the beginning; their permissions determine the real impact.
- Cloud penetration testing is largely about identifying and chaining misconfigurations.

## Core Mental Model

    FIND EXPOSURE
          ↓
    ENUMERATE ACCESS
          ↓
    FIND CREDENTIALS
          ↓
    ENUMERATE IAM
          ↓
    FIND PRIVILEGE
          ↓
    ACCESS MORE RESOURCES