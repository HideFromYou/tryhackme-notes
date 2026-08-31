# Compiled

## Overview

This room focused on basic binary analysis and decompilation.

The goal was to determine the password required by the compiled binary.

The main attack chain was:

    Run Binary
      ↓
    Observe Password Prompt
      ↓
    Decompile with Ghidra
      ↓
    Analyze main()
      ↓
    Understand scanf() format
      ↓
    Identify expected value
      ↓
    Construct correct input
      ↓
    Correct!

---

## 1. Running the Binary

I first downloaded the provided binary and tried to execute it:

    ./Compiled.Compiled

The program asked for a password:

    Password: test
    Try again!

This confirmed that the main objective was to determine what input the binary expected.

---

## 2. Decompiling with Ghidra

Since the password was not obvious from simply running the binary, I opened it in **Ghidra** and inspected the `main()` function.

The important part of the decompiled code was:

    fwrite("Password: ",1,10,stdout);
    __isoc99_scanf("DoYouEven%sCTF",local_28);

The input was stored in:

    local_28

The program then compared `local_28` against two strings.

First:

    __dso_handle

If the input matched this value, the program printed:

    Try again!

Then it compared the input with:

    _init

If the input matched `_init`, the program printed:

    Correct!

---

## 3. Understanding the scanf() Format

The important part was:

    scanf("DoYouEven%sCTF", local_28);

The input format contains:

    DoYouEven
    %s
    CTF

The `%s` portion is what gets stored in `local_28`.

The important observation was that the program expects the input to begin with:

    DoYouEven

and the value captured by `%s` needs to become:

    _init

Therefore, I needed to provide:

    DoYouEven_init

---

## 4. Testing the Password

I ran the binary again:

    ./Compiled.Compiled

and entered:

    Password: DoYouEven_init

The binary returned:

    Correct!

So the required input was:

    DoYouEven_init

---

## 5. Important Code Logic

The relevant logic can be simplified to:

    input → local_28

    if local_28 == "__dso_handle":
        Try again!

    if local_28 == "_init":
        Correct!
    else:
        Try again!

The important part was understanding what value actually ends up inside `local_28`.

The full password I enter is not simply `_init`.

Because of the `scanf()` format string, I need to provide:

    DoYouEven_init

so that the `%s` portion produces:

    _init

---

## Attack / Analysis Chain

    Execute binary
        ↓
    Password prompt
        ↓
    Failed normal input
        ↓
    Decompile binary with Ghidra
        ↓
    Inspect main()
        ↓
    Find scanf("DoYouEven%sCTF", local_28)
        ↓
    Find strcmp(local_28, "_init")
        ↓
    Determine required local_28 value
        ↓
    Construct input: DoYouEven_init
        ↓
    Correct!

---

## Tools Used

### Ghidra

Used to decompile the compiled binary and understand its internal logic.

### Linux

Used to execute and test the binary:

    ./Compiled.Compiled

---

## Key Takeaways

- When a binary asks for a password and there is no obvious way to determine it, decompilation can reveal the validation logic.
- Ghidra can convert compiled binaries into a more readable representation.
- Pay close attention to `strcmp()` because it can reveal what value the program is comparing against.
- Pay close attention to `scanf()` format strings because they determine how the input is parsed.
- The important value to identify is what gets stored in the program's variable, not necessarily the exact text typed by the user.

### Important Concept

    scanf("DoYouEven%sCTF", local_28)

means the `%s` input is what gets stored in `local_28`.

In this case:

    Input:
    DoYouEven_init

    ↓

    local_28:
    _init

    ↓

    strcmp(local_28, "_init")

    ↓

    Correct!