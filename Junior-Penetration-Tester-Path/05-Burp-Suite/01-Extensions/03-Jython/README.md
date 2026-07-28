# Jython

## Overview

Jython is a Java implementation of the Python programming language that enables Python code to run on the Java Virtual Machine (JVM). Within Burp Suite, Jython provides compatibility for Python-based extensions, allowing users and developers to create or use extensions without writing Java code directly.

Understanding Jython helps explain how Burp Suite supports multiple programming languages through its Extender framework.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Jython is
- Explain why Burp Suite uses Jython
- Recognise the relationship between Python and the Java Virtual Machine
- Understand Jython's role in Burp Suite extensions
- Configure Burp Suite to use Jython when required

---

## Main Content

### What is Jython?

Jython is an implementation of Python that runs on the Java Virtual Machine (JVM). Unlike the standard Python interpreter (CPython), Jython allows Python code to interact directly with Java libraries and applications.

This compatibility makes it possible for Burp Suite to support Python-based extensions while maintaining its Java architecture.

---

### Why Burp Suite Uses Jython

Burp Suite is developed in Java, but many extension developers prefer writing code in Python due to its readability and simplicity.

By using Jython, Burp Suite can execute Python-based extensions without requiring them to be rewritten in Java.

This allows developers to create custom functionality while taking advantage of Java's underlying framework.

---

### Jython and Burp Extensions

Some Burp Suite extensions require Jython to function correctly.

Once Jython is configured within Burp Suite, compatible extensions can access the Burp Extender API and interact with application traffic, requests, responses, and other Burp modules.

This enables developers to build automation, analysis tools, and custom workflow enhancements.

---

### Configuration

To use Python-based extensions, Burp Suite may require the location of the Jython standalone JAR file to be configured within the Extender settings.

After configuration, compatible extensions can be loaded in the same way as other supported extension types.

---

## Skills Practiced

- Understanding Jython
- JVM Fundamentals
- Python Extension Support
- Burp Suite Configuration
- Extender Integration

---

## Key Takeaways

- Jython is a Python implementation that runs on the Java Virtual Machine.
- Burp Suite uses Jython to support Python-based extensions.
- Jython enables Python code to interact with Burp Suite's Java architecture.
- Proper configuration allows compatible extensions to run successfully.
- Understanding Jython helps when working with custom Burp Suite extensions.