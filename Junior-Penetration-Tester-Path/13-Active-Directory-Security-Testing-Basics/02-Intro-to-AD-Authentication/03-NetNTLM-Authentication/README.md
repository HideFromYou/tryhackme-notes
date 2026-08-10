# 03 - NetNTLM Authentication

## Overview

Explored how NetNTLM authentication works and the
challenge-response mechanism used by NTLM.

## Topics Covered

- NetNTLM
- Challenge-response authentication
- NTLM authentication flow
- NTLM hashes
- Domain Controller validation
- Pass-the-Hash
- NTLM Relay
- Downgrade attacks
- Lack of mutual authentication

## NetNTLM

NetNTLM is a challenge-response authentication protocol
used in Windows environments.

The plaintext password is not transmitted over the network.

## Authentication Flow

    Client
      |
      | Authentication Request
      v
    Server
      |
      | Challenge
      v
    Client
      |
      | Challenge Response
      v
    Server
      |
      | Validation
      v
    Domain Controller
      |
      | Result
      v
    Server

## Challenge-Response

The server generates a challenge.

The client uses authentication material associated with the
user's password to generate a response.

The response is then validated by the Domain Controller.

## Security Weaknesses

NTLM has several important weaknesses:

- Weak cryptography
- Pass-the-Hash
- NTLM Relay
- Downgrade attacks
- Lack of mutual authentication

## Pass-the-Hash

An attacker who obtains an NTLM hash can potentially
authenticate without knowing the plaintext password.

## NTLM Relay

NTLM does not provide mutual authentication, allowing
authentication attempts to potentially be intercepted and
relayed to another service.

## Key Takeaways

NTLM uses challenge-response authentication.

Although the plaintext password is not transmitted,
compromise of the NTLM hash can still allow authentication.