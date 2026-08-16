# 02 - Mobile Application Security


---


# 01 - Introduction


Mobile application security testing is different from traditional web application testing because mobile applications have their own package formats, permission models and application components.


The room focuses on building a platform-independent foundation before moving into Android- or iOS-specific testing.


---


# 02 - How Mobile Applications Work


## Application Package


A mobile application is a structured package containing:


- Application binary
- Manifest or configuration file
- Resources
- Assets
- Images
- Fonts
- Local databases
- Stored strings


The package is the starting point for static analysis.


## Manifest / Configuration


The manifest describes how the application interacts with the operating system.


It can contain:


- Application information
- Requested permissions
- Component configuration
- Component accessibility


From a security testing perspective, the manifest can reveal excessive permissions and unnecessarily exposed components.


## Sandbox


Mobile operating systems use a sandbox model to isolate applications.


Applications normally run inside their own containers and cannot directly access the files or processes of other applications.


A weakened sandbox or insecure application configuration can therefore create additional attack surface.


## Application Components


Mobile applications are composed of different components.


Components may:


- Display information
- Run in the background
- Respond to system events
- Provide data to other applications


Components can be internal or exported.


An exported component that should have remained internal can become an attack surface.


---


# 03 - Mobile Penetration Testing Methodology


A mobile penetration test follows four main phases:


```text
Reconnaissance
      ↓
Static Analysis
      ↓
Dynamic Analysis
      ↓
Reporting
Reconnaissance

Understand the application and its attack surface.

Static Analysis

Analyse the application package without executing it.

Look for:

Permissions
Configuration
Components
Hardcoded secrets
Application logic
Local files
Dynamic Analysis

Analyse the application while it is running.

Look for:

Network traffic
Runtime behaviour
Local storage
Logs
Authentication behaviour
Component interaction
Reporting

Document:

Finding
Location
Description
Impact
Evidence
Remediation
04 - Static Analysis

Static analysis examines the application without executing it.

Package Acquisition

The application package may be obtained from:

Client-provided files
A test device
An application store

Once obtained, the package can be unpacked and analysed.

Decompilation

A decompiler converts compiled application code into a more human-readable representation.

This allows the tester to:

Understand application logic
Follow data flow
Search for sensitive information
Identify potential vulnerabilities
Android Manifest

Important checks include:

Over-requested Permissions

Determine whether the application requests permissions that it does not actually require.

Exported Components

Check whether activities, services or data providers are unnecessarily accessible to other applications.

Insecure Configuration

Look for configuration options that weaken the application's security.

iOS Info.plist

The iOS equivalent is Info.plist.

It contains:

Permissions
Configuration
Application behaviour

One important setting is:

NSAppTransportSecurity
└── NSAllowsArbitraryLoads

When enabled, this can disable App Transport Security and allow unencrypted HTTP communication.

This maps to:

M5 - Insecure Communication
M8 - Security Misconfiguration
Hardcoded Secrets

Search for:

API keys
Passwords
Encryption keys
Tokens
Internal URLs

Potential locations include:

Decompiled code
String resources
Configuration files
Databases
.plist files
MobSF

Mobile Security Framework (MobSF) is an open-source automated mobile security analysis tool.

It can identify:

Permissions
Hardcoded secrets
Insecure configurations
Other potential security issues

MobSF provides a useful initial overview before deeper manual analysis.

05 - Dynamic Analysis

Dynamic analysis examines the behaviour of a running application.

Unlike static analysis, which focuses on code and package contents, dynamic analysis focuses on what the application actually does.

Traffic Interception

A proxy can be used to inspect:

Requests
Responses
Authentication tokens
Backend communication
Third-party communication
HTTPS/TLS usage

Unencrypted sensitive traffic maps to:

M5 - Insecure Communication
SSL Pinning

SSL pinning restricts the certificates an application trusts.

When enabled, an interception proxy may be unable to inspect HTTPS traffic normally.

SSL pinning is a security control, not a vulnerability itself.

Objection can be used during security testing to work around SSL pinning on a running application.

Runtime Instrumentation

Runtime instrumentation allows a tester to observe or modify application behaviour while it is executing.

Frida can be used to:

Inspect classes and methods
Hook functions
Observe data
Test authentication logic
Inspect runtime data

Objection is built on top of Frida.

Insecure Logging

Applications may accidentally write sensitive information to system logs.

Potentially exposed information includes:

Usernames
Tokens
API responses
Passwords

Sensitive information in logs maps to:

M9 - Insecure Data Storage
06 - Common Mobile Vulnerabilities
Insecure Data Storage

Sensitive information may be stored insecurely on the device.

Examples:

Plain-text credentials
Session tokens
Unencrypted databases
Shared storage
Sensitive cached API responses
M9 - Insecure Data Storage
Improper Platform Usage

Applications may misuse platform security features.

Examples:

Excessive permissions
Insecure component communication
Incorrect use of platform security controls

Relevant categories include:

M1 - Improper Credential Usage
M8 - Security Misconfiguration
Insecure Authentication and Session Management

Potential findings include:

Weak session tokens
Tokens that do not expire
Insecure token storage
Missing re-authentication
Weak biometric implementations

A client-side-only biometric check may be bypassable at runtime.

M3 - Insecure Authentication and Authorisation
Exposed Application Components

An exported component can allow other applications on the device to interact with sensitive functionality.

If appropriate access controls are missing, the component becomes an attack surface.

M8 - Security Misconfiguration
Insufficient Binary Protections

Binary protections make applications harder to reverse engineer, modify or execute in unauthorised environments.

Important checks include:

Code obfuscation
Tamper detection
Root detection
Jailbreak detection

The absence of root or jailbreak detection can be significant for applications handling sensitive information.

M7 - Insufficient Binary Protections
07 - Practical Challenge: Leaky Package
Scenario

The challenge involves Helix Solutions, a technology company whose internal employee portal applications contain sensitive information inside production packages.

Two packages are analysed:

Android APK
iOS IPA

Both applications originate from the same codebase.

The main tool used is:

MobSF
Android Analysis

The Android application:

LeakyPackage.apk

was analysed using MobSF.

Initial findings included:

Security Score: 40/100
Package: com.tryhackme.leakypackage
Exported Activities: 1 / 2

The analysis exposed:

AndroidManifest.xml
Decompiled Java
Smali bytecode
Permissions
Security findings
Excessive Permissions

Dangerous permissions included:

ACCESS_FINE_LOCATION
CAMERA
READ_CONTACTS
READ_EXTERNAL_STORAGE
RECORD_AUDIO

For an internal employee portal, these permissions are excessive.

This maps to:

M8 - Security Misconfiguration
Debuggable Application

The manifest contained:

android:debuggable="true"

A production application should not be released with debugging enabled.

Exported Admin Activity

The application contained:

com.tryhackme.leakypackage.AdminPanelActivity

with:

android:exported="true"

and no permission restriction.

This means another application installed on the device could launch the activity directly.

Hardcoded Secrets

The decompiled Java source contained sensitive information.

API Key

A hardcoded API key was found in:

HelixConfig.java

This maps to:

M1 - Improper Credential Usage
Database Credentials

DatabaseHelper.java contained:

Database host
Database name
Production database password

This demonstrates the danger of storing backend credentials directly inside a distributed mobile application.

iOS Analysis

The iOS application:

LeakyPackage.ipa

was analysed with MobSF.

Security Score: 45/100
Identifier: com.tryhackme.LeakyPackage
App Transport Security

The Info.plist contained:

NSAppTransportSecurity
└── NSAllowsArbitraryLoads = true

This disables App Transport Security and allows unencrypted HTTP communication.

Relevant categories:

M5 - Insecure Communication
M8 - Security Misconfiguration
Sensitive Data in IPA

The application bundle contained:

internal_config.plist

The file contained an internal sensitive token that should not have been included in a production application.

This maps to:

M9 - Insecure Data Storage
Overall Mobile Testing Workflow
                 Mobile Application
                         │
                         ▼
                  Reconnaissance
                         │
                         ▼
                  Obtain Package
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
       Static Analysis       Dynamic Analysis
              │                     │
              ▼                     ▼
        Manifest / plist       Network Traffic
        Decompiled Code        SSL Pinning
        Permissions            Runtime Behaviour
        Hardcoded Secrets      Logging
        Components             Storage
              │                     │
              └──────────┬──────────┘
                         ▼
                    Vulnerabilities
                         │
                         ▼
                      Reporting
Key Tools
Tool	Purpose
MobSF	Automated mobile application security analysis
jadx / decompiler	Analyse compiled application code
apktool	Android package analysis
Burp Suite	Network traffic interception
Objection	Runtime mobile exploration and SSL-pinning bypass
Frida	Runtime instrumentation
Key Concepts
Application Package
Manifest
Info.plist
Sandbox
Permissions
Exported Components
Static Analysis
Dynamic Analysis
SSL Pinning
Runtime Instrumentation
Hardcoded Secrets
Insecure Storage
Authentication
Binary Protections
MobSF
Attack Surface

A mobile application should be assessed across multiple layers:

Application Package
        ↓
Configuration
        ↓
Permissions
        ↓
Application Components
        ↓
Source / Decompiled Code
        ↓
Local Storage
        ↓
Network Communication
        ↓
Runtime Behaviour
Final Takeaway

Mobile application penetration testing requires analysing both the application package and the application's behaviour at runtime.

Static analysis can reveal permissions, insecure configurations, exposed components and hardcoded secrets before the application is executed.

Dynamic analysis complements this by revealing network communication, runtime behaviour, SSL-pinning controls, logging and runtime data handling.

The most important lesson from this room is that a mobile application should never be considered secure simply because its UI and backend appear to work correctly.

A proper assessment requires looking underneath the application and systematically analysing its package, configuration, code, storage, communication and runtime behaviour.

Next Steps

Recommended next topics include:

Mobile Malware Analysis
OWASP Mobile Security Testing Guide
Android security testing
iOS security testing