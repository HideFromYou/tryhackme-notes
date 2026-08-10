# 05 - Trees, Forests and Trusts

## Overview

Explored how multiple Active Directory domains can be organized
into larger structures.

## Topics Covered

- Multiple AD domains
- Trees
- Forests
- Enterprise Admins
- Trust Relationships
- One-way trusts
- Two-way trusts
- Access across domains

## Trees

A Tree is a group of Active Directory domains that share the
same namespace.

Example:

    thm.local
    ├── uk.thm.local
    └── us.thm.local

Each domain can have its own:

- Domain Controller
- Users
- Computers
- Policies
- Domain Administrators

## Enterprise Admins

The Enterprise Admins group provides administrative privileges
across the domains in an enterprise.

Domain Admins normally administer their individual domain,
while Enterprise Admins can manage the enterprise.

## Forests

A Forest is a collection of multiple domain trees that can use
different namespaces.

Example:

    thm.local
    mht.local

Together, their trees can form a forest.

## Trust Relationships

Trust relationships allow users from one domain to be
authorized to access resources in another domain.

## One-Way Trust

In a one-way trust:

    Domain A trusts Domain B

Users from Domain B can potentially be authorized to access
resources in Domain A.

The direction of the trust is opposite to the direction of
the resulting access.

## Two-Way Trust

A two-way trust allows both domains to mutually authorize
users from the other domain.

Domains within a tree or forest can have trust relationships
automatically established.

## Important

A trust relationship does NOT automatically give users access
to every resource in the other domain.

Permissions still need to be explicitly configured.

## Key Takeaways

- Tree = domains sharing the same namespace.
- Forest = collection of domain trees.
- Trust = relationship allowing cross-domain authentication/
  authorization.
- Trust does not automatically equal resource access.