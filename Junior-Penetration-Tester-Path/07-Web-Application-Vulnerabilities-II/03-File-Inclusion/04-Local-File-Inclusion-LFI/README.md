# Local File Inclusion (LFI)

## Overview

Local File Inclusion (LFI) is a web application vulnerability that occurs when an application allows user-controlled input to determine which local file is loaded by server-side functions such as `include()` or `require()`. Unlike simple Path Traversal, LFI causes the server to process the requested file through the application's execution logic, potentially leading to information disclosure or even remote code execution under certain conditions. :contentReference[oaicite:0]{index=0}

This lesson explains how Local File Inclusion vulnerabilities arise, demonstrates common implementation mistakes, and highlights the security risks associated with insecure server-side file handling. :contentReference[oaicite:1]{index=1}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Local File Inclusion (LFI) is
- Differentiate between Path Traversal and LFI
- Recognise common insecure file inclusion functions
- Understand how user-controlled file paths create security risks
- Identify secure coding practices that prevent LFI vulnerabilities

---

## Main Content

### What is Local File Inclusion?

Local File Inclusion occurs when a web application passes user-controlled input directly into a server-side file inclusion function.

Common PHP functions include:

- `include()`
- `require()`
- `include_once()`
- `require_once()`

If the supplied filename is not validated, the application may load unintended files from the local filesystem. :contentReference[oaicite:2]{index=2}

---

### LFI vs Path Traversal

Although closely related, LFI differs from traditional Path Traversal.

| Path Traversal | Local File Inclusion |
|----------------|----------------------|
| Reads arbitrary files | Loads files through server-side include functions |
| Returns file contents | Processes the file before returning output |
| Primarily causes information disclosure | May lead to code execution under certain conditions |

Because the included file is processed by the server, LFI often presents a greater security risk. :contentReference[oaicite:3]{index=3}

---

### Common Vulnerable Scenarios

LFI vulnerabilities frequently occur when applications use user input to determine which file should be loaded.

Examples include:

- Language selection
- Theme loading
- Templates
- Configuration files
- Dynamic page content

Without proper validation, attackers may supply arbitrary local file paths instead of the intended application files. :contentReference[oaicite:4]{index=4}

---

### Preventing Local File Inclusion

Applications should never allow direct user control over included file paths.

Recommended practices include:

- Use allowlists for permitted files
- Validate all user input
- Avoid passing raw input into include functions
- Restrict filesystem permissions
- Implement secure application architecture

These controls significantly reduce the risk of Local File Inclusion vulnerabilities.

---

## Skills Practiced

- Local File Inclusion (LFI)
- Secure File Handling
- Input Validation
- PHP File Inclusion
- Web Application Security

---

## Key Takeaways

- Local File Inclusion occurs when user-controlled input determines which local file is processed by server-side include functions.
- LFI is more dangerous than simple Path Traversal because included files are executed by the application rather than simply displayed.
- Insecure use of functions such as `include()` and `require()` can expose sensitive files or enable further attacks.
- Proper input validation, allowlists, and secure file handling are essential for preventing LFI vulnerabilities. :contentReference[oaicite:5]{index=5}