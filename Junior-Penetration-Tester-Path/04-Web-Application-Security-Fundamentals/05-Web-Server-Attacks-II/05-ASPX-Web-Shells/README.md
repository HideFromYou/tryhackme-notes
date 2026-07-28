# ASPX Web Shells

## Overview

ASPX is the primary server-side technology used by ASP.NET applications hosted on Microsoft IIS. Understanding how IIS processes ASPX files helps security professionals recognise why executable content requires strict access controls and secure configuration.

This lesson focuses on the role of ASPX files within IIS and the security implications of allowing executable content inside web-accessible directories.

---

## Learning Objectives

- Understand ASPX applications
- Learn how IIS processes ASPX files
- Recognise executable server-side content
- Understand execution contexts
- Identify secure deployment principles

---

## What is ASPX?

ASPX files contain server-side code that is executed by the ASP.NET runtime before content is returned to the client.

Unlike static HTML files, ASPX pages can:

- Process user input
- Access databases
- Execute application logic
- Generate dynamic responses

---

## IIS Processing

When an ASPX file is requested, IIS passes the request to the ASP.NET framework rather than serving the file as static content.

This execution model allows dynamic applications while requiring careful configuration of executable directories.

---

## Application Pools

ASP.NET applications typically execute inside an IIS Application Pool.

Application Pools provide:

- Process isolation
- Resource management
- Permission separation
- Improved stability

The permissions assigned to an Application Pool influence what the hosted application can access.

---

## Security Considerations

Administrators should ensure:

- Upload directories cannot execute server-side code
- Application permissions follow least privilege
- Executable content is restricted
- Sensitive files remain outside publicly accessible locations

Proper separation between uploaded files and executable applications is a key security control.

---

## Skills Practiced

- ASP.NET architecture
- IIS execution model
- Application Pool concepts
- Web application security
- Configuration assessment

---

## Key Takeaways

- ASPX files are executed by the ASP.NET runtime.
- IIS distinguishes between static and executable content.
- Application Pools isolate hosted applications.
- Upload directories should never execute server-side code.
- Secure configuration greatly reduces unnecessary risk.