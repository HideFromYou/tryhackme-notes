# CyberHeroes / Superheroes

## Enumeration

I started with a basic Nmap scan to identify open ports and running services:

    sudo nmap -sC -sV -Pn <IP_ADDRESS>

The scan revealed:

    22/tcp → OpenSSH 8.2p1
    80/tcp → Apache httpd 2.4.48

Port 80 was hosting a webpage titled:

    CyberHeroes

---

## Directory Enumeration

I used Gobuster to search for hidden directories:

    gobuster dir -u http://<IP_ADDRESS> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50

The enumeration did not reveal anything particularly useful.

I then manually explored the website.

---

## Web Enumeration

The homepage contained a `Login` option.

I opened the login page and inspected its source code using:

    Ctrl + U

Instead of immediately trying to brute-force the login, I searched the source for:

    flag

This revealed hidden values that contained credentials.

I found:

    Username: h3ck3rBoi
    Password: 54321@terceSrepuS

The password looked reversed.

---

## Password Decoding

I used the Linux `rev` command to reverse the string:

    echo "54321@terceSrepuS" | rev

The result was:

    SuperSecret@12345

So the credentials were:

    Username: h3ck3rBoi
    Password: SuperSecret@12345

---

## Login

I used the discovered credentials to log into the application.

After logging in, the flag was revealed:

    flag{edb0be532c540b1a150c3a7e85d2466e}

---

## Attack Chain

    Nmap
      ↓
    Ports 22 / 80
      ↓
    Web Enumeration
      ↓
    Gobuster
      ↓
    Login Page
      ↓
    Inspect Page Source
      ↓
    Hidden Credentials
      ↓
    Reversed Password
      ↓
    rev
      ↓
    Valid Credentials
      ↓
    Login
      ↓
    Flag

---

## Tools & Commands

### Nmap

    sudo nmap -sC -sV -Pn <IP_ADDRESS>

Used to identify open ports, services, and versions.

### Gobuster

    gobuster dir -u http://<IP_ADDRESS> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50

Used for directory enumeration.

### rev

    echo "54321@terceSrepuS" | rev

Used to reverse the discovered password string.

---

## Key Takeaways

- Start with basic enumeration before attacking the application.
- Always inspect the page source when dealing with a web application.
- Search the source code for interesting keywords such as `flag`, `password`, `username`, and other clues.
- Do not assume that a strange-looking string is encrypted; it may simply be reversed or encoded.
- Simple Linux utilities such as `rev` can be useful during enumeration.
- Methodical enumeration can reveal credentials without requiring brute-force attacks.