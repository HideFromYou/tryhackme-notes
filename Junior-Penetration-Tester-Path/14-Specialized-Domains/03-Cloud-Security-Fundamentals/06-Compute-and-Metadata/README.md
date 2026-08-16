# 06 - Compute and Metadata Services

## Overview

Cloud instances are still regular Linux or Windows systems, so traditional attacks such as exposed services, weak credentials, vulnerable applications, and missing patches still apply.

The cloud-specific feature that is especially important to a penetration tester is the **Instance Metadata Service (IMDS)**.

---

## Cloud Compute

A cloud instance is essentially a virtual machine running inside the provider's infrastructure.

Common attack surfaces remain:

    Open Services
    Weak Credentials
    Vulnerable Applications
    Unpatched Software
    Misconfigured Permissions

The cloud adds another important attack surface:

    Instance Metadata Service

---

# Instance Metadata Service (IMDS)

The metadata service provides information about the running cloud instance.

A commonly used metadata address is:

    169.254.169.254

Depending on the cloud provider, metadata can expose information such as:

    Instance Information
    Configuration
    Identity Information
    Temporary Credentials

For a penetration tester, temporary credentials are particularly important because they may allow access to other cloud resources.

---

# IMDS and Credentials

A cloud instance can have an associated IAM role or equivalent identity.

The metadata service may provide temporary credentials associated with that role.

Conceptually:

    Cloud Instance
          ↓
    Instance Metadata
          ↓
    Temporary Credentials
          ↓
    IAM Permissions
          ↓
    Cloud Resources

The impact therefore depends heavily on the permissions assigned to the instance identity.

---

# IMDSv1 vs IMDSv2

## IMDSv1

IMDSv1 uses simple HTTP requests.

The weakness from an attacker's perspective is that applications vulnerable to **SSRF** may be able to make requests to the metadata service on behalf of the attacker.

Conceptually:

    Attacker
       ↓
    SSRF Vulnerability
       ↓
    Metadata Service
       ↓
    Temporary Credentials

---

## IMDSv2

IMDSv2 introduces a session-token mechanism.

A client must first obtain a metadata session token and then use that token for subsequent metadata requests.

This makes common SSRF attacks significantly harder because a simple GET request is no longer sufficient.

The security lesson is:

    IMDSv1 → Easier metadata access
    IMDSv2 → Token-based access

---

# SSRF → Cloud Credentials

This is one of the most important cloud attack chains.

A vulnerable application may allow an attacker to control a URL that the server fetches.

If the server can reach the metadata service:

    Vulnerable Web Application
              ↓
             SSRF
              ↓
       Metadata Service
              ↓
      Instance Credentials
              ↓
         IAM Permissions
              ↓
       Cloud Resources

The SSRF itself may therefore have a much greater impact in a cloud environment than on a normal web server.

---

# AWS Metadata Example

AWS commonly uses:

    169.254.169.254

An attacker testing an authorised SSRF vulnerability may investigate the metadata service.

Example metadata path:

    /latest/meta-data/

IAM role credentials are associated with a path such as:

    /latest/meta-data/iam/security-credentials/<role-name>

A successful response may contain temporary values such as:

    AccessKeyId
    SecretAccessKey
    Token
    Expiration

These credentials should be treated as sensitive secrets.

---

# Other Cloud Providers

The exact metadata implementation differs between providers.

| Provider | Metadata Address / Service |
|---|---|
| AWS | 169.254.169.254 |
| Azure | 169.254.169.254 |
| Google Cloud | metadata.google.internal / metadata service |

The important pentesting concept is not memorising every provider-specific endpoint.

It is recognising:

    SSRF
      +
    Cloud Metadata
      =
    Potential Credential Access

---

# Other Cloud Compute Targets

Cloud compute is not limited to traditional virtual machines.

Examples include:

    Virtual Machines
    Containers
    Serverless Functions
    Managed Container Platforms

Each introduces different attack surfaces.

Potential findings include:

    Exposed Services
    Secrets in Configuration
    Excessive IAM Permissions
    Vulnerable Applications
    Insecure Container Configuration

---

# Pentester Mindset

After compromising a cloud instance, do not stop at the operating system.

Ask:

    What identity does this instance have?

    Can it access metadata?

    Is IMDSv1 enabled?

    What permissions does its role have?

    What cloud resources can those permissions access?

    Can the compromised instance reach internal services?

This turns a simple host compromise into a cloud attack-path investigation.

---

# Attack Chain to Remember

    Initial Access
         ↓
    Compromised Cloud Instance
         ↓
    Metadata Service
         ↓
    Temporary Credentials
         ↓
    IAM Role
         ↓
    Cloud API Access
         ↓
    Additional Resources

---

# Key Takeaways

- Cloud instances still have traditional operating-system attack surfaces.
- The Instance Metadata Service is a major cloud-specific attack surface.
- `169.254.169.254` is a commonly used metadata address.
- Metadata can provide temporary credentials associated with an instance identity.
- SSRF can potentially be chained with metadata access.
- IMDSv1 is significantly easier to abuse through simple SSRF.
- IMDSv2 adds token-based protection.
- The impact of stolen cloud credentials depends on the permissions of the associated IAM role.
- Always investigate the instance identity and its permissions after gaining a cloud foothold.

## Core Concept

    SSRF → Metadata → Credentials → IAM → Cloud Resources