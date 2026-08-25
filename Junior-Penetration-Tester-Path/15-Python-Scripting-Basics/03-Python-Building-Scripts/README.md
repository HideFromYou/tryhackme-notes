# 03 - Python: Building Scripts

## Overview

This room focuses on moving from individual Python concepts into complete and practical scripts.

Building on the previous `Python: Core Concepts` room, I learned how to organise code into reusable functions, handle errors, work with files, use libraries, and combine these concepts into a complete Python program.

---

## Lessons Covered

- 01 - Introduction
- 02 - Functions
- 03 - Error Handling
- 04 - Reading and Writing Files
- 05 - Libraries and Pip
- 06 - Password Strength Checker
- 07 - Conclusion

---

## Main Concepts

The progression through the room is:

```text
Python Core Concepts
        ↓
Functions
        ↓
Error Handling
        ↓
File I/O
        ↓
Libraries
        ↓
Complete Python Script
```

---

## Functions

Functions allow me to organise code into reusable blocks.

```python
def function_name():
    # code
```

Functions can accept parameters:

```python
def greet(name):
    print(f"Hello, {name}")
```

and return values:

```python
def add_numbers(a, b):
    return a + b
```

Important concepts:

```text
def
    ↓
Define a function

Parameters
    ↓
Inputs accepted by the function

Arguments
    ↓
Values passed to the function

return
    ↓
Send a result back

Scope
    ↓
Control where variables are available
```

---

## Error Handling

Python provides exception handling so that unexpected situations can be handled without immediately crashing the program.

```python
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Invalid input.")
```

The main components are:

```text
try
    ↓
Code that may generate an exception

except
    ↓
Handle the exception

else
    ↓
Execute when no exception occurs

finally
    ↓
Execute regardless of the result

raise
    ↓
Manually generate an exception
```

---

## File I/O

Python can read and write files.

The main file modes are:

```text
r
    ↓
Read

w
    ↓
Write / overwrite

a
    ↓
Append
```

A safe way to work with files is:

```python
with open("example.txt", "r") as file:
    content = file.read()
```

Files can also be processed line by line:

```python
with open("targets.txt", "r") as file:
    for line in file:
        target = line.strip()
        print(target)
```

This is useful for working with:

```text
Wordlists
Targets
Usernames
Passwords
Logs
Scan results
```

---

## Libraries and pip

Python provides a large collection of existing modules that can be imported into scripts.

Examples:

```python
import os
import string
import hashlib
```

Third-party packages can be installed using `pip`:

```bash
pip install requests
```

The basic workflow is:

```text
Need functionality
        ↓
Find appropriate library
        ↓
Install if necessary
        ↓
Import it
        ↓
Use it in the script
```

---

## Security-Relevant Libraries

Some libraries that can be useful when developing security scripts include:

```text
requests
    ↓
HTTP requests

scapy
    ↓
Network packets

paramiko
    ↓
SSH

hashlib
    ↓
Hashing

beautifulsoup4
    ↓
HTML parsing
```

The important skill is understanding when existing functionality can be reused instead of implementing everything from scratch.

---

## Password Strength Checker

The final project combines the concepts covered throughout the room.

The program:

```text
Load common passwords
        ↓
Ask the user for a password
        ↓
Check password length
        ↓
Check character composition
        ↓
Check common-password list
        ↓
Calculate score
        ↓
Assign strength
        ↓
Display feedback
        ↓
Write result to a log
```

The project combines:

```text
Variables
Lists
Dictionaries
Strings
Conditionals
Loops
Functions
Error Handling
File I/O
Libraries
```

---

## Password Scoring

The password checker evaluates several characteristics:

```text
Length >= 8
    ↓
+1

Length >= 12
    ↓
+1

Uppercase character
    ↓
+1

Digit
    ↓
+1

Special character
    ↓
+1
```

Maximum score:

```text
5/5
```

If the password is found in the common-password list, the score is reset to:

```text
0/5
```

---

## Logging

The final script writes the result to a log file.

The password itself should not be stored in plaintext.

Instead of:

```text
Password: C0mpl3x!Pass#99
```

the log uses masking:

```text
Password: **************
```

This demonstrates an important security principle:

```text
Sensitive Data
      ↓
Avoid unnecessary plaintext storage
```

---

## Security Scripting Progression

The Python rooms build progressively:

```text
Python: Simple Demo
        ↓
Basic Python Syntax
        ↓
Python: Core Concepts
        ↓
Data + Operators + Loops
        ↓
Python: Building Scripts
        ↓
Functions + Error Handling + Files + Libraries
        ↓
Complete Python Scripts
        ↓
Security Automation
```

---

## Main Takeaway

The main transition in this room is:

```text
"I understand Python concepts"
            ↓
"I can combine Python concepts"
            ↓
"I can build complete Python scripts"
```

The skills from this room provide the foundation for applying Python directly to cybersecurity and penetration-testing tasks.