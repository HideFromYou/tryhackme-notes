# 01 - Introduction

## Overview

Introduction to Active Directory lateral movement.

The room begins with a compromised Linux WebServer and
introduces the techniques required to move from one
compromised host to other systems inside an Active
Directory environment.

## Topics Covered

- Lateral Movement
- Remote Execution
- Credential Reuse
- Pass-the-Hash
- Pivoting
- Valid Credentials
- NTLM Hashes
- Kerberos Tickets
- Network Segmentation

## Starting Point

The initial foothold is a compromised WebServer.

The objective is to use available credentials and access
to move through the internal network and eventually reach
the Domain Controller.

## Core Techniques

The room focuses on three main lateral movement techniques:

    Remote Execution
          ↓
    Credential Reuse
          ↓
    Pivoting

## Main Tools

- Impacket
- NetExec
- Evil-WinRM
- SSH
- Mimikatz
- Rubeus
- Chisel
- Ligolo-ng

## Key Takeaway

Lateral movement is the process of moving from one
compromised host to another using valid authentication
material.

The overall objective is to turn an initial foothold into
access to higher-value systems.