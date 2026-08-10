# 07 - Mitigations

## Overview

Explored defensive measures against the AD breaching
techniques covered in the module.

## Topics Covered

- Secrets management
- Password policies
- Account lockout
- Device hardening
- LDAP / LDAPS
- File-share security
- NTLM hardening
- SMB signing
- Network segmentation
- MFA

## Secrets Management

Avoid storing credentials directly in:

- Source code
- Git repositories
- Configuration files
- CI/CD logs

Recommended controls:

- Dedicated secrets vaults
- Pre-commit secret scanning
- Repository history audits
- Immediate credential rotation
- CI/CD log redaction

Example tools:

    TruffleHog
    Gitleaks

## Password Policies

Recommended controls include:

- Long passwords
- Banned common passwords
- Avoiding predictable organisation-specific patterns
- Unique initial passwords
- Appropriate account lockout policies
- Monitoring distributed authentication failures

## Device Hardening

Network devices should:

- Have default credentials changed
- Use LDAPS instead of plaintext LDAP
- Restrict administration interfaces
- Use dedicated low-privilege service accounts
- Be included in vulnerability scanning and asset management

## LDAP Security

Plaintext LDAP:

    TCP 389

Encrypted LDAP:

    LDAPS TCP 636

Use LDAPS for directory integrations where possible.

## File Share Security

Apply the principle of least privilege.

Users should only have write access where required.

Monitor suspicious file types such as:

    .url
    .lnk
    .scf
    desktop.ini

Also monitor unusual SMB authentication patterns.

## NTLM Hardening

Disable NTLMv1 and enforce NTLMv2.

Relevant Group Policy setting:

    Network Security: LAN Manager authentication level

Recommended configuration:

    Send NTLMv2 response only.
    Refuse LM & NTLM

## SMB Signing

Enforce SMB signing to reduce the risk of NTLM relay attacks.

## Outbound SMB

Block unnecessary outbound SMB traffic:

    TCP 445

especially from internal workstations to external systems.

## Network Segmentation

Separate sensitive management interfaces into dedicated
management networks/VLANs.

Examples:

- Printer administration
- Jenkins
- Git servers
- Other management interfaces

## MFA

Enable MFA on:

- Internet-facing services
- VPN
- Email
- Remote access gateways
- Critical internal services

## Key Takeaways

The same techniques used to breach AD can be understood from
the defensive perspective.

Strong credential management, hardened authentication,
least privilege, network segmentation and monitoring
significantly reduce the available attack surface.