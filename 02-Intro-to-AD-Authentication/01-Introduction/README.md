# 01 - Introduction

## Overview

Introduction to authentication in Active Directory environments.

## Topics Covered

- What authentication means
- Authentication material
- Username and password authentication
- Certificates
- Password hashes
- Authentication vs Authorisation
- NetNTLM
- Kerberos
- LDAP
- SMB
- AD authentication attack surface

## Authentication

Authentication is the process of proving your identity.

It answers the question:

    "Are you who you claim to be?"

## Authentication Material

Common authentication material includes:

- Username and password
- Cryptographic certificates
- Password hashes

## Authentication vs Authorisation

### Authentication

Proves who you are.

    "You are John."

### Authorisation

Determines what you are allowed to access.

    "John has access to the finance share."

Authentication happens first. Authorisation then determines
what resources the authenticated identity can access.

## Core AD Authentication Protocols

The two core authentication protocols in Active Directory are:

- NetNTLM
- Kerberos

## Key Takeaways

Understanding NTLM and Kerberos is fundamental to understanding
Active Directory authentication and many common AD attacks.