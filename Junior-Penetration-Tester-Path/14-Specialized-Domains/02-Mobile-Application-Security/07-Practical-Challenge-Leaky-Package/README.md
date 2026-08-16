
The supplied material explicitly covers insecure storage, improper platform usage, authentication/session management, exposed components and binary protections. :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}

### 07 — Practical Challenge: Leaky Package

```markdown
# Practical Challenge — Leaky Package

## Scenario

The challenge focuses on **Helix Solutions**, a technology company whose mobile employee portal application may contain sensitive information left inside its production packages.

Two application packages are analysed:

- Android APK
- iOS IPA

Both are based on the same application codebase.

## Tool

The main tool used in the challenge is:

```text
MobSF

The goal is to perform static analysis and identify sensitive information and security weaknesses.

Android Analysis

The Android application is uploaded to MobSF and analysed.

Initial findings included:

Security score: 40/100
Package: com.tryhackme.leakypackage
1 of 2 activities exported
Decompiled Java source available
AndroidManifest.xml available
Smali bytecode available
Permissions

Several dangerous permissions were identified, including:

ACCESS_FINE_LOCATION
CAMERA
READ_CONTACTS
READ_EXTERNAL_STORAGE
RECORD_AUDIO

The challenge identifies these as excessive permissions for an internal employee portal.

This maps to:

OWASP M8 — Security Misconfiguration
Findings

The challenge required identifying:

Hardcoded API key in Java source
Hardcoded database password
Unprotected exported Activity
Info.plist key disabling App Transport Security
Sensitive value stored in internal_config.plist
iOS Analysis

MobSF identified:

App Transport Security AllowsArbitraryLoads is allowed

The application also contained:

internal_config.plist

with a sensitive internal value bundled inside the production IPA.

Lessons

The challenge demonstrates how static analysis can uncover real security findings without needing to execute the application.

Important areas to inspect include:

Permissions
Manifest
Decompiled code
Exported components
Configuration files
Property lists
Hardcoded secrets
Transport security configuration