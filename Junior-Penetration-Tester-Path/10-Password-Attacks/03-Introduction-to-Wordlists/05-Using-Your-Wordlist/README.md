# Using Your Wordlist

## Overview

After gathering, cleaning, and optimizing custom wordlists, the final step is putting them into practice. This lesson demonstrates how tailored wordlists improve both **directory enumeration** and **authentication attacks** by using two common penetration testing tools: **ffuf** and **Hydra**.

Rather than relying on large generic lists, customized wordlists built from OSINT provide faster, more accurate results by targeting organization-specific terminology and username conventions. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Use custom wordlists with ffuf
- Perform directory enumeration
- Use Hydra with username and password lists
- Understand Hydra's HTTP POST module
- Interpret brute-force results
- Apply customized wordlists during penetration tests

---

## Main Content

### Directory Enumeration with ffuf

The first practical use of the custom wordlist is discovering hidden directories on a web server.

The lesson demonstrates using **ffuf** to test every entry from `words_clean.txt` against the target website.

Example command:

```bash
ffuf -w words_clean.txt \
-u http://tryfinanceme.local/FUZZ \
-e .php,.html,/ \
-mc 200,301,302
```

Important options include:

| Option | Description |
|---------|-------------|
| `-w` | Wordlist to use |
| `-u` | Target URL containing the `FUZZ` keyword |
| `-e` | File extensions to test |
| `-mc` | HTTP status codes to display |

The scan reports only successful pages or redirects, helping identify hidden resources efficiently. :contentReference[oaicite:1]{index=1}

---

### Handling False Positives

Some web servers return identical responses for nonexistent pages.

To reduce false positives, ffuf supports filtering by:

- Response size (`-fs`)
- Number of lines (`-fl`)

These filters improve scan accuracy by ignoring common error pages.

---

### Discovering Hidden Resources

Using the customized wordlist allows ffuf to identify hidden directories that generic wordlists might miss.

In the practical exercise, directory enumeration reveals the hidden path:

```
/helios/
```

This directory contains the application's login page and becomes the next attack target. :contentReference[oaicite:2]{index=2}

---

### Brute-Forcing the Login Form with Hydra

Once the login page is discovered, **Hydra** is used to test combinations of usernames and passwords.

The lesson uses:

- `users.txt`
- `pass_helios.txt`

Example command:

```bash
hydra -L users.txt -P pass_helios.txt \
-f -V -t 4 \
tryfinanceme.local \
http-post-form \
'/helios/login.php:username=^USER^&password=^PASS^:S=THM{'
```

Important options include:

| Option | Description |
|---------|-------------|
| `-L` | Username list |
| `-P` | Password list |
| `-f` | Stop after the first valid credential |
| `-V` | Verbose output |
| `-t` | Number of concurrent threads |

Hydra replaces the `^USER^` and `^PASS^` placeholders with values from the supplied wordlists until valid credentials are found. :contentReference[oaicite:3]{index=3}

---

### Successful Authentication

When Hydra identifies valid credentials, it displays:

- Username
- Password

The discovered credentials can then be used to authenticate to the application and verify successful access during the penetration test.

---

## Skills Practiced

- ffuf
- Hydra
- Directory Enumeration
- HTTP Fuzzing
- Authentication Testing
- Wordlist Usage
- Penetration Testing

---

## Key Takeaways

- Customized wordlists greatly improve the effectiveness of directory enumeration.
- ffuf uses tailored wordlists to discover hidden web resources.
- Hydra combines username and password lists to perform HTTP login brute-force attacks.
- Filtering ffuf results helps eliminate false positives during enumeration.
- Combining OSINT-derived wordlists with automated tools increases the success rate of penetration testing engagements. :contentReference[oaicite:4]{index=4}