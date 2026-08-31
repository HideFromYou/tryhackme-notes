# Lo-Fi

## Overview

This room was a basic introduction to **Local File Inclusion (LFI)**.

The main attack chain was:

    Nmap
      ↓
    Web Application
      ↓
    Identify `page` parameter
      ↓
    Burp Suite
      ↓
    Test Local File Inclusion
      ↓
    Path Traversal
      ↓
    Read local files
      ↓
    Find flag.txt

---

## 1. Enumeration

I started with a full TCP port scan and service detection:

    nmap -p- lofi.thm -sV --min-rate 10000

The scan showed two open ports:

    22 → SSH
    80 → HTTP

Port 80 was hosting a Lo-Fi music web application.

---

## 2. Identifying the LFI Parameter

While navigating through the different sections of the website, I noticed that the URL changed depending on the selected page.

The application was referencing PHP files through a `page` parameter.

For example, the URL contained something similar to:

    ?page=chill.php

This was interesting because the application appeared to be dynamically including PHP files based on user input.

### Observation

When I see a parameter that appears to control which file the application loads, I should consider **Local File Inclusion (LFI)**.

---

## 3. Testing with Burp Suite

I opened Burp Suite and captured a request while navigating through the website.

I sent the request to **Repeater** so I could modify the `page` parameter manually.

I first changed:

    chill.php

to:

    /etc/passwd

The application returned an error.

I then tested path traversal by adding:

    ../

before `/etc/passwd`.

The response changed, indicating that the validation could be bypassed using path traversal.

I continued adding `../` because I did not initially know the exact directory depth of the application.

Eventually, I was able to access:

    /etc/passwd

---

## 4. Understanding the Path Traversal

The important concept was that:

    ../

moves one directory level upwards.

For example:

    ../../etc/passwd

means:

    current directory
        ↓
    ..
        ↓
    ..
        ↓
    /etc/passwd

The application was restricting direct access to the file, but the path traversal sequence allowed me to move outside the expected directory.

---

## 5. Finding the Flag

After confirming that I could read local files, I needed to find the flag.

The room indicated that the flag was located in the root directory of the filesystem.

I changed the requested file from:

    /etc/passwd

to:

    flag.txt

and used the same path traversal technique.

This allowed me to access:

    /flag.txt

and retrieve the flag.

---

## Attack Chain

    Nmap
      ↓
    Port 80
      ↓
    Lo-Fi web application
      ↓
    `page` parameter
      ↓
    Burp Suite Repeater
      ↓
    Test `/etc/passwd`
      ↓
    Path traversal with `../`
      ↓
    Local File Inclusion
      ↓
    Read `/etc/passwd`
      ↓
    Read `/flag.txt`
      ↓
    Flag

---

## Tools Used

### Nmap

    nmap -p- lofi.thm -sV --min-rate 10000

Used for port and service enumeration.

### Burp Suite

Used to intercept and modify HTTP requests and test the `page` parameter.

### Burp Repeater

Used to manually modify the request and test different file paths.

---

## Key Takeaways

- A parameter that controls which file is loaded can be an indicator of LFI.
- Burp Suite Repeater is useful for manually testing and modifying HTTP parameters.
- `../` is used for path traversal and moves one directory level upwards.
- If direct access to a local file fails, path traversal may bypass the application's validation.
- Once LFI is confirmed, test whether other sensitive local files can be read.
- Always think about where the target file is located and whether additional `../` traversal is required.

### LFI Mental Model

    User-controlled file parameter
              ↓
        Application includes file
              ↓
       Input validation bypass
              ↓
         `../` traversal
              ↓
       Local file disclosure