# 01 - Introduction

## Overview

This room is my first practical introduction to Python.

The goal is to build a simple **Guess the Number** game while learning the basic building blocks of Python.

The computer chooses a number between 1 and 20, and the user keeps guessing until they find it.

The program needs to:

    Pick a secret number
        ↓
    Ask the user for a guess
        ↓
    Compare the guess with the secret
        ↓
    Tell the user if the guess is too high or too low
        ↓
    Repeat until the number is guessed

---

## What I Will Learn

The room focuses on three fundamental Python concepts:

- Variables
- Conditional statements
- Iterations / loops

These concepts are introduced by building the game step by step.

---

## Example

~~~text
I'm thinking of a number between 1 and 20

Take a guess: 10
Too high, try again.

Take a guess: 5
Too low, try again.

Take a guess: 8
You got it in 3 tries!
~~~

---

## Variables

Variables will be used to store information required by the game.

For example:

~~~python
secret = random.randint(1, 20)
tries = 0
guess = 0
~~~

The program needs to remember:

    secret → The number selected by the computer
    guess  → The user's current guess
    tries  → Number of attempts

---

## Conditional Statements

The program needs to make decisions based on the user's input.

For example:

~~~python
if guess < secret:
    print("Too low, try again.")
elif guess > secret:
    print("Too high, try again.")
else:
    print("You got it!")
~~~

This allows the program to react differently depending on the user's guess.

---

## Iterations

The user needs more than one attempt.

A loop allows the program to continue asking for guesses until the correct number is found.

The basic idea is:

~~~python
while guess != secret:
    # ask for another guess
~~~

---

## Program Logic

The complete idea behind the game is:

    Generate Random Number
            ↓
    Store Variables
            ↓
    Ask for User Input
            ↓
    Compare Guess
            ↓
    Give Feedback
            ↓
    Repeat
            ↓
    Correct Guess
            ↓
    End

---

## Main Goal

The purpose of this room is not simply to copy the final program.

The important part is understanding how the individual Python concepts work together:

~~~text
Variables
    ↓
User Input
    ↓
Conditions
    ↓
Loops
    ↓
Program Behaviour
~~~

By the end of the room, these concepts will be combined into a working Python game.