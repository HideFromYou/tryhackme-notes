# 03 - Conditional Statements

## Overview

At this stage, the program can accept a guess, but it cannot yet determine whether the guess is correct.

Conditional statements allow the program to make decisions based on the relationship between the user's guess and the secret number.

The basic structure is:

~~~python
if condition:
    # code

elif condition:
    # code

else:
    # code
~~~

---

## Comparing the Guess

The game needs to check three possible situations:

    Guess is lower than secret
        ↓
    Too low

    Guess is higher than secret
        ↓
    Too high

    Guess equals secret
        ↓
    Correct

This can be implemented with:

~~~python
if guess < secret:
    print("Too low, try again.")
elif guess > secret:
    print("Too high, try again.")
else:
    print("You got it in", tries, "tries!")
~~~

---

## Comparison Operators

The important comparison operators used by the game are:

~~~text
<    Less than
>    Greater than
==   Equal to
!=   Not equal to
~~~

For example:

~~~python
guess < secret
~~~

checks whether the guess is smaller than the secret number.

While:

~~~python
guess == secret
~~~

checks whether both values are equal.

---

## Checking the Valid Range

The game expects a number between 1 and 20.

A guess outside this range should be rejected:

~~~python
if guess < 1 or guess > 20:
    print("That number is out of range. Try again.")
~~~

The `or` operator means that either condition can make the complete condition true.

---

## Complete Conditional Logic

The game can now use:

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

The conditions are checked from top to bottom.

---

## Decision Flow

The logic can be visualised as:

~~~text
Is the guess outside 1-20?
        ↓
      YES → Out of range
        ↓ NO
Is guess smaller than secret?
        ↓
      YES → Too low
        ↓ NO
Is guess greater than secret?
        ↓
      YES → Too high
        ↓ NO
      Correct!
~~~

---

## Current Program

The program now looks like:

~~~python
import random

secret = random.randint(1, 20)
tries = 0
guess = 0

print("I'm thinking of a number between 1 and 20")

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

The program can now correctly evaluate a guess.

The remaining problem is that the user only gets **one attempt**.

To allow multiple attempts, the program needs a loop.