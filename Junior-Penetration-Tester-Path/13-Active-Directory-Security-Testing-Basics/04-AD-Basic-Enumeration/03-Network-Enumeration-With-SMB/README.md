# 03 - Network Enumeration With SMB

## Overview

In this task, we focused on enumerating network shares using
the Server Message Block (SMB) protocol.

We used Nmap to discover relevant services and then used
smbclient and smbmap to enumerate and access SMB shares.

## Topics Covered

- SMB
- Nmap
- SMB ports
- smbclient
- smbmap
- Anonymous SMB access
- Null sessions
- SMB share enumeration
- Share permissions
- Accessing SMB shares
- Downloading files
- enum4linux
- enum4linux-ng
- Impacket smbclient
- CrackMapExec

## SMB-Related Ports

| Port | Protocol | Purpose |
|---:|---|---|
| 88 | Kerberos | Active Directory authentication |
| 135 | MS-RPC | Remote Procedure Calls |
| 139 | NetBIOS Session Service | File sharing in older Windows systems |
| 389 | LDAP | Active Directory enumeration |
| 445 | SMB | File sharing and remote administration |
| 636 | LDAPS | Secure LDAP |

## Nmap Service Discovery

The relevant Windows and Active Directory ports can be
enumerated with:

    nmap -p 88,135,139,389,445,636 -sV -sC <TARGET_IP>

### Options

    -sV    Service version detection
    -sC    Run default NSE scripts

The presence of Kerberos, LDAP and SMB can indicate that
the target is part of an Active Directory environment and
may be a Domain Controller.

## Listing SMB Shares

Since we did not have valid credentials, we tested whether
the SMB server allowed anonymous access.

### smbclient

List available SMB shares:

    smbclient -L //<TARGET_IP> -N

### Options

    -L    List available shares
    -N    Do not request a password

An anonymous SMB connection is also known as a null session.

## smbmap

`smbmap` can enumerate SMB shares and display the permissions
available to the current session.

    smbmap -H <TARGET_IP>

Example permissions:

    READ
    WRITE
    READ, WRITE
    NO ACCESS

This makes it useful for quickly identifying shares that
may be accessible without credentials.

## SMB Share Enumeration with Nmap

Nmap can also enumerate SMB shares using:

    nmap -p445 --script smb-enum-shares <TARGET_IP>

This can identify which shares provide READ, WRITE or
NO ACCESS permissions.

## Accessing SMB Shares

To connect to an anonymously accessible share:

    smbclient //<TARGET_IP>/<SHARE_NAME> -N

Once connected, list the files:

    ls

Download a file:

    get <file_name>

Exit the SMB session:

    exit

## Example Workflow

The basic process is:

    smbclient -L //<TARGET_IP> -N
        ↓
    Identify accessible shares
        ↓
    smbclient //<TARGET_IP>/<SHARE_NAME> -N
        ↓
    ls
        ↓
    get <file_name>

## What Can Be Found in SMB Shares?

From a penetration testing perspective, SMB shares can
contain:

- Configuration files
- Backup files
- Scripts
- Documents
- Usernames
- Credentials
- Other sensitive information

Writable shares can be particularly interesting because
users may upload files to them.

## Other Tools

### Impacket smbclient

Impacket provides a Python-based implementation of
`smbclient`.

The toolkit is available on the AttackBox under:

    /opt/impacket/examples/

### CrackMapExec

CrackMapExec can also be used for SMB enumeration,
credential testing and other Windows network operations.

### enum4linux

A broad SMB enumeration tool:

    enum4linux -a <TARGET_IP>

### enum4linux-ng

A newer implementation capable of extensive enumeration
against Windows systems.

## Key Takeaways

SMB is one of the most important services to enumerate
during an Active Directory assessment.

Anonymous or misconfigured SMB shares can expose useful
information even when no valid credentials are available.

The main enumeration workflow is:

    Nmap
      ↓
    Identify SMB
      ↓
    Enumerate Shares
      ↓
    Identify Permissions
      ↓
    Access Anonymous Shares
      ↓
    Download Interesting Files
      ↓
    Search for Sensitive Information