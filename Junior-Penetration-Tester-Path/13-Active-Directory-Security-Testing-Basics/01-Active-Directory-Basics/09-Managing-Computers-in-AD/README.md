# 09 - Managing Computers in AD

## Overview

Organized domain computers into appropriate Organizational Units.

## Topics Covered

- Computers container
- Workstations
- Servers
- Domain Controllers
- Organizational Units
- Computer organization
- Policy-based management

## Default Computer Location

By default, computers joining the domain are placed inside:

    Computers

Domain Controllers are handled separately.

## Why Organize Computers?

Keeping every machine inside the same container makes it
difficult to apply different policies to different types
of systems.

A better structure is to separate machines according to
their purpose.

## Workstations

Workstations are machines used by regular users for:

- Daily work
- Browsing
- Normal user activities

Privileged users should not normally sign into workstations.

## Servers

Servers provide services to:

- Users
- Other servers
- Applications

They should be managed separately from normal workstations.

## Domain Controllers

Domain Controllers are the most sensitive systems in the
environment because they manage the Active Directory domain
and contain highly sensitive authentication data.

## OU Structure

The lab created separate OUs for:

    Workstations
    Servers

Domain Controllers already had their own OU.

## Key Takeaways

Separating computers into appropriate OUs allows different
policies and security controls to be applied according to
the purpose of each machine.