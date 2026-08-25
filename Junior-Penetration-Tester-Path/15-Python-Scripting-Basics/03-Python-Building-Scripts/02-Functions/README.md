# 02 - Functions

## Overview

Functions allow me to organise code into reusable blocks.

Instead of writing the same code multiple times, I can define a function once and call it whenever I need it.

The basic structure is:

~~~python
def function_name():
    # code
~~~

---

## Defining a Function

A simple function:

~~~python
def greet():
    print("Hello!")
~~~

The function does not run when it is defined.

I need to call it:

~~~python
greet()
~~~

Output:

~~~text
Hello!
~~~

---

## Parameters

Functions can receive information through parameters.

~~~python
def greet(name):
    print(f"Hello, {name}!")
~~~

I can then provide an argument:

~~~python
greet("Nikos")
~~~

Output:

~~~text
Hello, Nikos!
~~~

The difference is:

~~~text
Parameter
    ↓
Variable defined by the function

Argument
    ↓
Actual value passed to the function
~~~

---

## Multiple Parameters

A function can accept multiple parameters.

~~~python
def add_numbers(a, b):
    print(a + b)
~~~

Calling it:

~~~python
add_numbers(5, 3)
~~~

Output:

~~~text
8
~~~

---

## Return Values

Functions can return a value using `return`.

~~~python
def add_numbers(a, b):
    return a + b
~~~

The returned value can be stored in a variable:

~~~python
result = add_numbers(5, 3)

print(result)
~~~

Output:

~~~text
8
~~~

This is different from simply printing the result because the returned value can be used elsewhere in the program.

---

## Returning Multiple Values

Python functions can return multiple values.

~~~python
def get_user():
    username = "admin"
    role = "administrator"

    return username, role
~~~

The returned values can be assigned to multiple variables:

~~~python
username, role = get_user()

print(username)
print(role)
~~~

Python returns these values together as a tuple.

---

## Default Parameters

A function can define a default value for a parameter.

~~~python
def greet(name="Guest"):
    print(f"Hello, {name}!")
~~~

Calling the function without an argument:

~~~python
greet()
~~~

Output:

~~~text
Hello, Guest!
~~~

Providing an argument overrides the default:

~~~python
greet("Nikos")
~~~

Output:

~~~text
Hello, Nikos!
~~~

---

## Scope

Variables created inside a function are local to that function.

~~~python
def example():
    message = "Hello"
    print(message)
~~~

The variable `message` exists inside the function's scope.

A variable created outside the function has a different scope:

~~~python
message = "Outside"

def example():
    print(message)
~~~

Understanding scope becomes important when building larger programs because functions should generally operate with their own inputs and outputs rather than relying on unexpected global state.

---

## Why Functions Matter

Functions make programs easier to:

~~~text
Organise
    ↓
Reuse
    ↓
Test
    ↓
Maintain
    ↓
Expand
~~~

Instead of putting an entire program into one large block, I can separate its functionality into smaller pieces.

---

## Security Relevance

Functions are particularly useful in security scripts.

For example, instead of writing scanning logic directly into the main program:

~~~python
def scan_port(target, port):
    # scanning logic
    pass
~~~

I can call the function for different targets and ports.

The same idea can be applied to:

~~~text
DNS Enumeration
    ↓
Function

Port Scanning
    ↓
Function

HTTP Requests
    ↓
Function

Input Validation
    ↓
Function

Result Processing
    ↓
Function
~~~

This makes security scripts easier to structure and reuse.

---

## Key Takeaways

~~~text
def
    ↓
Define a function

Parameters
    ↓
Accept input

Arguments
    ↓
Provide values

return
    ↓
Send a result back

Default Parameters
    ↓
Provide fallback values

Scope
    ↓
Control where variables exist
~~~

Functions are one of the main building blocks for turning individual Python commands into organised and reusable scripts.