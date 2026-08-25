# 03 - Working with Strings

## Overview

Strings are one of the most commonly used data types in Python.

In security scripting, I will constantly work with text such as:

- Usernames
- Passwords
- URLs
- File names
- HTTP responses
- Logs
- Command output

Understanding how to manipulate strings is therefore an important part of writing useful security scripts.

---

## Creating Strings

Strings can be created using single or double quotation marks.

~~~python
username = "admin"
password = 'password123'
~~~

Triple quotes can also be used for multi-line strings:

~~~python
message = """This is
a multi-line
string."""
~~~

---

## String Length

The `len()` function returns the number of characters in a string.

~~~python
password = "Tr0ub4dor"

length = len(password)

print(length)
~~~

Output:

~~~text
9
~~~

This can be useful when checking input such as password length.

---

## String Indexing

Strings are sequences of characters.

Python uses zero-based indexing, meaning the first character is at index `0`.

For example:

~~~python
word = "Python"
~~~

The indexes are:

~~~text
P  y  t  h  o  n
0  1  2  3  4  5
~~~

Individual characters can be accessed using their index:

~~~python
print(word[0])
print(word[3])
~~~

Output:

~~~text
P
h
~~~

---

## Negative Indexing

Negative indexes allow me to access characters starting from the end of a string.

~~~python
word = "Python"

print(word[-1])
print(word[-2])
~~~

Output:

~~~text
n
o
~~~

So:

~~~text
-1 → Last character
-2 → Second-to-last character
~~~

---

## String Slicing

Slicing allows me to extract part of a string.

The basic syntax is:

~~~python
string[start:end]
~~~

The start index is included, while the end index is excluded.

Example:

~~~python
word = "Python"

print(word[0:3])
~~~

Output:

~~~text
Pyt
~~~

Other examples:

~~~python
print(word[2:])
print(word[:4])
~~~

Output:

~~~text
thon
Pyth
~~~

---

## Useful String Methods

Python provides many built-in methods for manipulating strings.

### `.upper()`

Converts a string to uppercase.

~~~python
"hello".upper()
~~~

Result:

~~~text
HELLO
~~~

### `.lower()`

Converts a string to lowercase.

~~~python
"HELLO".lower()
~~~

Result:

~~~text
hello
~~~

### `.strip()`

Removes whitespace from the beginning and end of a string.

~~~python
"  admin  ".strip()
~~~

Result:

~~~text
admin
~~~

### `.replace()`

Replaces one value with another.

~~~python
"hello world".replace("world", "python")
~~~

Result:

~~~text
hello python
~~~

### `.split()`

Splits a string into a list.

~~~python
ports = "22,80,443"

print(ports.split(","))
~~~

Output:

~~~text
['22', '80', '443']
~~~

### `.startswith()`

Checks whether a string starts with a specific value.

~~~python
url = "https://tryhackme.com"

print(url.startswith("https"))
~~~

Output:

~~~text
True
~~~

### `.endswith()`

Checks whether a string ends with a specific value.

~~~python
filename = "passwords.txt"

print(filename.endswith(".txt"))
~~~

Output:

~~~text
True
~~~

### `.count()`

Counts how many times a value appears.

~~~python
text = "banana"

print(text.count("a"))
~~~

Output:

~~~text
3
~~~

---

## Character Checking Methods

Python also provides methods for checking the contents of individual characters or strings.

~~~python
char = "A"

print(char.isupper())
print(char.islower())
print(char.isdigit())
print(char.isalpha())
print(char.isalnum())
~~~

Output:

~~~text
True
False
False
True
True
~~~

These methods return Boolean values, so they can be used directly inside conditions.

---

## Searching With `in`

The `in` operator can check whether one string exists inside another.

~~~python
url = "https://tryhackme.com/room/pythoncoreconcepts"

print("tryhackme" in url)
print("hackthebox" in url)
~~~

Output:

~~~text
True
False
~~~

This can be useful when searching command output, URLs, logs, or HTTP responses for specific keywords.

---

## Strings and Security

String manipulation is particularly important when writing security scripts.

For example:

~~~text
HTTP Response
      ↓
String
      ↓
Search for keyword
      ↓
Extract interesting information
      ↓
Process result
~~~

Another example:

~~~text
Password
    ↓
len()
    ↓
Check length

Password
    ↓
isdigit()
isupper()
isalpha()
    ↓
Check character composition
~~~

---

## Key Takeaways

~~~text
len()
    ↓
Find string length

Indexing
    ↓
Access individual characters

Slicing
    ↓
Extract part of a string

.upper()
.lower()
    ↓
Change case

.strip()
    ↓
Remove surrounding whitespace

.replace()
    ↓
Replace text

.split()
    ↓
Convert text into a list

.startswith()
.endswith()
    ↓
Check beginning / end

.count()
    ↓
Count occurrences

.isupper()
.islower()
.isdigit()
.isalpha()
.isalnum()
    ↓
Check character content

in
    ↓
Search for text
~~~

Strings are one of the most important building blocks for processing data in Python and will be heavily used in practical security scripts.