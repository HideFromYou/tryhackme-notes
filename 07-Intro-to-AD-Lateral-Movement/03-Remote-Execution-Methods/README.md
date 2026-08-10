# 03 - Remote Execution Methods

## Overview

This task focused on remote command execution as a method
of lateral movement.

The main hands-on techniques were PsExec and Evil-WinRM,
with additional Windows remote execution methods covered
as reference.

## Topics Covered

- PsExec
- Impacket
- SMB
- ADMIN$
- Service Control Manager
- Windows Services
- SYSTEM
- WinRM
- Evil-WinRM
- WMI
- DCOM
- SMBExec
- AtExec
- NetExec

## Requirements

Most remote execution methods require administrative
access on the target host.

Before attempting execution, access can be verified
with NetExec.

Example:

    nxc smb <TARGET_IP> -u <USERNAME> -p '<PASSWORD>' -d <DOMAIN>

A successful administrative login may display:

    Pwn3d!

## PsExec

PsExec uses SMB to upload and execute a service on the
target system.

The general process is:

    Authenticate over SMB
          ↓
    Access ADMIN$
          ↓
    Upload Service Binary
          ↓
    Create Windows Service
          ↓
    Start Service
          ↓
    Obtain SYSTEM Shell

Example:

    psexec.py <DOMAIN>/<USER>:'<PASSWORD>'@<TARGET_IP>

## How PsExec Works

1. Authenticate to SMB on port 445.
2. Access the IPC$ share.
3. Connect to ADMIN$.
4. Upload a service executable.
5. Connect to the Service Control Manager.
6. Create a service.
7. Start the service.
8. Redirect input/output through named pipes.
9. Receive a SYSTEM shell.

## Why PsExec Is Noisy

PsExec leaves several detectable indicators:

- File written to ADMIN$
- New Windows service
- Service execution
- Event ID 7045
- Named pipe activity

## Evil-WinRM

WinRM provides remote PowerShell access over HTTP/HTTPS.

Evil-WinRM can establish an interactive PowerShell
session using valid credentials.

Example:

    evil-winrm -i <TARGET_IP> -u <USERNAME> -p '<PASSWORD>'

WinRM is useful because it provides a PowerShell session
without requiring the same service-creation mechanism
used by PsExec.

## Other Remote Execution Methods

### WMI

WMI can be used to execute commands remotely through
Windows Management Instrumentation.

Impacket:

    wmiexec.py

### DCOM

Distributed Component Object Model can provide another
remote execution path.

Impacket:

    dcomexec.py

### SMBExec

SMBExec uses SMB and Windows services for remote execution.

Impacket:

    smbexec.py

### AtExec

Scheduled tasks can be abused for remote command execution.

Impacket:

    atexec.py

## Comparison

| Method | Main Protocol | Typical Mechanism |
|---|---|---|
| PsExec | SMB | Service creation |
| Evil-WinRM | WinRM | PowerShell session |
| WMIExec | WMI/RPC | WMI execution |
| DCOMExec | DCOM/RPC | DCOM execution |
| SMBExec | SMB | Service execution |
| AtExec | SMB/RPC | Scheduled task |

## Key Takeaways

Remote execution allows valid credentials with sufficient
privileges to become interactive access on another host.

The choice of technique depends on:

- Available protocols
- Required privileges
- Network connectivity
- Detection considerations
- Desired level of interaction