# 06 - Password Strength Checker

## Overview

This lesson brings together the concepts covered in both the `Python: Core Concepts` room and this `Python: Building Scripts` room.

The result is a complete **Password Strength Checker**.

The program:

~~~text
Load common passwords
        ↓
Ask the user for a password
        ↓
Check password length
        ↓
Check character variety
        ↓
Check common-password list
        ↓
Calculate score
        ↓
Assign strength label
        ↓
Display feedback
        ↓
Write result to log
~~~

The complete script is stored as:

~~~text
password_checker.py
~~~

---

## Step 1 - Loading Common Passwords

The program first loads common passwords from:

~~~text
common_passwords.txt
~~~

A function is used to handle this:

~~~python
import string

def load_common_passwords(filepath):
    """Load a list of common passwords from a text file."""
    common = []

    try:
        with open(filepath, "r") as f:
            for line in f:
                common.append(line.strip().lower())

    except FileNotFoundError:
        print(f"Warning: '{filepath}' not found. Skipping common-password check.")

    return common
~~~

This function combines several concepts:

~~~text
Function
    ↓
File I/O
    ↓
try / except
    ↓
List
    ↓
Loop
    ↓
String methods
~~~

The passwords are converted to lowercase so that comparisons are case-insensitive.

---

## Step 2 - Password Scoring Function

The main password analysis is performed by:

~~~python
def check_password(password, common_list):
    """Evaluate a password and return (score, feedback_list)."""

    score = 0
    feedback = []

    # Length checks
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("Password should be at least 8 characters.")

    if len(password) >= 12:
        score += 1

    # Character variety checks
    if any(c in string.ascii_uppercase for c in password):
        score += 1
    else:
        feedback.append("Add at least one uppercase letter.")

    if any(c in string.digits for c in password):
        score += 1
    else:
        feedback.append("Add at least one digit.")

    if any(c in string.punctuation for c in password):
        score += 1
    else:
        feedback.append("Add at least one special character (e.g., !, @, #).")

    # Common password check
    if password.lower() in common_list:
        score = 0
        feedback = [
            "This password is in the common-passwords list. Choose another."
        ]

    return score, feedback
~~~

---

## Password Scoring

The password receives points based on several checks.

~~~text
Length >= 8
    ↓
+1

Length >= 12
    ↓
+1

Uppercase character
    ↓
+1

Digit
    ↓
+1

Special character
    ↓
+1
~~~

The maximum score is:

~~~text
5/5
~~~

However, if the password appears in the common-password list:

~~~text
Score = 0
~~~

The common-password check overrides the other scoring.

---

## Returning Multiple Values

The function returns:

~~~python
return score, feedback
~~~

Two values are returned together.

They can be received as:

~~~python
score, feedback = check_password(password, common_list)
~~~

The returned values are effectively received together as a tuple.

---

## Step 3 - Strength Labels

The program maps the numerical score to a strength label using a dictionary:

~~~python
strength_labels = {
    0: "Weak",
    1: "Weak",
    2: "Moderate",
    3: "Moderate",
    4: "Strong",
    5: "Strong"
}
~~~

The label is retrieved using:

~~~python
label = strength_labels.get(score, "Unknown")
~~~

This connects the numerical score with a human-readable result.

---

## Step 4 - Main Program

The main program loads the common-password list:

~~~python
common_list = load_common_passwords("common_passwords.txt")
~~~

Then it continuously asks for passwords:

~~~python
while True:
    password = input("\nEnter a password to check (or 'quit' to exit): ")
~~~

The user can exit by entering:

~~~text
quit
~~~

The program checks this with:

~~~python
if password.lower() == "quit":
    print("Goodbye.")
    break
~~~

---

## Handling Empty Passwords

An empty password should not be processed.

The program checks for this:

~~~python
if len(password) == 0:
    print("Password cannot be empty. Try again.")
    continue
~~~

Here:

~~~text
continue
    ↓
Skip the current iteration
    ↓
Ask for another password
~~~

---

## Running the Password Check

The password is passed to the scoring function:

~~~python
score, feedback = check_password(password, common_list)
~~~

The strength label is then retrieved:

~~~python
label = strength_labels.get(score, "Unknown")
~~~

The result is displayed:

~~~python
print(f"\nStrength: {label} ({score}/5)")
~~~

---

## Displaying Feedback

If suggestions exist:

~~~python
if feedback:
    print("Suggestions:")

    for tip in feedback:
        print(f"  - {tip}")
~~~

This uses:

~~~text
if
    ↓
Check whether feedback exists

for
    ↓
Process every suggestion

f-string
    ↓
Format the output
~~~

---

## Logging the Result

The program also writes the result to:

~~~text
password_log.txt
~~~

The file is opened in append mode:

~~~python
with open("password_log.txt", "a") as log:
    log.write(
        f"Password: {'*' * len(password)} | "
        f"Strength: {label} ({score}/5)\n"
    )
~~~

The actual password is **not** written to the log.

Instead, asterisks are used:

~~~text
Password: ************** | Strength: Strong (5/5)
~~~

This is an important security practice.

Plaintext passwords should not be stored in logs.

---

## Complete Program

~~~python
import string


def load_common_passwords(filepath):
    """Load a list of common passwords from a text file."""
    common = []

    try:
        with open(filepath, "r") as f:
            for line in f:
                common.append(line.strip().lower())

    except FileNotFoundError:
        print(f"Warning: '{filepath}' not found. Skipping common-password check.")

    return common


def check_password(password, common_list):
    """Evaluate a password and return (score, feedback_list)."""

    score = 0
    feedback = []

    # Length checks
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("Password should be at least 8 characters.")

    if len(password) >= 12:
        score += 1

    # Character variety checks
    if any(c in string.ascii_uppercase for c in password):
        score += 1
    else:
        feedback.append("Add at least one uppercase letter.")

    if any(c in string.digits for c in password):
        score += 1
    else:
        feedback.append("Add at least one digit.")

    if any(c in string.punctuation for c in password):
        score += 1
    else:
        feedback.append("Add at least one special character (e.g., !, @, #).")

    # Common password check
    if password.lower() in common_list:
        score = 0
        feedback = [
            "This password is in the common-passwords list. Choose another."
        ]

    return score, feedback


def main():
    strength_labels = {
        0: "Weak",
        1: "Weak",
        2: "Moderate",
        3: "Moderate",
        4: "Strong",
        5: "Strong"
    }

    common_list = load_common_passwords("common_passwords.txt")

    while True:
        password = input(
            "\nEnter a password to check (or 'quit' to exit): "
        )

        if password.lower() == "quit":
            print("Goodbye.")
            break

        if len(password) == 0:
            print("Password cannot be empty. Try again.")
            continue

        score, feedback = check_password(password, common_list)
        label = strength_labels.get(score, "Unknown")

        print(f"\nStrength: {label} ({score}/5)")

        if feedback:
            print("Suggestions:")

            for tip in feedback:
                print(f"  - {tip}")

        with open("password_log.txt", "a") as log:
            log.write(
                f"Password: {'*' * len(password)} | "
                f"Strength: {label} ({score}/5)\n"
            )


main()
~~~

---

## Example Results

### Common Password

Input:

~~~text
password
~~~

Result:

~~~text
Strength: Weak (0/5)

Suggestions:
  - This password is in the common-passwords list. Choose another.
~~~

### Moderate Password

Input:

~~~text
Tr0ub4dor
~~~

Result:

~~~text
Strength: Moderate (3/5)

Suggestions:
  - Add at least one special character (e.g., !, @, #).
~~~

### Strong Password

Input:

~~~text
C0mpl3x!Pass#99
~~~

Result:

~~~text
Strength: Strong (5/5)
~~~

---

## Example Test

The room also tests the password:

~~~text
TryHackMe!2025
~~~

The program reports:

~~~text
Strong
~~~

When the result is written to the log, the password itself is masked with asterisks.

The recorded number of asterisks for this test is:

~~~text
14
~~~

---

## Concepts Combined

This project brings together the concepts from the previous rooms:

~~~text
Variables
    ↓
Strings
    ↓
Lists
    ↓
Dictionaries
    ↓
Conditionals
    ↓
Loops
    ↓
Functions
    ↓
Error Handling
    ↓
File I/O
    ↓
Libraries
    ↓
Complete Python Program
~~~

---

## Security Lessons

The most important security-related lesson is that sensitive information should not be unnecessarily stored in plaintext.

The password checker therefore logs:

~~~text
Password: **************
~~~

instead of:

~~~text
Password: C0mpl3x!Pass#99
~~~

This is a practical example of applying secure thinking while writing a script.

---

## Key Takeaways

This project demonstrates how individual Python concepts can be combined into a complete security-oriented program.

The important progression is:

~~~text
Learn Python Concepts
        ↓
Create Functions
        ↓
Handle Errors
        ↓
Read External Data
        ↓
Process Data
        ↓
Write Results
        ↓
Build a Complete Security Tool
~~~

This is the point where Python starts becoming useful for practical cybersecurity automation.