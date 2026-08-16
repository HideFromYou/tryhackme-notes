# How Mobile Applications Work

## Application Package

A mobile application is a structured package rather than a single file.

A package contains:

- Compiled application code
- Manifest or configuration file
- Resources
- Assets
- Images
- Fonts
- Local databases
- Stored strings

The application package is the starting point for static analysis.

## Manifest / Configuration File

The manifest or configuration file declares information about the application to the operating system.

It can contain:

- Application name
- Version
- Requested permissions
- Component configuration
- Component accessibility

From a security testing perspective, the manifest is important because it can reveal:

- Over-requested permissions
- Unnecessarily exposed components
- Insecure configuration

## Sandbox Model

Mobile operating systems use a sandbox to isolate applications.

Each application normally runs inside its own container and cannot directly access another application's files or processes.

The sandbox limits the impact of a compromised application.

A weakened application configuration or a sandbox escape can therefore become an important security finding.

## Application Components

Mobile applications consist of distinct components.

Components can:

- Display information
- Run in the background
- Respond to system events
- Provide data to other applications

Components may be internal or exported.

An exported component that was not intended to be accessible by other applications represents an attack surface.

## Why Package Structure Matters

Understanding the package structure helps a tester know where to look:

- Manifest → permissions and configuration
- Compiled code → application logic
- Resources → strings and potentially sensitive values
- Assets → databases and other bundled files

This knowledge makes static analysis systematic and repeatable.

## Key Takeaway

Understanding what exists inside a mobile application package is the foundation for effective mobile security testing.