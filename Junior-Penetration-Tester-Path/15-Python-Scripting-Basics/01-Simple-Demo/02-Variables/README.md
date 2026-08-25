# 02 - Variables

## Overview

The first part of building the game is creating the variables that store the information the program needs.

The game needs to keep track of:

    The secret number
    The user's guess
    The number of attempts

---

## Importing random

Python provides the `random` module for generating random values.

~~~python
import random
~~~

To generate a random number between 1 and 20:

~~~python
secret = random.randint(1, 20)
~~~

The generated number is stored in the variable:

~~~text
secret
~~~

---

## Creating Variables

The game starts with:

~~~python
tries = 0
guess = 0
~~~

These variables have different purposes:

~~~text
secret → Random number selected by the computer
guess  → Current number entered by the user
tries  → Number of guesses made
~~~

---

## Getting User Input

The `input()` function allows the program to receive information from the user.

~~~python
text = input("Take a guess: ")
~~~

The value returned by `input()` is text.

Because the game needs to compare the guess with an integer, the input must be converted:

~~~python
guess = int(text)
~~~

This converts the user's input into an integer.

---

## Counting Attempts

Every time the user makes a guess, the number of attempts needs to increase.

~~~python
tries = tries + 1
~~~

For example:

~~~text
tries = 0
guess → first attempt
tries = 1

guess → second attempt
tries = 2
~~~

---

## Current Program

At this stage, the program can generate a secret number, accept user input, convert it into an integer, and count the attempt.

~~~python
import random

secret = random.randint(1, 20)
tries = 0
guess = 0

print("I'm thinking of a number between 1 and 20")

text = input("Take a guess: ")
guess = int(text)

tries = tries + 1
~~~

The program can now collect the user's guess.

However, it still needs logic to determine whether the guess is:

    Too low
    Too high
    Correct

That will be handled with conditional statements.