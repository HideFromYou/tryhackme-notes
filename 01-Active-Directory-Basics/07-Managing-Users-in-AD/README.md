# 07 - Managing Users in AD

## Overview

Explored user management and delegation inside Active Directory.

## Topics Covered

- Active Directory Users and Computers
- OUs
- Users
- Advanced Features
- Delegation
- Password reset delegation
- Group-based administration

## Active Directory Users and Computers

The main management interface used to administer:

- Users
- Groups
- Computers
- OUs

## Advanced Features

Advanced Features can be enabled from:

    View -> Advanced Features

This exposes additional AD containers and management options.

## Delegation

Delegation allows specific users or groups to perform
administrative tasks over selected OUs without requiring
Domain Administrator privileges.

## Example

The Tech Support group was delegated permission over the
Bankers OU.

The delegated permission allowed members of Tech Support to:

- Reset user passwords
- Force users to change their password at next logon

## Why Delegation Matters

Delegation follows the principle of giving specific
administrative capabilities without granting full
Domain Administrator privileges.

## Key Takeaways

- AD administration can be delegated.
- Delegation can be applied to specific OUs.
- Permissions can be granular.
- Helpdesk/IT support users can receive limited administrative
  capabilities without becoming Domain Administrators.