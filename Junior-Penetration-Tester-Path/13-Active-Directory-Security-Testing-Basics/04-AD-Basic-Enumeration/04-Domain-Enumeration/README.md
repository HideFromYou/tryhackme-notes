# 04 - Domain Enumeration

## Overview

In this task, we focused on enumerating Active Directory
users and domain information without valid credentials.

We used LDAP, RPC and Kerberos-based techniques to discover
and validate domain users.

## Topics Covered

- LDAP
- Anonymous LDAP Bind
- ldapsearch
- enum4linux-ng
- RPC
- Null Sessions
- rpcclient
- User Enumeration
- RID Cycling
- Kerberos
- Kerbrute
- Username Validation

## LDAP Enumeration

LDAP is commonly used to access and manage directory services
such as Microsoft Active Directory.

Some LDAP servers may allow anonymous read-only queries.

### Test Anonymous LDAP Bind

    ldapsearch -x -H ldap://<DC_IP> -s base

### Options

    -x    Simple authentication / anonymous authentication
    -H    Specify the LDAP server
    -s    Specify the search scope

If anonymous access is enabled, the query can reveal
information about the domain and Domain Controller.

## LDAP User Enumeration

After identifying the domain, user information can be queried:

    ldapsearch -x -H ldap://<DC_IP> \
    -b "dc=<domain>,dc=<tld>" "(objectClass=person)"

This searches for objects with:

    objectClass=person

## enum4linux-ng

`enum4linux-ng` automates several Windows and Active Directory
enumeration techniques.

Command:

    enum4linux-ng -A <DC_IP> -oA results.txt

### Options

    -A    Perform all available enumeration functions
    -oA   Save output to YAML and JSON files

The enumeration can include:

- Users
- Groups
- Shares
- Password policy
- RID information
- Operating system information
- NetBIOS information

## RPC Enumeration

Microsoft RPC services can be accessed through SMB.

If the target allows unauthenticated null sessions, an
unauthenticated user may be able to enumerate domain
information.

### Test RPC Null Session

    rpcclient -U "" <DC_IP> -N

### Options

    -U ""    Use an empty username
    -N       Do not request a password

If the connection is successful, domain users can be
enumerated with:

    enumdomusers

## RID Cycling

A Relative Identifier (RID) forms part of a Windows Security
Identifier (SID).

Some well-known RIDs include:

    500    Administrator
    501    Guest
    512    Domain Admins
    513    Domain Users
    514    Domain Guests

User accounts commonly use higher RID values.

If direct user enumeration is restricted, individual RIDs
can be queried.

Example:

    for i in $(seq 500 2000); do \
    echo "queryuser $i" | rpcclient -U "" -N <DC_IP> 2>/dev/null \
    | grep -i "User Name"; \
    done

### Command Breakdown

    for i in $(seq 500 2000)

Iterates through a range of possible RIDs.

    queryuser $i

Queries the object associated with the current RID.

    2>/dev/null

Suppresses error messages.

    grep -i "User Name"

Filters the output for usernames.

## Kerbrute Username Enumeration

Kerberos is the primary authentication protocol for
Microsoft Windows domains.

Kerbrute can be used to enumerate valid Active Directory
usernames through Kerberos pre-authentication behaviour.

### Validate a User List

    ./kerbrute userenum --dc <DC_IP> -d <DOMAIN> users.txt

Valid usernames are returned as:

    VALID USERNAME

## Why Validate Usernames?

Usernames obtained through other enumeration techniques
may include:

- Disabled accounts
- Non-domain accounts
- Honeypot accounts
- False positives

Kerbrute can help confirm which usernames are valid
Active Directory accounts.

## Enumeration Workflow

    LDAP Anonymous Bind
            ↓
    LDAP User Enumeration
            ↓
    RPC Null Session
            ↓
    RID Cycling
            ↓
    Candidate User List
            ↓
    Kerbrute
            ↓
    Valid AD Users
            ↓
    Password Spraying

## Key Takeaways

Unauthenticated LDAP, RPC and Kerberos enumeration can reveal
valuable information about an Active Directory environment.

The main objective is to build an accurate list of valid
domain users that can be used during the next stage of the
assessment.