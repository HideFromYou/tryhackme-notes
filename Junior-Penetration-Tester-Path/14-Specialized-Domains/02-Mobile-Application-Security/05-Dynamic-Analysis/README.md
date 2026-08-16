
The supplied material specifically covers unpacking/decompilation, Android Manifest, iOS `Info.plist`, `NSAllowsArbitraryLoads`, hardcoded secrets and MobSF. :contentReference[oaicite:3]{index=3} :contentReference[oaicite:4]{index=4}

### 05 — Dynamic Analysis

```markdown
# Dynamic Analysis

## Overview

Dynamic analysis examines a mobile application while it is running.

Unlike static analysis, which focuses on code and package contents, dynamic analysis focuses on actual application behaviour.

## What We Observe

During dynamic analysis, a tester can examine:

- Network traffic
- Data stored on the device
- Application logs
- Runtime behaviour
- Application components
- Authentication behaviour

## Traffic Interception

A proxy can be used to intercept application traffic.

This allows the tester to determine:

- What data is sent to the backend
- Whether HTTPS/TLS is used
- How authentication tokens are handled
- Whether unexpected third-party services are contacted

Unencrypted sensitive traffic can indicate **M5 — Insecure Communication**.

## SSL Pinning

SSL pinning restricts an application to trusting specific certificates rather than any certificate issued by a recognised authority.

This can prevent a proxy from intercepting HTTPS traffic.

SSL pinning itself is a security control rather than a vulnerability.

For testing purposes, the supplied material introduces **Objection** as a tool that can help disable SSL pinning on a running application.

## Runtime Instrumentation

Runtime instrumentation allows a tester to observe or modify application behaviour while it is executing.

**Frida** is introduced as a widely used runtime instrumentation framework.

It can be used to:

- List classes and methods
- Hook functions
- Observe data passed through functions
- Test authentication logic
- Inspect data held in memory

Objection is built on top of Frida.

## Dynamic vs Static Analysis

```text
Static Analysis
    ↓
Examines code and package contents

Dynamic Analysis
    ↓
Examines runtime behaviour

Both approaches are required for a thorough mobile security assessment.

Key Takeaway

Static analysis shows what the application contains, while dynamic analysis shows what the application actually does while running.