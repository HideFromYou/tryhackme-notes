# 04 - Enumeration With BloodHound

## Overview

BloodHound was used to visualize relationships within an
Active Directory environment.

Instead of manually analysing large amounts of AD data,
BloodHound helps represent relationships between users,
groups, computers and permissions as a graph.

## Topics Covered

- BloodHound
- Active Directory relationships
- Domain users
- Domain groups
- Computers
- Group memberships
- Permissions
- Attack paths
- AD graph analysis

## Why BloodHound?

Active Directory environments can contain many users,
groups, computers and relationships.

BloodHound helps identify relationships that may not be
obvious from traditional command-line enumeration.

## Enumeration Concept

The general process is:

    Collect AD Information
            ↓
    Import Data into BloodHound
            ↓
    Build Relationship Graph
            ↓
    Analyse Users / Groups / Computers
            ↓
    Identify Interesting Relationships
            ↓
    Identify Potential Attack Paths

## Important Relationships

BloodHound can help visualise relationships involving:

- Users
- Groups
- Computers
- Domain Admins
- Local Administrators
- Sessions
- Permissions
- Group memberships

## Attack Path Analysis

The main value of BloodHound is understanding how different
permissions and memberships can connect an ordinary account
to higher-privileged accounts or systems.

Example concept:

    User
      ↓
    Group Membership
      ↓
    Local Administrator
      ↓
    Computer
      ↓
    Privileged Session
      ↓
    Higher Privileges

## Key Takeaways

BloodHound changes Active Directory enumeration from a large
collection of individual objects into a relationship graph.

This makes it easier to identify interesting relationships
and potential attack paths within the domain.