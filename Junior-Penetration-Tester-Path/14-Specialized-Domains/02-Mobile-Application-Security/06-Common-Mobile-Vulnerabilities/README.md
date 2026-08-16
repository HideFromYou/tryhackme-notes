
These concepts and tools are directly covered in the supplied Dynamic Analysis material. :contentReference[oaicite:5]{index=5}

### 06 — Common Mobile Vulnerabilities

```markdown
# Common Mobile Vulnerabilities

## Insecure Data Storage

Sensitive information may be stored insecurely on the device.

Examples include:

- Plain-text credentials
- Session tokens
- Unencrypted local databases
- Sensitive data in shared storage
- Cached API responses

This maps to:

```text
OWASP M9 — Insecure Data Storage


Improper Platform Usage

Applications may misuse or fail to use platform security features correctly.

Examples include:

Excessive permissions
Insecure communication between application components
Improper use of platform functionality
Insecure Authentication and Session Management

Common findings include:

Weak session tokens
Tokens stored insecurely
Missing re-authentication
Weak biometric authentication implementations

A biometric check that is trusted only on the client side may be bypassable at runtime.

This maps to:

OWASP M3 — Insecure Authentication and Authorisation
Exposed Application Components

An exported component may allow another application on the device to interact with sensitive functionality.

If appropriate access controls are missing, the component becomes an attack surface.

This maps to:

OWASP M8 — Security Misconfiguration
Insufficient Binary Protections

Weak binary protections make reverse engineering and tampering easier.

Important checks include:

Code obfuscation
Tamper detection
Root detection
Jailbreak detection

The absence of root or jailbreak detection can be a finding for applications handling sensitive information.

This maps to:

OWASP M7 — Insufficient Binary Protections
Key Takeaway

The major vulnerability categories covered include:

Insecure Data Storage
        ↓
Improper Platform Usage
        ↓
Insecure Authentication
        ↓
Exposed Components
        ↓
Insufficient Binary Protections