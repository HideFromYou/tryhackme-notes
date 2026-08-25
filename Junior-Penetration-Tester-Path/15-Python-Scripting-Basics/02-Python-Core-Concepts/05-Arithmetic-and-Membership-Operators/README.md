# 05 - Arithmetic and Membership Operators

## Overview

This lesson expands my understanding of Python operators.

The main focus is on:

- Arithmetic operators
- Membership operators
- Using operators together with conditions

These operators are useful when performing calculations, comparing values, and checking whether specific data exists inside a collection.

---

## Arithmetic Operators

The basic arithmetic operators are:

~~~text
+    Addition
-    Subtraction
*    Multiplication
/    Division
~~~

Additional operators include:

~~~text
**   Exponent
//   Floor Division
%    Modulus
~~~

---

## Exponent

The `**` operator raises a number to a power.

~~~python
2 ** 8
~~~

Result:

~~~text
256
~~~

Another example:

~~~python
2 ** 10
~~~

Result:

~~~text
1024
~~~

---

## Floor Division

The `//` operator performs division and returns the result rounded down to the nearest whole number.

~~~python
7 // 2
~~~

Result:

~~~text
3
~~~

Normal division:

~~~python
7 / 2
~~~

returns:

~~~text
3.5
~~~

---

## Modulus

The `%` operator returns the remainder after division.

~~~python
7 % 2
~~~

Result:

~~~text
1
~~~

The modulus operator can also be used to determine whether a number is even or odd.

~~~python
number = 10

if number % 2 == 0:
    print("Even")
~~~

---

## Membership Operators

Python provides the `in` and `not in` operators for checking whether a value exists inside a collection.

~~~text
in
    ↓
Value exists

not in
    ↓
Value does not exist
~~~

---

## `in`

For example, I can check whether a password exists in a list of common passwords:

~~~python
common_passwords = [
    "123456",
    "password",
    "qwerty",
    "letmein"
]

user_password = "qwerty"

if user_password in common_passwords:
    print("This password is too common.")
~~~

The condition becomes `True` because `"qwerty"` exists in the list.

---

## `not in`

The opposite check can be performed with `not in`:

~~~python
if user_password not in common_passwords:
    print("Password is not in the common list.")
~~~

This becomes `True` when the value does not exist in the collection.

---

## Combining Operators

Operators can be combined with conditions to create more useful logic.

For example, I can check whether a password meets basic requirements:

~~~python
password = "Tr0ub4dor"

length = len(password)
has_digit = any(char.isdigit() for char in password)

if length >= 8 and has_digit:
    print("Moderate strength")
elif length >= 8 or has_digit:
    print("Weak, but has some merit")
else:
    print("Very weak")
~~~

Here I am combining:

~~~text
len()
    ↓
Measure string length

>=
    ↓
Compare the length

isdigit()
    ↓
Check for a digit

and / or
    ↓
Combine conditions
~~~

---

## Security Relevance

These operators can be useful when writing security scripts.

Examples include:

~~~text
Password validation
        ↓
Input validation
        ↓
Wordlist checking
        ↓
Number calculations
        ↓
Processing security data
~~~

For example, when working with a password list:

~~~python
passwords = ["123456", "password", "admin"]

if "admin" in passwords:
    print("Found admin password candidate")
~~~

This basic concept can later be expanded into scripts that process much larger datasets.

---

## Key Takeaways

~~~text
**
    Exponent

//
    Floor Division

%
    Remainder

in
    Check whether a value exists

not in
    Check whether a value does not exist

and
    Both conditions must be True

or
    At least one condition must be True
~~~

The important idea is that operators allow me to calculate values, compare information, and make decisions based on data.