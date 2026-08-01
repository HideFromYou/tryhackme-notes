# Path Traversal

## Overview

Path Traversal, also known as Directory Traversal, is a web application vulnerability that allows attackers to access files and directories outside the intended application directory. It occurs when user-controlled input is incorporated into file paths without proper validation, allowing traversal sequences to navigate the server's filesystem.

This lesson introduces the fundamentals of Path Traversal, explains how directory traversal sequences work, demonstrates common attack scenarios, and discusses defensive techniques used to prevent unauthorised file access.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what a Path Traversal vulnerability is
- Explain how directory traversal attacks work
- Recognise common Path Traversal payloads
- Understand the security impact of arbitrary file access
- Identify secure coding practices that prevent Path Traversal vulnerabilities

---

## Main Content

### What is Path Traversal?

Path Traversal occurs when a web application allows user input to influence a file path without properly restricting where the application can access files.

Instead of remaining inside the intended directory, attackers may manipulate the path to reach other locations on the server's filesystem.

---

### Directory Traversal Sequences

Operating systems organise files using directory structures.

Traversal sequences allow navigation through these directories.

Examples include:

- `../` (Unix/Linux)
- `..\` (Windows)

When user input containing these sequences is not properly validated, the application may resolve paths outside its intended directory.

---

### Why Path Traversal Matters

Successful Path Traversal attacks may allow attackers to access sensitive resources such as:

- Configuration files
- Application source code
- Log files
- User data
- Operating system files

The impact depends on the permissions granted to the web application.

---

### Preventing Path Traversal

Applications should never allow users to directly control filesystem paths.

Recommended defensive practices include:

- Input validation
- Allowlists of permitted filenames
- Canonical path validation
- Restricting filesystem permissions
- Avoiding direct use of user-supplied file paths

Combining multiple layers of protection significantly reduces the risk of Path Traversal vulnerabilities.

---

## Skills Practiced

- Path Traversal
- Directory Traversal
- File System Security
- Input Validation
- Web Application Security

---

## Key Takeaways

- Path Traversal allows attackers to access files outside the intended application directory.
- Directory traversal sequences exploit insufficient validation of user-controlled file paths.
- Sensitive files may become accessible if applications improperly process filesystem paths.
- Strong input validation, allowlists, and secure filesystem design are essential for preventing Path Traversal vulnerabilities.