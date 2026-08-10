# 10 - Group Policies

## Overview

Explored Group Policy Objects (GPOs) and how they can be used
to apply configurations and security settings to OUs.

## Topics Covered

- Group Policy
- Group Policy Objects (GPOs)
- GPO linking
- OU inheritance
- Security Filtering
- Computer Configuration
- Restricted Groups
- SYSVOL
- gpupdate

## Group Policy Objects

A GPO is a collection of settings that can be applied to
users and computers.

GPOs can be linked to OUs.

## GPO Scope

A GPO applies to the OU where it is linked and can also affect
sub-OUs.

Example:

    Domain
      |
      └── OU
           |
           └── Sub-OU

A GPO linked higher in the hierarchy can affect objects
below it.

## Security Filtering

Security Filtering can restrict which users or computers
receive a GPO.

By default, GPOs commonly apply to:

    Authenticated Users

## Computer Configuration

Policies can target computer objects.

Example configuration used in the lab:

    Computer Configuration
    -> Policies
    -> Windows Settings
    -> Security Settings
    -> Restricted Groups

## Restricted Groups

The lab used Restricted Groups to add the:

    Product Admins

group to the local:

    Administrators

group on servers in the Servers OU.

## GPO Distribution

GPOs are distributed through the network share:

    SYSVOL

The default SYSVOL location on a Domain Controller is:

    C:\Windows\SYSVOL\sysvol\

## Force GPO Update

A computer can immediately request updated policies with:

    gpupdate /force

## Key Takeaways

- GPOs centralize Windows configuration.
- GPOs can target users or computers.
- GPOs are linked to OUs.
- GPOs can affect sub-OUs.
- Security Filtering controls who receives a GPO.
- SYSVOL is used to distribute GPOs.
- `gpupdate /force` forces an immediate policy refresh.