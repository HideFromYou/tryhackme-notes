# 05 - Password Spraying

## Overview

In this task, we focused on password spraying against
discovered Active Directory users.

Before performing the spray, we first enumerated the domain
password policy to understand the account lockout settings
and avoid unnecessary failed authentication attempts.

## Topics Covered

- Password spraying
- Brute-force vs password spraying
- Password policy
- Account lockout
- rpcclient
- CrackMapExec
- SMB authentication
- Credential validation

## Password Spraying

Password spraying tests a small number of common passwords
against many different user accounts.

The basic idea is:

    One Password
         ↓
    Many Accounts

This is different from traditional brute-force attacks:

    One Account
         ↓
    Many Passwords

## Why Password Spraying?

Password spraying can be effective when users:

- Reuse common passwords
- Use predictable password patterns
- Use seasonal passwords
- Use passwords that have appeared in previous breaches

The objective is to find a valid username/password
combination without triggering account lockout.

## Enumerating the Password Policy

Before performing a password spray, we need to understand
the target domain's password policy.

### rpcclient

Connect to the Domain Controller using an anonymous
null session:

    rpcclient -U "" <DC_IP> -N

Once connected, query the domain password information:

    getdompwinfo

Important information includes:

- Minimum password length
- Password complexity
- Password history
- Account lockout threshold
- Lockout duration
- Reset counter

### CrackMapExec

The password policy can also be queried using:

    crackmapexec smb <DC_IP> --pass-pol

## Password Complexity

Windows password policies can require a combination of:

- Uppercase letters
- Lowercase letters
- Numbers
- Special characters

Passwords may also be prevented from containing the user's
account name or significant parts of their full name.

## Creating a Password List

Based on the discovered password policy, a small list of
potential passwords can be created.

Example:

    Password!
    Password1
    Password1!
    P@ssword
    Pa55word1

The exact passwords used during an engagement should be
based on information gathered during reconnaissance.

## Password Spraying with CrackMapExec

Using the discovered usernames and password list:

    crackmapexec smb <TARGET_IP> -u users.txt -p passwords.txt

Where:

    users.txt      Contains discovered usernames
    passwords.txt  Contains candidate passwords

## Interpreting Results

A successful authentication is commonly indicated by:

    [+]

A failed authentication can appear as:

    STATUS_LOGON_FAILURE

The result should always be interpreted together with the
target's account and password policies.

## Account Lockout

Account lockout policies are critical when performing
password spraying.

Important values include:

    Account Lockout Threshold
    Account Lockout Duration
    Reset Account Lockout Counter After

The goal is to keep the number of failed attempts against
each individual account below the lockout threshold.

## Attack Chain

The complete process is:

    Domain Enumeration
          ↓
    Valid User List
          ↓
    Password Policy Enumeration
          ↓
    Candidate Passwords
          ↓
    Password Spray
          ↓
    Valid Credentials

## Key Takeaways

Password spraying is not simply about trying many passwords.

The important part is combining:

- Accurate username enumeration
- Password policy enumeration
- Account lockout awareness
- Carefully selected passwords
- Controlled authentication attempts

This makes password spraying a practical technique for
obtaining initial Active Directory credentials.