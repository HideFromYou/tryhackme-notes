# Decoder

## Overview

The **Decoder** module in Burp Suite is a utility designed to encode, decode, transform, and hash data during web application security testing. It allows testers to quickly convert values between different formats without leaving Burp Suite, making request analysis and manipulation more efficient.

Decoder is especially useful when working with encoded parameters, cookies, tokens, or other data that requires transformation before further analysis.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the purpose of the Decoder module
- Encode and decode data using common formats
- Generate hash values
- Use Smart Decode to automatically identify layered encodings
- Recognise situations where Decoder simplifies web application testing

---

## Main Content

### What is Decoder?

Decoder is a utility module that performs various data transformations directly within Burp Suite.

It enables testers to manipulate intercepted data without relying on external tools, improving both speed and workflow efficiency.

---

### Encoding and Decoding

Decoder supports a variety of encoding and decoding operations commonly encountered during web application testing.

These operations help convert data into formats required by applications or reveal the original content of encoded values.

Common uses include:

- URL Encoding
- URL Decoding
- Base64 Encoding
- Base64 Decoding
- HTML Encoding
- HTML Decoding
- Hex Encoding and Decoding

---

### Hashing

Decoder can generate cryptographic hash values for supplied input.

Hashing is useful for verifying data integrity, comparing values, and understanding how applications store or process sensitive information.

---

### Smart Decode

Smart Decode automatically attempts to identify the encoding applied to a value and recursively decodes it until readable data is produced.

This feature is particularly useful when multiple layers of encoding have been applied.

---

## Skills Practiced

- Data Encoding
- Data Decoding
- Hash Generation
- Data Transformation
- Web Data Analysis

---

## Key Takeaways

- Decoder provides built-in data transformation capabilities within Burp Suite.
- Multiple encoding and decoding formats are supported.
- Smart Decode simplifies the analysis of layered encodings.
- Hash generation is available without external utilities.
- Decoder improves efficiency during web application security assessments.