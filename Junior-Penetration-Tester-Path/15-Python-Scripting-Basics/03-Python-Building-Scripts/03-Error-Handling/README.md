# 03 - Error Handling

## Overview

When writing scripts, unexpected situations can cause a program to stop with an error.

Error handling allows me to anticipate these situations and handle them without allowing the entire program to crash.

Python uses `try` and `except` to catch exceptions.

---

## Basic try / except

The basic structure is:

~~~python
try:
    # code that may cause an error
except:
    # code executed if an error occurs
~~~

For example:

~~~python
try:
    number = int(input("Enter a number: "))
except:
    print("Invalid input.")
~~~

If the user enters something that cannot be converted into an integer, the program handles the error instead of crashing.

---

## Handling Specific Exceptions

Instead of catching every possible error, I can catch a specific exception.

~~~python
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Please enter a valid number.")
~~~

`ValueError` occurs when a value has the correct type but an inappropriate value for the operation.

For example:

~~~text
Enter a number: hello
        ↓
ValueError
        ↓
"Please enter a valid number."
~~~

---

## Multiple Exceptions

A program can handle different exceptions separately.

~~~python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
except ValueError:
    print("Please enter a valid number.")
except ZeroDivisionError:
    print("Cannot divide by zero.")
~~~

This allows the program to respond differently depending on what went wrong.

---

## else

The `else` block runs when no exception occurs.

~~~python
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Invalid input.")
else:
    print(f"You entered {number}.")
~~~

The flow is:

~~~text
try
  ↓
Error?
  ↓
YES → except
  ↓
NO
  ↓
else
~~~

---

## finally

The `finally` block runs whether an exception occurs or not.

~~~python
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Invalid input.")
finally:
    print("Finished.")
~~~

This is useful when there is code that should always execute.

---

## Raising Exceptions

I can also deliberately raise an exception using `raise`.

~~~python
age = -1

if age < 0:
    raise ValueError("Age cannot be negative.")
~~~

This allows a function or program to explicitly signal that something is invalid.

---

## Why Error Handling Matters

Without error handling, unexpected input can terminate a program.

For example:

~~~python
number = int(input("Enter a number: "))
~~~

If the user enters:

~~~text
hello
~~~

the program can crash with a `ValueError`.

With error handling:

~~~python
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Invalid number.")
~~~

the program can continue running normally.

---

## Error Handling Flow

~~~text
Program
    ↓
Potentially dangerous operation
    ↓
try
    ↓
Did an exception occur?
    ↓
YES ─────────→ except
                  ↓
             Handle error
                  ↓
               Continue
                  
NO ──────────→ else
                  ↓
             Normal execution
~~~

The `finally` block can be used when something must happen regardless of the result.

---

## Security Relevance

Error handling is important when writing security scripts because scripts often interact with unpredictable input and external resources.

Examples include:

~~~text
User Input
    ↓
Invalid values

Files
    ↓
Missing / inaccessible files

Network Connections
    ↓
Connection failures

HTTP Requests
    ↓
Unexpected responses

Command Execution
    ↓
Execution errors
~~~

A security script should fail in a controlled way instead of unexpectedly crashing.

---

## Example

A simple security-oriented example:

~~~python
target_port = input("Enter a port: ")

try:
    port = int(target_port)

    if port < 1 or port > 65535:
        raise ValueError("Port must be between 1 and 65535.")

    print(f"Valid port: {port}")

except ValueError as error:
    print(f"Invalid port: {error}")
~~~

This validates the input and handles invalid values without terminating unexpectedly.

---

## Key Takeaways

~~~text
try
    ↓
Code that may cause an exception

except
    ↓
Handle the exception

else
    ↓
Run when no exception occurs

finally
    ↓
Run regardless of the result

raise
    ↓
Manually trigger an exception
~~~

The main goal of error handling is to make scripts more predictable and resilient when something unexpected happens.