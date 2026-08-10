# 11 - Foreign Forest Trust

## Overview

Established a trust relationship between two different
Active Directory forests and used it to provide cross-forest
access to resources.

## Scenario

Two forests were involved:

    thm.loc
    tvm.loc

A trust relationship was configured between them.

## Topics Covered

- Active Directory Domains and Trusts
- Forest Trust
- Two-way Trust
- Forest-wide authentication
- Cross-domain resource access
- Cross-forest users
- Group membership across trusts
- Bidirectional trust

## Creating the Trust

The trust was configured through:

    Active Directory Domains and Trusts

The configuration involved:

1. Opening the Trusts properties.
2. Creating a New Trust.
3. Specifying the other domain.
4. Selecting Forest Trust.
5. Selecting a Two-way trust.
6. Configuring the relationship for both domains.
7. Providing credentials from the other domain.
8. Selecting Forest-wide authentication.
9. Confirming incoming and outgoing trusts.

## Sharing Resources

After establishing the trust, a user from the external forest
could be added to a security group in the other domain.

Example:

    THM\Claire

was added to:

    Server Admins

This allowed the external user to authenticate to a server
in the other domain.

## Bidirectional Trust

The lab demonstrated how trust relationships can extend
through a parent-child domain structure.

The relationship was:

    tvm.loc
        ↕
    thm.loc
        ↕
    tbm.thm.loc

Because `tbm.thm.loc` is a child domain of `thm.loc`, the
trust relationship with the external forest also allowed
cross-forest interaction with the child domain.

## Cross-Forest Administration Example

The `alice.king` account from `tvm.loc` was added to the
`Product Admins` group in `tbm.thm.loc`.

The previous GPO configured Product Admins as local
administrators on servers in the Servers OU.

Therefore, the external account could ultimately obtain
local administrative access to Server1.

## Important Security Concept

Trust relationships do not automatically provide
administrative privileges.

Access is possible because:

1. A trust relationship exists.
2. The external account is added to an appropriate group.
3. That group has permissions over the target resource.

## Key Takeaways

- Forest Trusts allow cross-forest relationships.
- Trusts can be one-way or two-way.
- Two-way trusts allow mutual authorization.
- External users can be added to groups in trusted domains.
- Existing group permissions and GPOs can extend the impact
  of cross-forest trust relationships.