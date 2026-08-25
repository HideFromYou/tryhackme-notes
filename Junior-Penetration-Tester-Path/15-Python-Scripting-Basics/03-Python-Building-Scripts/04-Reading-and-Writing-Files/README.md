# 04 - Reading and Writing Files

## Overview

Python scripts often need to read information from files and write results back to files.

File I/O allows a script to work with persistent data instead of keeping everything only in memory.

The main concepts covered are:

- Opening files
- Reading files
- Writing files
- Appending to files
- Using the `with` context manager
- Handling missing files with exceptions

---

## Opening a File

Python can open a file using `open()`.

~~~python
file = open("example.txt", "r")
~~~

The second argument specifies the mode.

Common modes are:

~~~text
r
    Read

w
    Write

a
    Append
~~~

---

## Reading a File

The `.read()` method reads the contents of a file.

~~~python
file = open("example.txt", "r")

content = file.read()

print(content)

file.close()
~~~

This reads the entire file into a string.

---

## Reading Line by Line

A file can also be processed one line at a time.

~~~python
file = open("usernames.txt", "r")

for line in file:
    print(line.strip())

file.close()
~~~

This is useful when working with files containing many entries.

For example:

~~~text
admin
root
guest
user
~~~

Each line can be processed individually.

---

## The `with` Context Manager

A safer and cleaner way to work with files is to use `with`.

~~~python
with open("example.txt", "r") as file:
    content = file.read()

print(content)
~~~

The file is automatically closed when the `with` block finishes.

This is preferable to manually calling:

~~~python
file.close()
~~~

---

## Reading a File With a Loop

A common pattern is:

~~~python
with open("usernames.txt", "r") as file:
    for line in file:
        username = line.strip()
        print(username)
~~~

The `.strip()` removes whitespace and the newline character from the end of each line.

---

## Writing to a File

The `w` mode opens a file for writing.

~~~python
with open("results.txt", "w") as file:
    file.write("Scan completed\n")
    file.write("Port 22: SSH\n")
    file.write("Port 80: HTTP\n")
~~~

The `w` mode creates the file if it does not exist.

If the file already exists, its previous contents are overwritten.

---

## Appending to a File

The `a` mode adds new content to the end of an existing file.

~~~python
with open("results.txt", "a") as file:
    file.write("Port 443: HTTPS\n")
~~~

Unlike `w`, append mode does not overwrite the existing contents.

---

## File Modes

The three main modes are:

~~~text
r
    Read existing content

w
    Write new content
    Existing content is overwritten

a
    Append content
    Existing content is preserved
~~~

Choosing the correct mode is important when working with security results and logs.

---

## Handling Missing Files

A file may not exist when the script tries to open it.

This can be handled using `try` / `except`.

~~~python
try:
    with open("common_passwords.txt", "r") as file:
        passwords = file.read()

except FileNotFoundError:
    print("File not found.")
~~~

Instead of crashing, the script can handle the problem and continue.

---

## Reading Data Into a List

Files containing one value per line can easily be converted into a list.

~~~python
passwords = []

with open("common_passwords.txt", "r") as file:
    for line in file:
        passwords.append(line.strip().lower())
~~~

The result is a list containing the values from the file.

For example:

~~~text
password
123456
admin
qwerty
~~~

can become:

~~~python
[
    "password",
    "123456",
    "admin",
    "qwerty"
]
~~~

---

## Security Relevance

File I/O is extremely useful in penetration-testing scripts.

Security tools commonly work with files containing:

~~~text
Wordlists
    ↓
Usernames
    ↓
Passwords
    ↓
Targets
    ↓
URLs
    ↓
Scan results
    ↓
Logs
~~~

For example, a script could read a list of targets:

~~~python
with open("targets.txt", "r") as file:
    for target in file:
        target = target.strip()
        print(f"Processing {target}")
~~~

This allows the same operation to be performed against multiple targets.

---

## Logging Results

File writing can also be used to store results.

~~~python
with open("scan_results.txt", "a") as log:
    log.write("192.168.1.10 - Port 80 open\n")
~~~

Using append mode is useful for logs because new results can be added without deleting previous entries.

---

## File I/O Flow

~~~text
File
    ↓
open()
    ↓
Read / Write / Append
    ↓
Process Data
    ↓
Close Automatically
~~~

When using `with`, Python handles the closing of the file automatically.

---

## Key Takeaways

~~~text
open()
    ↓
Open a file

r
    ↓
Read

w
    ↓
Write / overwrite

a
    ↓
Append

read()
    ↓
Read complete content

for line in file
    ↓
Process line by line

with
    ↓
Safely manage the file

FileNotFoundError
    ↓
Handle missing files
~~~

File I/O allows Python scripts to work with persistent data, wordlists, targets, results, and logs, making it an important component of practical security automation.