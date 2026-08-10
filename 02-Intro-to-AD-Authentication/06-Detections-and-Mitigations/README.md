# 06 - Detections & Mitigations

## Overview

Explored Windows Security Event IDs used to detect
authentication activity and mapped authentication attacks
to defensive mitigations.

## Key Windows Event IDs

| Event ID | Description |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4768 | Kerberos TGT requested |
| 4769 | Kerberos service ticket requested |
| 4771 | Kerberos pre-authentication failed |

## Detecting NTLM Attacks

Event ID:

    4624

Important fields include:

    Authentication Package: NTLM
    Logon Type: 3

A network logon using NTLM against a high-value target can
indicate a possible Pass-the-Hash attack.

## Detecting Kerberoasting

Event ID:

    4769

Kerberoasting may produce a high volume of service-ticket
requests from a single account within a short period.

Another indicator is:

    Ticket Encryption Type: 0x17

which represents RC4-HMAC.

## Detecting AS-REP Roasting

Event ID:

    4771

A spike of Kerberos pre-authentication failures across
multiple accounts may indicate AS-REP Roasting or
brute-force activity.

## Mitigations

### Pass-the-Hash

- Add privileged accounts to Protected Users
- Disable NTLM where Kerberos is available

### NTLM Relay

- Enforce SMB signing
- Enable Extended Protection for Authentication (EPA)
  on LDAP and AD CS

### Kerberoasting

- Use strong random service-account passwords
- Migrate to Group Managed Service Accounts (gMSA)

### Golden Ticket

- Protect the KRBTGT account
- Reset the KRBTGT password twice after suspected compromise

### Password Spraying

- Configure account lockout policies
- Monitor Event ID 4625

## Key Takeaways

Authentication attacks leave traces in Windows Security logs.

Understanding Event IDs and their relevant fields allows
defenders to identify suspicious authentication activity
and apply appropriate mitigations.