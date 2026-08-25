# 01 - Simple Demo

## Overview

This room was my first practical introduction to Python.

The goal was to build a simple **Guess the Number** game while learning the basic building blocks of Python.

The program chooses a random number between 1 and 20 and allows the user to keep guessing until the correct number is found.

---

## What I Learned

The room introduced three fundamental Python concepts:

- Variables
- Conditional Statements
- Iterations / `while` loops

These concepts were introduced step by step and then combined into one working program.

---

## 01 - Introduction

I learned the basic idea behind the Python program and how the different concepts would be combined to create the game.

The overall logic was:

~~~text
Generate Secret Number
        ↓
Ask for User Input
        ↓
Compare Guess
        ↓
Give Feedback
        ↓
Repeat Until Correct
~~~

---

## 02 - Variables

I learned how variables store information used by the program.

The game uses variables such as:

~~~python
secret = random.randint(1, 20)
tries = 0
guess = 0
~~~

I also learned how to receive user input:

~~~python
text = input("Take a guess: ")
guess = int(text)
~~~

And how to increase the number of attempts:

~~~python
tries = tries + 1
~~~

Important concepts:

~~~text
secret → Random number
guess  → User's current guess
tries  → Number of attempts
~~~

---

## 03 - Conditional Statements

I learned how Python makes decisions using:

~~~python
if
elif
else
~~~

The game compares the user's guess with the secret number:

~~~python
if guess < secret:
    print("Too low, try again.")
elif guess > secret:
    print("Too high, try again.")
else:
    print("You got it in", tries, "tries!")
~~~

I also learned comparison operators:

~~~text
<     Less than
>     Greater than
==    Equal to
!=    Not equal to
~~~

And the logical operator:

~~~text
or
~~~

which was used to check whether the number was outside the valid range of 1–20.

---

## 04 - Iterations

I learned how to repeat code using a `while` loop.

The game continues while the guess is not equal to the secret number:

~~~python
while guess != secret:
~~~

The logic is:

~~~text
Check Condition
      ↓
Condition True
      ↓
Execute Code
      ↓
Get New Guess
      ↓
Check Condition Again
      ↓
Correct Guess
      ↓
Condition False
      ↓
Exit Loop
~~~

This allowed the user to make multiple attempts instead of only one.

---

## 05 - Conclusion

The final program combined everything learned in the room:

~~~text
Variables
    ↓
User Input
    ↓
Conditional Statements
    ↓
while Loop
    ↓
Working Python Program
~~~

The completed game:

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

## Final Mental Model

The main lesson from this room was understanding how basic Python building blocks work together:

~~~text
VARIABLES
Store information
      ↓
INPUT
Receive information from the user
      ↓
CONDITIONALS
Make decisions
      ↓
LOOPS
Repeat actions
      ↓
PROGRAM
Combine everything into useful behaviour
~~~

This room established the basic Python foundation needed for the following modules, where the focus moves from simple concepts towards writing complete scripts.