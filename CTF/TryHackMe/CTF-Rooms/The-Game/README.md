# The Game — TryHackMe CTF

## Room Information

**Room:** The Game

**TryHackMe Room:** https://tryhackme.com/room/hfb1thegame

**Difficulty:** Easy

---

# Challenge Overview

The Game is a very simple TryHackMe CTF challenge.

The challenge provides a ZIP file containing a Windows executable:

```text
Tatrix.exe
```

After extracting the ZIP file and running the `.exe` file, a game is launched.

The game gives off strong nostalgia vibes, bringing back childhood memories of pixel blocks and timeless fun.

At first, it appears to simply be a game.

However, there is a very basic but hidden twist.

The important part of the challenge is not necessarily playing the game itself, but investigating the executable.

---

# 1. Challenge File

The challenge provides a ZIP archive.

After extracting the archive, the main file is:

```text
Tatrix.exe
```

The executable is a Windows `.exe` file.

Running the executable launches the game.

The game consists of pixel blocks and has a classic nostalgic style.

The main question is:

```text
Where is the flag?
```

There is a hidden element inside the executable that can be investigated without needing to reverse engineer the entire program.

---

# 2. The Hidden Twist

The hidden twist is related to the information contained inside the `.exe` file.

The executable can contain printable ASCII strings.

These strings can sometimes reveal information that is not directly visible when running the program.

To extract printable ASCII strings from binary files or executable files, we can use:

```text
strings
```

The `strings` utility is used to extract printable ASCII strings from binary files and executables.

---

# 3. Using strings Against the Executable

Run the `strings` command against the executable:

```bash
strings Tatrix.exe
```

The command extracts the printable strings contained inside:

```text
Tatrix.exe
```

The output produces plenty of lines of information related to the game and the executable.

Instead of manually going through all of the output, the results can be filtered.

---

# 4. Searching the Output with Grep

Since the `strings` command produces plenty of lines, `grep` can be used to search for specific information.

For example:

```bash
strings Tatrix.exe | grep flag
```

This performs two operations:

```text
Tatrix.exe
    ↓
strings
    ↓
Extract printable ASCII strings
    ↓
grep
    ↓
Search for "flag"
```

The `grep` command filters the output of `strings` and searches for occurrences of:

```text
flag
```

The relevant result reveals the hidden flag.

---

# 5. Flag Discovery

The flag is hidden inside the executable as printable information.

Instead of having to exploit the game itself, the executable can simply be inspected using:

```bash
strings Tatrix.exe
```

and then filtered with:

```bash
strings Tatrix.exe | grep flag
```

The second command makes it much easier to locate the flag among the large amount of output produced by `strings`.

The flag is therefore obtained directly from the executable.

---

# Attack Flow

```text
ZIP File
   ↓
Extract Tatrix.exe
   ↓
Run Tatrix.exe
   ↓
Classic Pixel-Block Game
   ↓
Investigate the Executable
   ↓
strings Tatrix.exe
   ↓
Plenty of Printable Strings
   ↓
grep
   ↓
Search for "flag"
   ↓
Flag
```

---

# Commands Used

## Extract Printable ASCII Strings

```bash
strings Tatrix.exe
```

The `strings` utility extracts printable ASCII strings from the binary/executable file.

---

## Filter the Output

```bash
strings Tatrix.exe | grep flag
```

This pipes the output of `strings` into `grep` and searches for the word:

```text
flag
```

---

# Tools Used

- `strings`
- `grep`
- Terminal
- `Tatrix.exe`

---

# Key Concepts

## Strings in Executables

Executable files are binary files, but they can still contain readable text.

The `strings` utility allows us to extract printable ASCII sequences from those files.

This can be useful during initial analysis because developers may leave:

- Strings
- Messages
- URLs
- File paths
- Credentials
- Configuration data
- Flags
- Other readable information

inside a binary.

---

## Filtering Large Output

Running:

```bash
strings Tatrix.exe
```

can produce a large amount of output.

Instead of manually reviewing every line, command-line tools such as `grep` can be used to filter the results:

```bash
strings Tatrix.exe | grep flag
```

This is a simple example of combining Unix/Linux command-line utilities through a pipe:

```text
Command 1
   ↓
Output
   ↓
Pipe |
   ↓
Command 2
   ↓
Filtered Output
```

---

# Methodology

```text
1. Receive the ZIP file
        ↓
2. Extract the archive
        ↓
3. Identify Tatrix.exe
        ↓
4. Execute the application
        ↓
5. Recognize that the executable itself may contain useful information
        ↓
6. Use strings against Tatrix.exe
        ↓
7. Review the printable strings
        ↓
8. Use grep to search for "flag"
        ↓
9. Identify the flag
```

---

# Key Takeaways

- A very simple CTF can hide information inside an executable.
- Running the application is not always enough; the underlying file should also be investigated.
- Executables can contain printable ASCII strings.
- `strings` is a useful first step when inspecting an unknown binary or executable.
- `strings` can produce a large amount of output.
- `grep` can be used to quickly filter that output.
- The combination:

```bash
strings Tatrix.exe | grep flag
```

can quickly locate a flag embedded in an executable.