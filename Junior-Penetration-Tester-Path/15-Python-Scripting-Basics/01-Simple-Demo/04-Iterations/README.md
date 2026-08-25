# 04 - Iterations

## Overview

At this stage, the game can evaluate a single guess.

The problem is that the user needs to be able to keep guessing until the correct number is found.

To achieve this, I need to use a loop.

Python provides different types of loops. In this game, I use a `while` loop.

---

## while Loop

The basic structure of a `while` loop is:

~~~python
while condition:
    # code to repeat
~~~

For the number guessing game, the loop should continue while the guess is **not** equal to the secret number:

~~~python
while guess != secret:
    # ask for another guess
~~~

The condition is therefore:

~~~python
guess != secret
~~~

As long as this condition is `True`, the loop continues.

Once the guess becomes equal to the secret number, the condition becomes `False` and the loop stops.

---

## Building the Loop

The input and conditional logic can now be placed inside the `while` loop:

~~~python
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

## How the Loop Works

Suppose the secret number is:

~~~python
secret = 10
~~~

Initially:

~~~python
guess = 0
~~~

The loop checks:

~~~python
guess != secret
~~~

Which gives:

~~~text
0 != 10
True
~~~

Therefore the loop executes.

The user enters:

~~~text
5
~~~

Now:

~~~text
5 != 10
True
~~~

The loop continues.

The user tries again:

~~~text
8
~~~

Again:

~~~text
8 != 10
True
~~~

The user eventually enters:

~~~text
10
~~~

Now:

~~~text
10 != 10
False
~~~

The `while` loop stops.

---

## Complete Program

The final version of the game is:

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

## Iteration Flow

~~~text
Start
  ↓
Generate Secret Number
  ↓
Check: guess != secret
  ↓
Ask for Guess
  ↓
Increment tries
  ↓
Compare Guess
  ↓
Too Low / Too High
  ↓
Check Condition Again
  ↓
Correct Guess
  ↓
guess == secret
  ↓
Condition becomes False
  ↓
Exit Loop
~~~

---

## Important Concept

The most important part of the iteration is the condition:

~~~python
while guess != secret:
~~~

The loop continues because the value of `guess` changes after every user input.

Eventually:

~~~python
guess == secret
~~~

At that point:

~~~python
guess != secret
~~~

becomes `False`, so Python exits the loop.

---

## What I Learned

The `while` loop allows the program to repeat a block of code while a condition remains true.

In this game:

~~~text
while guess != secret
        ↓
Keep asking for guesses
        ↓
Update guess
        ↓
Check condition again
        ↓
Correct guess
        ↓
Stop
~~~

This completes the main iteration logic of the Guess the Number game.