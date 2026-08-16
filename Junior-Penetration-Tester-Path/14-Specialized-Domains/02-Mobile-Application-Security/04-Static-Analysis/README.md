
The supplied conclusion explicitly defines the four phases as reconnaissance, static analysis, dynamic analysis and reporting. :contentReference[oaicite:2]{index=2}

### 04 — Static Analysis

```markdown
# Static Analysis

## Overview

Static analysis is the process of examining a mobile application without running it.

It is normally one of the first technical steps of a mobile penetration test because the application package alone can reveal significant findings.

## Obtaining the Package

The application package may be obtained:

- Directly from the client
- From a test device
- From an application store

Once obtained, the package can be unpacked and analysed.

## Decompilation

A decompiler converts compiled application code into a more human-readable form.

The output is not identical to the original source code, but it can provide enough information to:

- Understand application logic
- Follow data flow
- Identify sensitive information
- Discover vulnerabilities

## Android Manifest Analysis

Important checks include:

### Over-requested Permissions

Determine whether the application requests permissions that it does not actually need.

### Exported Components

Check whether activities, services or data providers are accessible to other applications unnecessarily.

### Insecure Configuration

Look for manifest settings that weaken the application's security posture.

## iOS Info.plist

On iOS, `Info.plist` provides application configuration information.

Important checks include:

- Permissions
- Configuration settings
- Application behaviour
- Security-related flags

### NSAllowsArbitraryLoads

The supplied material highlights:

```text
NSAppTransportSecurity
└── NSAllowsArbitraryLoads

When enabled, this can disable Apple's App Transport Security and allow unencrypted HTTP communication.

Hardcoded Secrets

Search for sensitive information such as:

API keys
Passwords
Encryption keys
Tokens
Internal URLs

Potential locations include:

Decompiled code
String resources
Configuration files
Local databases
.plist files
MobSF

Mobile Security Framework (MobSF) is an open-source automated tool used for mobile static analysis.

It can identify:

Permissions
Hardcoded secrets
Insecure configurations
Other potential security issues

MobSF provides a useful initial overview before performing deeper manual analysis.

OWASP Mapping

Static analysis findings can map to categories including:

M1 — Improper Credential Usage
M8 — Security Misconfiguration
Key Takeaway

Static analysis allows a tester to identify security weaknesses in an application package before executing the application.