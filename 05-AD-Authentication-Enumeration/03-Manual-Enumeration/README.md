# 03 - Manual Enumeration

## Overview

This task focuses on manual Active Directory enumeration
using native Windows CMD and PowerShell commands.

The objective is to understand the environment from an
authenticated Windows shell and identify users, groups,
privileges, sessions, services and system configuration.

## Topics Covered

- whoami
- whoami /all
- Security Identifiers (SID)
- Group memberships
- Token privileges
- hostname
- systeminfo
- Environment variables
- NET commands
- Domain users
- Domain groups
- Local groups
- Logged-on users
- Sessions
- Processes
- Service accounts
- WMIC
- SC
- Windows Registry
- Auto-logon credentials
- Installed applications
- Scheduled tasks

## Who Am I?

The first step is identifying the current account.

    whoami

For detailed information:

    whoami /all

This reveals:

- Username
- Domain
- SID
- Group memberships
- Account privileges

## Token Privileges

Important privileges to look for include:

    SeImpersonatePrivilege
    SeAssignPrimaryTokenPrivilege
    SeBackupPrivilege
    SeRestorePrivilege
    SeDebugPrivilege

These privileges can provide useful clues about the
current security context and potential privilege escalation
paths.

## System and Domain Information

Basic system information can be collected with:

    hostname
    systeminfo
    set

Useful information includes:

- Hostname
- Operating system
- Domain/workgroup
- Environment variables
- User directories
- Installed software hints

In PowerShell, environment variables can be viewed with:

    Get-ChildItem Env:

or:

    dir env:

## Domain User Enumeration

List domain users:

    net user /domain

Retrieve information about a specific domain user:

    net user <username> /domain

This can reveal:

- Account status
- Password information
- Group memberships
- Last logon
- Other account details

## Domain Group Enumeration

List domain groups:

    net group /domain

List members of a specific domain group:

    net group "Domain Admins" /domain

Groups worth investigating include:

- Domain Admins
- Enterprise Admins
- Server Operators
- Backup Operators
- Groups containing "Admin"

## Computer Enumeration

Machine accounts can be found through domain groups such as:

    net group "Domain Computers" /domain

Computer accounts normally end with:

    $

## Local Group Enumeration

List local groups:

    net localgroup

List members of the local Administrators group:

    net localgroup administrators

This can reveal domain accounts that have local
administrative privileges.

## Logged-on Users and Sessions

List users currently logged on:

    quser

This can reveal:

- Username
- Session type
- Session ID
- Session state
- Logon time

An administrator logged on to the system can be an
important finding during authenticated enumeration.

## Processes

List running processes:

    tasklist

Verbose output:

    tasklist /V

Processes such as:

    lsass.exe

are particularly important from a credential-access
perspective.

## SMB Sessions

Active SMB sessions can be viewed with:

    net session

This requires elevated privileges.

## Service Accounts

Services can reveal which accounts are being used to run
applications and system services.

### WMIC

    wmic service get Name,StartName

The `StartName` field identifies the account running the
service.

Interesting findings can include domain accounts such as:

    DOMAIN\username

### PowerShell

Equivalent command:

    Get-WmiObject Win32_Service | select Name, StartName

### SC

List all services:

    sc query state= all

Filter the output:

    sc query state= all | find "<keyword>"

Then inspect a specific service:

    sc qc <ServiceName>

The `SERVICE_START_NAME` field identifies the account used
by the service.

## Environment Variables

Environment variables can reveal information about:

- User directories
- Domains
- Installed software
- Development environments

Example:

    set

In PowerShell:

    Get-ChildItem Env:

## Windows Registry

The Registry can contain useful system configuration and,
in some cases, stored credentials.

### Auto-logon Credentials

Check:

    HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon

Example:

    reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v DefaultUsername

Potentially interesting values include:

    DefaultUsername
    DefaultPassword
    AutoAdminLogon

## Installed Applications

Installed applications can be enumerated with:

    reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

This can reveal software that may be relevant for further
enumeration.

## Registry Keyword Search

Search the Registry for a keyword such as "password":

    reg query HKLM /f "password" /t REG_SZ /s

## Scheduled Tasks

List scheduled tasks:

    schtasks /query

Scheduled tasks can reveal applications, scripts,
execution paths and accounts used to run tasks.

## Living Off The Land

The task demonstrates the concept of using native Windows
tools instead of introducing additional software.

Examples include:

    whoami
    net
    tasklist
    sc
    reg
    schtasks

## Key Takeaways

Manual enumeration provides a detailed picture of the
current Windows system and Active Directory environment.

The main questions are:

    Who am I?
        ↓
    What privileges do I have?
        ↓
    What domain am I in?
        ↓
    Who are the users and groups?
        ↓
    Who is logged on?
        ↓
    What services are running?
        ↓
    Which accounts run those services?
        ↓
    What sensitive information is stored locally?