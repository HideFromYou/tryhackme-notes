# 02 - Windows Domains

## Introduction

In a small environment, it is possible to manage every computer and user individually.

As an organisation grows, however, manually managing every machine becomes increasingly difficult.

Windows Domains provide a way to centralise the administration of users, computers and resources.

---

## Why Windows Domains?

Imagine an organisation with:

```text
157 computers
320 users
4 offices
```

Managing every computer separately would require administrators to configure and maintain each machine individually.

A Windows Domain allows the organisation to centralise this management.

Instead of:

```text
Computer 1 → Users
Computer 2 → Users
Computer 3 → Users
Computer 4 → Users
...
```

the environment can be managed centrally:

```text
                 Windows Domain
                       |
                Active Directory
                       |
          ┌────────────┼────────────┐
          |            |            |
       Users       Computers     Resources
```

---

# What is a Windows Domain?

A Windows Domain is a group of users and computers under the administration of a given organisation.

The main purpose of a domain is to centralise the administration of common components of a Windows network.

The centralised repository used to manage these identities and resources is:

```text
Active Directory
```

The server responsible for running the Active Directory services is called a:

```text
Domain Controller (DC)
```

---

# Domain Controller

A Domain Controller is a Windows server that runs the Active Directory services.

It acts as a central point for the domain and provides services such as:

- Authentication
- Active Directory management
- User management
- Computer management
- Domain administration

A simplified environment looks like:

```text
                  Domain
                    |
                    v
             Domain Controller
                    |
        ┌───────────┼───────────┐
        |           |           |
      Users      Computers   Resources
```

---

# Centralised Identity Management

One of the main advantages of a Windows Domain is centralised identity management.

Without a domain, every computer can maintain its own local accounts.

For example:

```text
Computer A
├── Alice
├── Bob
└── Charlie

Computer B
├── Alice
├── Bob
└── Charlie
```

Each computer would need to maintain its own accounts.

With a domain:

```text
              Active Directory
                     |
          ┌──────────┼──────────┐
          |          |          |
        Alice       Bob      Charlie
                     |
                     v
              Domain Resources
```

The accounts are managed centrally.

---

# Centralised Security Policies

Another advantage of Windows Domains is the ability to manage security policies centrally.

Administrators can configure policies and apply them across multiple computers and users.

For example:

```text
                Domain
                   |
            Security Policy
                   |
       ┌───────────┼───────────┐
       |           |           |
   Computer A  Computer B  Computer C
```

This makes it possible to maintain consistent security configurations across the organisation.

---

# Domain Authentication

A user can authenticate to a domain using their domain credentials.

The basic concept is:

```text
User
 |
 | Username + Password
 v
Computer
 |
 | Authentication Request
 v
Domain Controller
 |
 | Verify Credentials
 v
Authentication Result
```

This allows users to use their domain account across domain-connected computers, depending on their permissions and access.

---

# Active Directory and Windows Domains

The relationship between a Windows Domain and Active Directory can be represented as:

```text
Windows Domain
      |
      v
Active Directory
      |
      ├── Users
      ├── Computers
      ├── Groups
      └── Other AD Objects
```

Active Directory provides the centralised directory and management functionality used by the domain.

---

# TryHackMe Lab

The room provides a pre-configured Active Directory environment.

The domain used in the lab is:

```text
THM.local
```

The provided machine acts as the Domain Controller.

The administrator account can be used to access and manage the environment.

---

# RDP Access

The lab can be accessed using RDP.

The domain can be specified when authenticating.

Example:

```text
THM\Administrator
```

This tells Windows that the account belongs to the `THM` domain rather than being a local account.

---

# Local vs Domain Accounts

This distinction is important when working with Windows environments.

## Local Account

A local account exists only on the individual computer.

The account can be represented as:

```text
COMPUTER\username
```

For example:

```text
WS01\Administrator
```

This account belongs to the `WS01` computer.

---

## Domain Account

A domain account is managed by Active Directory.

It can be represented as:

```text
DOMAIN\username
```

For example:

```text
THM\Administrator
```

This account belongs to the `THM` domain.

---

# Domain Authentication Model

The difference can be visualised as:

```text
Local Authentication

User
 |
 v
Local Computer
 |
 v
Local Account Database
```

versus:

```text
Domain Authentication

User
 |
 v
Domain Computer
 |
 v
Domain Controller
 |
 v
Active Directory
```

This distinction becomes extremely important during penetration testing.

---

# Why Domain Membership Matters

Once a computer is part of a Windows Domain, it becomes part of a larger environment.

Instead of looking at the machine as an isolated target, we can start considering its relationships with:

```text
Computer
   |
   +-- Users
   |
   +-- Groups
   |
   +-- Domain
   |
   +-- Domain Controller
   |
   +-- Other Computers
   |
   +-- Network Resources
```

A compromise of one domain-connected machine can therefore provide information about the wider environment.

---

# Penetration Testing Perspective

When a tester identifies a Windows Domain, useful questions include:

```text
What is the domain name?
        |
        v
Who is the Domain Controller?
        |
        v
Which users exist?
        |
        v
Which groups exist?
        |
        v
Which computers are domain-joined?
        |
        v
What resources are available?
```

The answers to these questions become important during Active Directory enumeration.

---

# Important Terminology

| Term | Meaning |
|---|---|
| Windows Domain | Group of users and computers administered by an organisation |
| Active Directory | Centralised directory service used to manage the domain |
| Domain Controller | Server running Active Directory services |
| Domain Account | Account managed centrally by Active Directory |
| Local Account | Account that exists only on a specific computer |
| Domain Authentication | Authentication performed through the domain infrastructure |

---

# Questions

## Question 1

**In a Windows domain, credentials are stored in a centralised repository called?**

```text
Active Directory
```

---

## Question 2

**The server in charge of running the Active Directory services is called?**

```text
Domain Controller
```

---

# Key Takeaways

- A Windows Domain provides centralised administration.
- Domains are useful when organisations manage many users and computers.
- Active Directory provides the centralised directory used by the domain.
- The Domain Controller runs Active Directory services.
- Domain accounts are centrally managed.
- Local accounts exist only on individual machines.
- Domain authentication allows users to authenticate through the domain infrastructure.
- Domain membership connects a computer to a larger Active Directory environment.
- Understanding Windows Domains is essential before moving into Active Directory enumeration and security testing.

---

# Mental Model

```text
                         Windows Domain
                               |
                               v
                       Active Directory
                               |
                       Domain Controller
                               |
             ┌─────────────────┼─────────────────┐
             |                 |                 |
           Users           Computers          Groups
             |                 |                 |
             └─────────────────┼─────────────────┘
                               |
                          Resources
```

---

# Next

The next section covers:

**Active Directory**