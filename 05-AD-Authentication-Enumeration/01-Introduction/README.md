# 01 - Introduction

## Overview

This room focuses on authenticated Active Directory
enumeration.

It follows the AD: Basic Enumeration room and assumes that
we already have a valid domain account.

The objective is to use the authenticated access to gather
more detailed information about the domain, users, groups,
computers and relationships within Active Directory.

## Topics Covered

- Authenticated enumeration
- Active Directory reconnaissance
- Windows command-line enumeration
- NET commands
- PowerShell
- ActiveDirectory module
- PowerView
- BloodHound

## Enumeration Approach

The room uses several approaches:

    Windows Native Commands
            ↓
    PowerShell ActiveDirectory Module
            ↓
    PowerView
            ↓
    BloodHound

Each approach provides different levels of information about
the Active Directory environment.

## Key Takeaway

Having valid domain credentials significantly increases the
amount of information that can be gathered during Active
Directory enumeration.