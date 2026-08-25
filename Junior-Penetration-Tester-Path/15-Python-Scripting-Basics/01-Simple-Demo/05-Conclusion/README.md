# 05 - Conclusion

## Overview

This room introduced the basic Python concepts required to build a simple number guessing game.

The final program combines:

    Variables
        ↓
    User Input
        ↓
    Conditional Statements
        ↓
    while Loop
        ↓
    Complete Python Program

---

## Variables

Variables are used to store the information required by the program.

The game uses variables such as:

~~~python
secret = random.randint(1, 20)
tries = 0
guess = 0
~~~

They allow the program to keep track of the secret number, the current guess, and the number of attempts.

---

## User Input

The `input()` function allows the user to provide a guess:

~~~python
text = input("Take a guess: ")
~~~

Because `input()` returns text, the value is converted to an integer:

~~~python
guess = int(text)
~~~

---

## Conditional Statements

The program uses conditional statements to determine what feedback to give the user.

~~~python
if guess < 1 or guess > 20:
    print("That number is out of range. Try again.")
elif guess < secret:
    print("Too low, try again.")
elif guess > secret:
    print("Too high, try again.")
else:
    print("You got it in", tries, "tries!")
~~~

This allows the program to distinguish between:

    Invalid Guess
    Too Low
    Too High
    Correct Guess

---

## Iteration

The `while` loop allows the user to continue guessing:

~~~python
while guess != secret:
    # ask for another guess
~~~

The loop continues until:

~~~python
guess == secret
~~~

At that point the condition becomes false and the program exits the loop.

---

## Final Program

The concepts learned throughout the room come together in the completed game:

~~~python
import random

secret = random.randint(1, 20)
tries = 0
guess = 0

print("I'm thinking of a number between 1 and 20")

while guess != secret:
    text = input("Take a guess: ")
    guess = int(text)

    tries = tries + 1

    if guess < 1 or guess > 20:
        print("That number is out of range. Try again.")
    elif guess < secret:
        print("Too low, try again.")
    elif guess > secret:
        print("Too high, try again.")
    else:
        print("You got it in", tries, "tries!")
~~~

---

## Final Logic

~~~text
Generate Random Number
        ↓
Store Variables
        ↓
Ask for User Input
        ↓
Convert Input
        ↓
Increment Attempts
        ↓
Check Conditions
        ↓
Give Feedback
        ↓
Repeat with while
        ↓
Correct Guess
        ↓
Exit Program
~~~

---

## Key Takeaways

The main concepts covered in this room are:

~~~text
Variables
    ↓
Store Data

Conditional Statements
    ↓
Make Decisions

while Loop
    ↓
Repeat Code

Input
    ↓
Interact With the User
~~~

The important part is understanding how these individual Python concepts work together to create a functional program.

This simple game provides the foundation for writing more complex Python scripts in the following rooms.