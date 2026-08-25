# 05 - Libraries and Pip

## Overview

Python's strength comes partly from its ecosystem of pre-written code.

Instead of implementing everything from scratch, I can import existing libraries and use functionality that has already been built.

In the previous `Python: Simple Demo` room, I already used:

~~~python
import random
~~~

This allowed me to use:

~~~python
random.randint()
~~~

without having to implement random number generation myself.

---

## What Is a Library?

A library is a collection of pre-written code that can be imported into my own programs.

The basic idea is:

~~~text
My Script
    ↓
Import Library
    ↓
Use Existing Functionality
    ↓
Build Faster
~~~

This prevents me from having to reinvent functionality that already exists.

---

## Importing Libraries

Python provides several ways to import code.

### Import an Entire Library

~~~python
import os

print(os.getcwd())
~~~

This imports the `os` module and allows me to access its functions using:

~~~text
os.function()
~~~

---

## Import a Specific Function

I can import only a specific function from a module.

~~~python
from datetime import datetime

now = datetime.now()

print(f"Current time: {now}")
~~~

---

## Import With an Alias

I can also give a module a shorter name using `as`.

~~~python
import datetime as dt

now = dt.datetime.now()

print(now)
~~~

This can make code shorter when a module name is used repeatedly.

---

## Python Standard Library

Python includes a large collection of modules that are available without installing anything.

Some useful examples are:

| Module | Purpose | Example Use |
|---|---|---|
| `os` | Operating system interaction | Files, environment variables |
| `sys` | System-specific functionality | Command-line arguments |
| `random` | Random values | Random numbers, selecting items |
| `datetime` | Dates and times | Timestamps, time calculations |
| `json` | JSON data | API responses, configuration files |
| `hashlib` | Cryptographic hashing | MD5, SHA-256 |
| `string` | String constants | Characters, digits, punctuation |

---

## The `string` Module

The `string` module is particularly useful for the Password Strength Checker.

It provides constants such as:

~~~python
string.ascii_uppercase
string.digits
string.punctuation
~~~

Instead of manually creating lists of uppercase characters, digits, or special characters, I can use these predefined values.

---

## Password Character Checks

For example:

~~~python
import string

password = "S3cure!Pass"

has_upper = any(c in string.ascii_uppercase for c in password)
has_digit = any(c in string.digits for c in password)
has_special = any(c in string.punctuation for c in password)

print(f"Uppercase: {has_upper}")
print(f"Digit: {has_digit}")
print(f"Special: {has_special}")
~~~

Output:

~~~text
Uppercase: True
Digit: True
Special: True
~~~

This combines:

~~~text
Library
    ↓
string constants
    ↓
any()
    ↓
Character checks
~~~

---

## Third-Party Libraries

Python also has thousands of community-built libraries available through the **Python Package Index (PyPI)**.

These are installed using `pip`, Python's package manager.

For example:

~~~bash
pip install requests
~~~

After installation, the library can be imported:

~~~python
import requests
~~~

And used:

~~~python
response = requests.get("https://tryhackme.com")

print(response.status_code)
~~~

---

## Standard Library vs Third-Party Library

The main distinction is:

~~~text
Standard Library
    ↓
Included with Python
    ↓
Usually no installation required

Third-Party Library
    ↓
Created outside the Python core distribution
    ↓
Install with pip when required
~~~

---

## Security-Relevant Libraries

As I progress through the Jr Penetration Tester path, I will encounter libraries that are useful for penetration testing.

### requests

Used for sending HTTP requests.

~~~text
Web requests
API interaction
Web scraping
~~~

### scapy

Used for working with network packets.

~~~text
Craft packets
Send packets
Sniff packets
~~~

### pwntools

A toolkit commonly used for CTFs and binary exploitation.

### paramiko

Provides SSH functionality.

### beautifulsoup4

Used to parse and extract information from HTML.

---

## Important Point

I do not need to memorise every library or function immediately.

The important concept is understanding that Python has a large ecosystem of existing functionality.

Instead of implementing everything myself:

~~~text
"I need to send an HTTP request"
        ↓
Find the appropriate library
        ↓
Import it
        ↓
Use its functionality
~~~

This allows security scripts to perform complex tasks with relatively little code.

---

## hashlib

The `hashlib` module provides hashing functionality.

For example, SHA-256 can be calculated using:

~~~python
import hashlib

data = "hello"

hash_value = hashlib.sha256(data.encode()).hexdigest()

print(hash_value)
~~~

Changing the input produces a completely different hash.

This is useful when working with cryptographic hashes in security scripts.

---

## Practical Exercise

The VM contains:

~~~text
imports_demo.py
~~~

The script demonstrates imports from:

~~~text
os
datetime
string
hashlib
~~~

Running the script allows me to observe how these modules work.

The exercise also demonstrates how `hashlib` calculates a SHA-256 hash.

Changing the input string and running the script again shows how dramatically the resulting hash changes.

---

## Security Relevance

Libraries are essential when building penetration-testing tools.

Instead of implementing network protocols, cryptographic functions, SSH communication, or HTTP handling from scratch, I can use existing libraries.

This allows me to focus on:

~~~text
Reconnaissance
    ↓
Enumeration
    ↓
Analysis
    ↓
Automation
    ↓
Exploitation
~~~

while using Python libraries for the underlying technical functionality.

---

## Key Takeaways

~~~text
import
    ↓
Import an entire module

from ... import ...
    ↓
Import specific functionality

as
    ↓
Create an alias

Standard Library
    ↓
Built into Python

pip
    ↓
Install third-party packages

PyPI
    ↓
Repository of Python packages
~~~

The most important idea is that Python's ecosystem allows me to build useful security scripts without implementing every piece of functionality from scratch.