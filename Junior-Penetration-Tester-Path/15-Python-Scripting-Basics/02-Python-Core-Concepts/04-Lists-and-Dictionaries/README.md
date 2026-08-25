# 04 - Lists and Dictionaries

## Overview

When writing Python scripts, I often need to work with collections of related data.

Two important Python data structures for this are:

- Lists
- Dictionaries

These are especially useful in security scripting for storing things such as IP addresses, ports, usernames, services, and other collected information.

---

## Lists

A list stores multiple values in an ordered collection.

Lists use square brackets:

~~~python
ports = [22, 80, 443, 8080]

usernames = ["admin", "root", "guest"]
~~~

A list can also contain different data types:

~~~python
data = ["server1", 443, True]
~~~

---

## Accessing List Elements

Lists use zero-based indexing.

For example:

~~~python
ports = [22, 80, 443, 8080]

print(ports[0])
print(ports[2])
~~~

Output:

~~~text
22
443
~~~

Negative indexes can be used to access values from the end:

~~~python
print(ports[-1])
~~~

Output:

~~~text
8080
~~~

---

## List Slicing

Lists can also be sliced.

~~~python
ports = [22, 80, 443, 8080]

print(ports[1:3])
~~~

Output:

~~~text
[80, 443]
~~~

The same slicing concept used with strings applies to lists.

---

## Modifying Lists

Individual elements can be changed using their index.

~~~python
ports = [22, 80, 443]

ports[0] = 2222

print(ports)
~~~

Output:

~~~text
[2222, 80, 443]
~~~

---

## Adding Elements

`.append()` adds an item to the end of a list.

~~~python
ports = [22, 80, 443]

ports.append(8080)

print(ports)
~~~

Result:

~~~text
[22, 80, 443, 8080]
~~~

---

## Removing Elements

`.remove()` removes a specific value.

~~~python
ports.remove(80)
~~~

`.pop()` removes an item using its index and returns it.

~~~python
ports.pop(0)
~~~

---

## Sorting and Reversing

`.sort()` sorts the list:

~~~python
ports.sort()
~~~

`.reverse()` reverses the order:

~~~python
ports.reverse()
~~~

The length of a list can be found using:

~~~python
len(ports)
~~~

---

## Checking List Membership

The `in` operator can check whether a value exists in a list.

~~~python
common_passwords = [
    "123456",
    "password",
    "admin",
    "letmein"
]

if "password" in common_passwords:
    print("Password found in list")
~~~

This is useful when comparing collected information against known values.

---

# Dictionaries

A dictionary stores information as **key-value pairs**.

Dictionaries use curly brackets:

~~~python
services = {
    22: "SSH",
    80: "HTTP",
    443: "HTTPS",
    3306: "MySQL"
}
~~~

The key is used to retrieve its corresponding value.

---

## Accessing Dictionary Values

~~~python
print(services[22])
print(services[443])
~~~

Output:

~~~text
SSH
HTTPS
~~~

This makes dictionaries useful when I want to associate one piece of information with another.

For example:

~~~text
22   → SSH
80   → HTTP
443  → HTTPS
3306 → MySQL
~~~

---

## Adding Entries

A new key-value pair can be added directly:

~~~python
services[8080] = "HTTP-Alt"
~~~

---

## Updating Entries

An existing value can be changed using its key:

~~~python
services[22] = "OpenSSH"
~~~

---

## Removing Entries

An entry can be removed using `del`:

~~~python
del services[3306]
~~~

---

## Checking Dictionary Keys

The `in` operator can be used to check whether a key exists.

~~~python
if 22 in services:
    print(f"Port 22 runs {services[22]}")
~~~

---

## Dictionary Methods

### `.keys()`

Returns the dictionary's keys.

~~~python
services.keys()
~~~

### `.values()`

Returns the dictionary's values.

~~~python
services.values()
~~~

### `.items()`

Returns key-value pairs.

~~~python
services.items()
~~~

### `.get()`

Retrieves a value while allowing a default value if the key does not exist.

~~~python
service = services.get(9999, "Unknown")

print(service)
~~~

Output:

~~~text
Unknown
~~~

---

## Lists vs Dictionaries

The main difference is how I access the stored information.

~~~text
LIST
    ↓
Index
    ↓
ports[0]

DICTIONARY
    ↓
Key
    ↓
services[22]
~~~

A list is useful when I have an ordered collection of values.

A dictionary is useful when I want to associate one value with another.

---

## Security Relevance

These structures are very useful when writing security scripts.

For example:

~~~text
List
    ↓
IP addresses
Ports
Usernames
Passwords
URLs
~~~

And:

~~~text
Dictionary
    ↓
Port → Service
Username → Information
IP → Hostname
~~~

They allow collected data to be organised and processed efficiently.

---

## Key Takeaways

~~~text
LIST
    ↓
Ordered collection
    ↓
Index-based access
    ↓
.append()
.remove()
.pop()
.sort()
.reverse()
len()
in

DICTIONARY
    ↓
Key-value pairs
    ↓
Key-based access
    ↓
.keys()
.values()
.items()
.get()
~~~

Lists and dictionaries are fundamental data structures that I will use heavily when building practical Python and security scripts.