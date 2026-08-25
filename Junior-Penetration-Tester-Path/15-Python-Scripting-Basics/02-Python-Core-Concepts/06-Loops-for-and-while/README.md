# 06 - Loops: for and while

## Overview

The previous `Python: Simple Demo` room introduced the `while` loop.

In this lesson, I expanded my understanding of loops by working with:

- `for` loops
- `while` loops
- `range()`
- Iterating through strings
- Iterating through dictionaries
- `break`
- `continue`

Loops are important when I need to perform the same operation repeatedly, especially when processing security-related data.

---

## while Loop

A `while` loop repeatedly executes code while a condition remains `True`.

~~~python
attempts = 0
max_attempts = 3

while attempts < max_attempts:
    password = input("Enter password: ")
    attempts += 1
    print(f"Attempt {attempts} of {max_attempts}")
~~~

The loop continues while:

~~~python
attempts < max_attempts
~~~

Once the condition becomes `False`, the loop stops.

---

## for Loop

A `for` loop is useful when I want to iterate through a sequence of values.

For example, processing a list of IP addresses:

~~~python
targets = [
    "192.168.1.1",
    "192.168.1.2",
    "192.168.1.3"
]

for ip in targets:
    print(f"Scanning {ip}...")
~~~

Output:

~~~text
Scanning 192.168.1.1...
Scanning 192.168.1.2...
Scanning 192.168.1.3...
~~~

The variable `ip` takes the value of each item in the list one at a time.

---

## Iterating Through Strings

Strings are sequences, so I can also iterate through their characters.

~~~python
password = "S3cure!"

for char in password:
    if char.isdigit():
        print(f"Found digit: {char}")
    elif char.isupper():
        print(f"Found uppercase: {char}")
~~~

Output:

~~~text
Found uppercase: S
Found digit: 3
~~~

This can be useful for analysing password composition.

---

## range()

The `range()` function generates a sequence of numbers.

### `range(stop)`

~~~python
for i in range(5):
    print(i)
~~~

Output:

~~~text
0
1
2
3
4
~~~

The stop value is not included.

---

### `range(start, stop)`

~~~python
for i in range(1, 6):
    print(i)
~~~

Output:

~~~text
1
2
3
4
5
~~~

---

### `range(start, stop, step)`

~~~python
for i in range(0, 20, 5):
    print(i)
~~~

Output:

~~~text
0
5
10
15
~~~

The `step` value controls how much the number changes on each iteration.

---

## Iterating Through Dictionaries

Dictionaries can be processed using `.items()`.

~~~python
services = {
    22: "SSH",
    80: "HTTP",
    443: "HTTPS"
}

for port, name in services.items():
    print(f"Port {port} = {name}")
~~~

Output:

~~~text
Port 22 = SSH
Port 80 = HTTP
Port 443 = HTTPS
~~~

This is useful when processing relationships such as:

~~~text
Port → Service
Username → Information
IP → Hostname
~~~

---

## break

The `break` statement immediately terminates a loop.

Example:

~~~python
for port in [22, 80, 443, 8080]:
    if port == 443:
        print(f"Port {port} found. Stopping scan.")
        break

    print(f"Checked port {port}")
~~~

Output:

~~~text
Checked port 22
Checked port 80
Port 443 found. Stopping scan.
~~~

The loop stops as soon as port `443` is found.

---

## continue

The `continue` statement skips the current iteration and moves to the next one.

Example:

~~~python
lines = [
    "admin",
    "",
    "root",
    "",
    "guest"
]

for line in lines:
    if line == "":
        continue

    print(f"Processing: {line}")
~~~

Output:

~~~text
Processing: admin
Processing: root
Processing: guest
~~~

The empty values are skipped.

---

## for vs while

A useful way to think about the two loops is:

~~~text
for
    ↓
Iterate through a known sequence

while
    ↓
Repeat while a condition remains True
~~~

Examples:

~~~text
for
    ↓
IP addresses
Ports
Usernames
Passwords
Log entries
~~~

~~~text
while
    ↓
Retries
User input
Waiting for a condition
Repeated attempts
~~~

---

## Security Relevance

Loops are fundamental to security automation.

A list of targets can be processed automatically:

~~~text
IP Addresses
      ↓
for loop
      ↓
Process every target
~~~

A list of ports can be handled in the same way:

~~~text
Ports
      ↓
for loop
      ↓
Check each port
~~~

A condition-based operation can use `while`:

~~~text
Attempt
      ↓
Check condition
      ↓
Retry
      ↓
Check condition again
      ↓
Stop when condition changes
~~~

---

## Key Takeaways

~~~text
while
    Condition-based repetition

for
    Sequence-based iteration

range()
    Generate number sequences

break
    Exit the loop immediately

continue
    Skip the current iteration
~~~

The main idea is to choose the appropriate loop based on the task:

~~~text
Known collection
    ↓
for

Condition determines repetition
    ↓
while
~~~