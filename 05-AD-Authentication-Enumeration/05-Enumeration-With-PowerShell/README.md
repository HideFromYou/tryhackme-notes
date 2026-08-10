# 05 - Enumeration With PowerShell

## Overview

This task focuses on authenticated Active Directory
enumeration using PowerShell.

Two approaches were explored:

1. Microsoft's ActiveDirectory PowerShell module
2. PowerView from the PowerSploit framework

## Topics Covered

- PowerShell
- ActiveDirectory module
- RSAT
- Get-ADUser
- Get-ADGroup
- Get-ADGroupMember
- Get-ADComputer
- Get-ADDefaultDomainPasswordPolicy
- PowerView
- PowerSploit
- Get-DomainUser
- Get-DomainGroup
- Get-DomainComputer
- AdminCount
- SPNs

## ActiveDirectory Module

The Microsoft ActiveDirectory module provides PowerShell
cmdlets for interacting with Active Directory.

Check whether it is available:

    Get-Module -ListAvailable ActiveDirectory

Import the module:

    Import-Module ActiveDirectory

## User Enumeration

Enumerate all domain users:

    Get-ADUser -Filter *

Retrieve information about a specific user:

    Get-ADUser -Identity <username>

Retrieve all available properties:

    Get-ADUser -Identity <username> -Properties *

Useful properties include:

    LastLogonDate
    MemberOf
    Description
    Title
    PwdLastSet

## Filtering Users

Search for accounts containing "admin":

    Get-ADUser -Filter "Name -like '*admin*'"

Filtering helps reduce large amounts of output and focus
on interesting accounts.

## Group Enumeration

List all domain groups:

    Get-ADGroup -Filter *

Display only group names:

    Get-ADGroup -Filter * | Select Name

Enumerate members of a group:

    Get-ADGroupMember -Identity "<Group Name>"

For example:

    Get-ADGroupMember -Identity "Domain Admins"

## Computer Enumeration

List domain computers:

    Get-ADComputer -Filter *

Display computer names and operating systems:

    Get-ADComputer -Filter * | Select Name, OperatingSystem

## Password Policy

Retrieve the domain password policy:

    Get-ADDefaultDomainPasswordPolicy

Important properties include:

    ComplexityEnabled
    LockoutDuration
    LockoutObservationWindow
    LockoutThreshold
    MaxPasswordAge
    MinPasswordAge
    MinPasswordLength
    PasswordHistoryCount
    ReversibleEncryptionEnabled

## PowerView

PowerView is part of the PowerSploit framework and is
designed for Active Directory enumeration.

The PowerView script can be found in the Recon directory
of PowerSploit.

Import the module:

    Import-Module .\PowerView.ps1

## PowerView User Enumeration

Enumerate domain users:

    Get-DomainUser

Filter users by name:

    Get-DomainUser *admin*

PowerView provides more detailed output and flexible
filtering compared with basic `net user /domain`.

## PowerView Group Enumeration

Enumerate domain groups:

    Get-DomainGroup

Filter groups containing "admin":

    Get-DomainGroup "*admin*"

## PowerView Computer Enumeration

Enumerate domain computers:

    Get-DomainComputer

This can reveal information such as:

- Computer names
- Operating systems
- Domain information
- SPNs
- Account properties

## AdminCount

PowerView can identify users with administrative privileges:

    Get-DomainUser -AdminCount

The `AdminCount` attribute can help identify accounts that
have been associated with protected administrative groups.

## SPNs

PowerView can identify accounts with Service Principal Names:

    Get-DomainUser -SPN

Accounts with SPNs can be relevant when investigating
Kerberoasting opportunities.

## Comparison

### NET

    net user /domain
    net group /domain

Simple native Windows enumeration.

### ActiveDirectory Module

    Get-ADUser
    Get-ADGroup
    Get-ADComputer

Provides structured PowerShell-based Active Directory
enumeration.

### PowerView

    Get-DomainUser
    Get-DomainGroup
    Get-DomainComputer

Provides extensive AD reconnaissance and filtering
capabilities.

## Enumeration Workflow

    Valid Domain Credentials
            ↓
    PowerShell
            ↓
    ActiveDirectory Module
            ↓
    Users / Groups / Computers
            ↓
    Password Policy
            ↓
    PowerView
            ↓
    Admin Accounts / SPNs / Relationships
            ↓
    Further Attack Path Analysis

## Key Takeaways

PowerShell makes authenticated Active Directory enumeration
more efficient and flexible.

The ActiveDirectory module provides official Microsoft
cmdlets, while PowerView provides additional reconnaissance
capabilities useful during penetration testing.