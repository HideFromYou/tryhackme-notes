# 03 - Active Directory

## Active Directory Domain Services

Active Directory Domain Services (AD DS) is the core service used by Windows Domains.

It acts as a catalogue containing information about the objects that exist within the network.

Examples include:

- Users
- Computers
- Groups
- Printers
- Shares
- Other network resources

---

## Users

Users are one of the most common object types in Active Directory.

Users are also considered **Security Principals**.

A Security Principal is an object that can be authenticated and assigned permissions over resources.

Users can represent:

- People
- Services

### People

A normal user account can represent an employee who needs access to domain resources.

### Services

User accounts can also be used as service accounts.

Examples include services such as:

```text
IIS
MSSQL
```

Service accounts should normally have only the permissions required for the service they are running.

---

## Machines

Computers that join an Active Directory Domain receive a machine account.

Machine accounts are also Security Principals.

For example:

```text
Computer:
DC01

Machine Account:
DC01$
```

The `$` at the end identifies a machine account.

Machine account passwords are automatically rotated and are generally long random values.

---

## Security Groups

Security Groups allow administrators to organise multiple users or computers together.

Instead of assigning permissions individually:

```text
Alice → Permission
Bob → Permission
Charlie → Permission
```

a group can be created:

```text
Group
 ├── Alice
 ├── Bob
 └── Charlie
```

The permission can then be assigned to the group.

Groups can contain:

- Users
- Computers
- Other groups

---

## Important Default Groups

### Domain Admins

Members of Domain Admins have administrative privileges across the domain.

They can administer domain computers, including Domain Controllers.

### Server Operators

Can administer Domain Controllers but have restrictions on changing administrative group memberships.

### Backup Operators

Can access files for backup purposes while bypassing normal file permissions.

### Account Operators

Can create or modify accounts in the domain.

### Domain Users

Contains domain user accounts.

### Domain Computers

Contains domain computer accounts.

### Domain Controllers

Contains the Domain Controllers in the domain.

---

## Active Directory Users and Computers

The main graphical administration tool introduced in this section is:

```text
Active Directory Users and Computers
```

It allows administrators to manage:

- Users
- Groups
- Computers
- Organizational Units

---

## Organizational Units

Organizational Units (OUs) are containers used to organise objects in Active Directory.

Example:

```text
THM
├── IT
├── Management
├── Marketing
├── R&D
└── Sales
```

OUs are useful for organising users and computers and applying policies to specific organisational sections.

---

## OUs vs Security Groups

OUs and Security Groups have different purposes.

### Organizational Units

Primarily used for:

```text
Organisation
+
Policy Application
```

A user can belong to only one OU at a time.

### Security Groups

Primarily used for:

```text
Permissions
+
Access Control
```

A user can belong to multiple security groups.

Example:

```text
User
 ├── Sales OU
 ├── VPN Group
 ├── Printer Group
 └── Shared Folder Group
```

---

## Default Containers

Important default Active Directory containers include:

### Builtin

Contains default groups available to Windows hosts.

### Computers

Domain computers are placed here by default.

### Domain Controllers

Contains Domain Controllers.

### Users

Contains default domain users and groups.

### Managed Service Accounts

Contains managed service accounts.

---

## Questions

### Which group normally administrates all computers and resources in a domain?

```text
Domain Admins
```

### What is the machine account for TOM-PC?

```text
TOM-PC$
```

### What type of container should be used to group Quality Assurance users so policies can be applied consistently?

```text
Organizational Units
```

---

## Key Takeaways

- AD DS is the core Active Directory service.
- Users are Security Principals.
- Computers have machine accounts.
- Machine accounts use the `$` suffix.
- Security Groups are primarily used for permissions.
- Organizational Units are primarily used for organisation and policy application.
- Users can belong to multiple groups.
- Users belong to one OU at a time.
- Domain Admins provide domain-wide administrative access.