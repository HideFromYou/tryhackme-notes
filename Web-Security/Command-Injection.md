# Command Injection Notes

## Overview

Command Injection is a vulnerability where unsanitized user-controlled input is passed into operating system commands, allowing an attacker to execute arbitrary commands on the underlying server.

---

## Example Vulnerable Scenario

A web application allowed users to test the availability of a device by entering an IP address.

Example backend concept:

ping USER_INPUT

If the application executes input directly without validation, attacker-controlled commands may be appended.

Example:

127.0.0.1 ; whoami

Resulting execution:

ping 127.0.0.1 ; whoami

This executed the intended ping command followed by an attacker-controlled command.

---

## Practical Lab Exercise

Hands-on example completed:

Initial enumeration:

127.0.0.1 ; whoami

Purpose:
Identify the operating system user executing backend commands.

Flag retrieval example:

127.0.0.1 ; cat /home/tryhackme/flag.txt

Purpose:
Demonstrate arbitrary command execution and file access through command injection.

---

## Potential Impact

- Arbitrary OS command execution
- Information disclosure
- Sensitive file access
- User enumeration
- Privilege escalation opportunities
- Reverse shell possibilities

---

## Common Testing Concepts

Linux separators:

- ;
- &&
- |

Windows separators:

- &
- &&

---

## Key Learning

Main lesson:

User input should never be passed directly into shell commands without proper validation, sanitization, or safer implementation methods.

Payload construction may vary depending on operating system and application behavior.
