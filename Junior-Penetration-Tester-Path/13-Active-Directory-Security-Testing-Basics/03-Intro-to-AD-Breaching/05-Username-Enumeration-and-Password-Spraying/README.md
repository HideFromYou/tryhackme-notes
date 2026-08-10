# 05 - Username Enumeration and Password Spraying

## Overview

Explored password spraying against a validated list of
Active Directory usernames.

## Topics Covered

- Password spraying
- Brute-force vs password spraying
- Account lockout policies
- NetExec
- SMB authentication
- Password policy enumeration
- Authentication results
- Spray detection
- Spray targets

## Brute-Force vs Password Spraying

### Brute-Force

Targets one account with many passwords.

    One account
        ↓
    Many passwords

This can quickly trigger account lockout policies.

### Password Spraying

Uses one password against many accounts.

    One password
        ↓
    Many accounts

Then another password can be attempted after the appropriate
lockout observation period.

## Lockout Policies

Before spraying, determine the domain's password policy
when possible.

NetExec can query the policy:

    nxc smb <DC_IP> -u '<validuser>' -p '<validpassword>' --pass-pol

Important values include:

- Minimum password length
- Password history
- Account lockout threshold
- Reset counter
- Locked account duration
- Password complexity
- Password age

## Cleaning Kerbrute Output

Extract valid usernames:

    grep "VALID USERNAME" valid_users.txt | awk '{print $NF}' | sed 's/@thm.loc//' > clean_users.txt

## Password Spraying with NetExec

Example:

    nxc smb <DC_IP> -u clean_users.txt -p '<PASSWORD>' --continue-on-success

### Parameters

`-u`

Username or username list.

`-p`

Single password used for the spray.

`--continue-on-success`

Continue testing all usernames even after finding a
successful authentication.

## Interpreting Results

### Successful Authentication

    [+]

Valid username/password combination.

### Failed Authentication

    STATUS_LOGON_FAILURE

Incorrect password.

### Disabled Account

    STATUS_ACCOUNT_DISABLED

The account exists but is disabled.

### Locked Account

    STATUS_ACCOUNT_LOCKED_OUT

Stop spraying and investigate the lockout policy.

### Administrative Access

    Pwn3d!

Indicates local administrator privileges on the target host.

## Jitter

NetExec can introduce delays between attempts:

    nxc smb <DC_IP> -u clean_users.txt -p '<PASSWORD>' --continue-on-success --jitter 2-5

## Other Spray Targets

Password spraying can also target:

- SMB
- LDAP
- WinRM
- RDP
- MSSQL
- OWA
- VPN portals

## Key Takeaways

Password spraying differs fundamentally from brute-forcing.

The goal is to minimise authentication attempts per account
while testing predictable or known passwords across many
validated usernames.