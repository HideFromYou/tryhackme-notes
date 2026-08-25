# 02 - Quick Review: Hello World, Variables, and Conditionals

## Overview

This lesson is a quick review of the Python fundamentals introduced in the previous `Python: Simple Demo` room.

The focus is on revisiting:

- `print()`
- Comments
- Variables
- Data types
- Conditional statements
- Comparison operators
- Logical operators

It also introduces some useful additions:

- Type conversion
- f-strings
- Augmented assignment

---

## Hello World

The `print()` function is used to output information to the screen.

~~~python
# This is a comment.
print("Hello World")
~~~

Comments begin with `#` and are ignored by Python.

Strings can be written using single or double quotation marks:

~~~python
"hello"
'hello'
~~~

---

## Variables

Variables are used to store information.

~~~python
food = "ice cream"
money = 2000
~~~

Variables can also be updated:

~~~python
age = 30
age = age + 1

print(age)
~~~

Output:

~~~text
31
~~~

---

## Data Types

Some of the main Python data types are:

~~~text
str
    String

int
    Integer

float
    Floating-point number

bool
    Boolean

list
    List of values
~~~

Examples:

~~~python
username = "admin"
port = 443
version = 1.5
active = True
ports = [22, 80, 443]
~~~

---

## Checking Data Types

Python provides the `type()` function to identify the type of a value.

~~~python
username = "admin"
port = 8080

print(type(username))
print(type(port))
~~~

Output:

~~~text
<class 'str'>
<class 'int'>
~~~

---

## Conditional Statements

Conditional statements allow the program to make decisions.

The basic structure is:

~~~python
if condition:
    # code

elif condition:
    # code

else:
    # code
~~~

Example:

~~~python
age = 18

if age < 17:
    print("You are NOT old enough to drive")
else:
    print("You are old enough to drive")
~~~

---

## Comparison Operators

The main comparison operators are:

~~~text
==    Equal to
!=    Not equal to
<     Less than
>     Greater than
<=    Less than or equal to
>=    Greater than or equal to
~~~

These operators return a Boolean value:

~~~text
True
False
~~~

---

## Logical Operators

Multiple conditions can be combined using logical operators.

~~~text
and
or
not
~~~

Example:

~~~python
name = "bob"
hungry = True

if name == "bob" and hungry == True:
    print("Bob is hungry")
elif name == "bob" and not hungry:
    print("Bob is not hungry")
else:
    print("Not sure who this is or if they are hungry")
~~~

---

## `=` vs `==`

An important distinction is:

~~~text
=     Assignment
==    Comparison
~~~

For example:

~~~python
x = 5
~~~

assigns the value `5` to `x`.

While:

~~~python
x == 5
~~~

checks whether `x` is equal to `5`.

---

## Type Conversion

The `input()` function returns a string.

For example:

~~~python
text = input("Enter a port number: ")
~~~

Even if the user enters:

~~~text
443
~~~

the value is initially treated as:

~~~text
"443"
~~~

To convert it into an integer:

~~~python
port = int(text)
~~~

Common conversion functions include:

~~~python
int("42")
float("3.14")
str(42)
bool(0)
~~~

---

## f-Strings

f-strings provide a convenient way to insert variables into strings.

Instead of:

~~~python
print("User", username, "is on port", port)
~~~

I can use:

~~~python
print(f"User {username} is on port {port}")
~~~

Example:

~~~python
username = "admin"
port = 443

print(f"User {username} is on port {port}")
~~~

Output:

~~~text
User admin is on port 443
~~~

---

## Augmented Assignment

Python provides shorter ways to update variables.

Instead of:

~~~python
count = count + 1
~~~

I can use:

~~~python
count += 1
~~~

Other examples:

~~~python
count -= 1
count *= 2
count /= 4
~~~

These are useful when working with counters and calculations.

---

## Key Takeaways

This lesson refreshed the Python fundamentals from the previous room:

~~~text
print()
    ↓
Output

Variables
    ↓
Store data

Data Types
    ↓
Describe stored data

if / elif / else
    ↓
Make decisions

Comparison Operators
    ↓
Compare values

Logical Operators
    ↓
Combine conditions
~~~

It also introduced:

~~~text
Type Conversion
    ↓
Convert between data types

f-Strings
    ↓
Format output

Augmented Assignment
    ↓
Update variables more efficiently
~~~