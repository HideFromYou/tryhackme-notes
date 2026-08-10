# TryHackMe — W1seGuy

## Room Information

**Room:** W1seGuy

**Category:** Reverse Engineering / Encryption

---

# 1. Source Code Analysis

The first step is to obtain the source code provided by the challenge.

Download the source code and examine it to get an understanding of what is going on.

The key points to note are:

1. **Bitwise XOR encryption** is used and then the bytes are hex encoded.
2. The first flag is encrypted this way and output to you when you connect to port `1337` of the machine.
3. A key value is randomly generated, which the server expects you to input.
4. If the input is correct, the server provides the second flag.

---

# 2. Connecting to the Service

The service is running on port:

```text
1337
```

Connect to the machine using Netcat:

```bash
nc <machine_ip_address> 1337
```

The server provides an encrypted value.

The objective is to understand the encryption mechanism and recover the key required by the server.

---

# 3. Understanding Bitwise XOR

The encryption uses a bitwise XOR operation.

The important property of XOR is:

```text
Flag XOR Key = Xored_value
```

Because XOR is reversible:

```text
Xored_value XOR Flag = Key
```

This means that if the plaintext and the XORed value are known, the key can be recovered.

Therefore, the key is not really protected if part of the plaintext is already known.

---

# 4. Key Length

By inspecting the source code, the key is identified as having a length of:

```text
5 characters
```

The bitwise XOR operation is performed for each character of the flag.

However, the flag length and the key length do not match.

The key is therefore repeatedly used for the XOR operation whenever its characters run out.

For example, a five-character key is reused across the complete flag:

```text
KEY12KEY12KEY12KEY12...
```

This means the same key characters are repeatedly used against the plaintext.

---

# 5. Known Flag Format

The first four characters of the flag are known:

```text
THM{
```

The last character of the flag is:

```text
}
```

This known plaintext can be used to recover the five-character key.

The first four characters of the key can be recovered by performing XOR between:

```text
THM{
```

and the corresponding encrypted value.

For the fifth character, the assumption is that the last character of the flag:

```text
}
```

was used to encrypt the fifth character of the key.

Therefore, the known plaintext used to recover the five-character key is:

```text
THM{}
```

---

# 6. Hex Encoding

The encrypted bytes received from the server are hex encoded.

Before performing the XOR operation, the hexadecimal representation must be decoded.

The process is:

```text
Hex encoded value
       ↓
Hex decode
       ↓
Encrypted bytes
       ↓
Known plaintext XOR
       ↓
Recover key
```

The hex string can be decoded in Python with:

```python
bytes.fromhex(hex_string)
```

---

# 7. Recovering the Key

After decoding the encrypted value from hexadecimal, perform the XOR operation against the known plaintext:

```text
THM{}
```

The first four characters:

```text
T
H
M
{
```

are used against the corresponding encrypted characters.

The fifth encrypted character is XORed with:

```text
}
```

This produces the five-character key.

Once the key has been recovered, it can be submitted to the server.

If the key is correct, the server returns the second flag.

---

# 8. Decrypting the First Flag

After recovering the key, use the same XOR operation against the entire encrypted output received from the server.

The process is:

```text
Encrypted hex output
       ↓
Hex decode
       ↓
Encrypted bytes
       ↓
XOR with recovered key
       ↓
Decrypted flag
```

Because the key is shorter than the flag, it is reused cyclically.

The key is accessed using:

```python
key[i % len(key)]
```

This allows the five-character key to be applied repeatedly across the entire encrypted value.

---

# 9. Python Script

The complete process can be automated with the following script:

```python
hex_string = input("Enter hex string: ")   # Take hex input from user

hex_encoded = hex_string

xored_original = bytes.fromhex(hex_encoded).decode('utf-8')

def xor_encrypt(text):
    if len(text) < 5:
        raise ValueError("Input string must be at least 5 characters long.")

    keys = ['T', 'H', 'M', '{','}']  # 4 keys for first 4 characters

    output = []

    # XOR first 4 characters
    for i in range(4):
        output.append(chr(ord(text[i]) ^ ord(keys[i])))

    # XOR last character with }
    last_char = text[-1]
    output.append(chr(ord(last_char) ^ ord(keys[4])))

    return "".join(output)

# Key
print(xor_encrypt(xored_original))

key=xor_encrypt(xored_original)

flag=xored_original
xored=""
for i in range(0,len(flag)):
    xored += chr(ord(flag[i]) ^ ord(key[i%len(key)]))

print(xored)
```

---

# 10. Script Breakdown

## Input

```python
hex_string = input("Enter hex string: ")
```

The script accepts the hexadecimal encrypted value received from the server.

---

## Hex Decoding

```python
xored_original = bytes.fromhex(hex_encoded).decode('utf-8')
```

The hexadecimal value is converted back into bytes and then decoded as UTF-8.

---

## Known Plaintext

The known characters are defined as:

```python
keys = ['T', 'H', 'M', '{','}']
```

These correspond to the known flag format:

```text
THM{}
```

---

## XORing the First Four Characters

The first four characters are XORed individually:

```python
for i in range(4):
    output.append(chr(ord(text[i]) ^ ord(keys[i])))
```

This uses:

```text
T
H
M
{
```

to recover the first four characters of the key.

---

## XORing the Fifth Character

The final character is taken from the end of the encrypted value:

```python
last_char = text[-1]
```

and XORed against:

```text
}
```

using:

```python
output.append(chr(ord(last_char) ^ ord(keys[4])))
```

The result is the fifth character of the key.

---

# 11. Recovering the Key in the Script

The key is generated with:

```python
key=xor_encrypt(xored_original)
```

The script prints it first:

```python
print(xor_encrypt(xored_original))
```

The recovered key can then be supplied to the server.

The key is randomly generated by the server, so the same key cannot simply be reused for another instance.

---

# 12. Decrypting the Flag

The encrypted value is stored in:

```python
flag=xored_original
```

A new string is then constructed:

```python
xored=""
```

The XOR operation is performed over the entire encrypted value:

```python
for i in range(0,len(flag)):
    xored += chr(ord(flag[i]) ^ ord(key[i%len(key)]))
```

The expression:

```python
key[i%len(key)]
```

causes the five-character key to repeat whenever the end of the key is reached.

Finally, the decrypted value is printed:

```python
print(xored)
```

This produces the decrypted first flag.

---

# 13. Complete Attack Flow

```text
Obtain Source Code
        ↓
Analyze Encryption
        ↓
Identify XOR
        ↓
Identify 5-Character Key
        ↓
Connect to Port 1337
        ↓
Receive Hex-Encoded Ciphertext
        ↓
Hex Decode
        ↓
Known Plaintext: THM{}
        ↓
XOR Known Plaintext
        ↓
Recover 5-Character Key
        ↓
Submit Key to Server
        ↓
Receive Second Flag
        ↓
Use Key Against Entire Ciphertext
        ↓
Decrypt First Flag
```

---

# Commands Used

## Connect to the Target

```bash
nc <machine_ip_address> 1337
```

---

# Key Concepts

## XOR Encryption

XOR encryption has the reversible property:

```text
A XOR B = C
```

Therefore:

```text
C XOR B = A
```

and:

```text
C XOR A = B
```

In this challenge:

```text
Flag XOR Key = Xored_value
```

Therefore:

```text
Xored_value XOR Key = Flag
```

and when the plaintext is known:

```text
Xored_value XOR Flag = Key
```

---

## Known Plaintext Attack

The flag format provides known plaintext:

```text
THM{}
```

Because the key is only five characters long, the five known characters can be used to recover the entire key.

This is the critical weakness in the encryption scheme.

---

## Repeating XOR Key

The key is five characters long, while the flag is longer.

The key is therefore repeatedly reused:

```text
KEY12KEY12KEY12KEY12...
```

The Python script implements this with:

```python
key[i % len(key)]
```

---

## Hex Encoding vs Encryption

The encrypted output is hex encoded.

Hex encoding itself is not encryption.

It is simply a representation of bytes using hexadecimal characters.

Therefore, the process is:

```text
XOR Encryption
      ↓
Encrypted Bytes
      ↓
Hex Encoding
      ↓
Hex String
```

To decrypt:

```text
Hex String
      ↓
Hex Decode
      ↓
Encrypted Bytes
      ↓
XOR with Key
      ↓
Plaintext
```

---

# Tools Used

- Netcat
- Python
- Source Code Analysis
- XOR
- Hex Decoding

---

# Key Takeaways

- Source code can reveal how an encryption mechanism works.
- XOR is reversible and can be attacked when plaintext is known.
- A predictable flag format such as `THM{}` provides known plaintext.
- A five-character repeating XOR key can be recovered when enough plaintext is known.
- Hex encoding does not provide cryptographic protection.
- The encrypted output must be hex decoded before performing the XOR operation.
- Once the key is recovered, it can be submitted to the server.
- The same recovered key can then be used to decrypt the complete encrypted output.
- The server generates a new arbitrary key, so the recovered key cannot simply be reused for another instance.