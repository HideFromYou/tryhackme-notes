# Creating and Cleaning Wordlists

## Overview

After gathering information from multiple OSINT sources, the resulting data is often unstructured and contains duplicate, inconsistent, or irrelevant entries. Before using these lists in penetration testing tools, they should be merged, normalized, filtered, and optimized.

This lesson demonstrates how to transform raw data into clean, efficient wordlists for directory enumeration and password attacks. It also introduces pattern-based password generation using **Crunch** to create targeted password lists. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Merge multiple wordlists
- Remove duplicate entries
- Normalize word formatting
- Filter irrelevant strings
- Generate custom username lists
- Create pattern-based password lists with Crunch

---

## Main Content

### Why Clean Wordlists?

Raw wordlists often contain:

- Duplicate entries
- Mixed uppercase and lowercase words
- Special characters
- Very short or irrelevant strings

Cleaning these lists improves both speed and effectiveness when using enumeration and brute-force tools.

---

### Merging Password Wordlists

The first step is combining words collected from different sources.

Examples include:

- Website keywords
- PDF document strings

The lesson merges these files and removes duplicate entries using:

```bash
cat cewl_words.txt raw_words.txt | sort -u > words_raw.txt
```

Using `sort -u` alphabetically sorts the list while removing duplicate lines. :contentReference[oaicite:1]{index=1}

---

### Normalizing and Filtering

The merged wordlist is then standardized.

The cleaning process includes:

- Converting uppercase letters to lowercase
- Removing Windows carriage returns
- Filtering malformed entries
- Removing duplicates

This produces a clean, consistent wordlist suitable for automated tools.

Typical output contains well-formed lowercase words with a minimum length requirement.

---

### Validating the Wordlist

After cleaning, the list should be reviewed to ensure it contains an appropriate number of useful entries.

Common validation commands include:

- Counting total entries
- Previewing the first few words

This helps determine whether the list is too small or unnecessarily large for the intended task.

---

### Merging Username Lists

Usernames generated from multiple OSINT techniques are merged into a single list.

Sources include:

- Email addresses
- Employee names
- Username permutations

Duplicate usernames are removed to create a clean authentication list.

---

### Pattern-Based Password Generation

Sometimes password formats are partially known.

The lesson demonstrates generating passwords using **Crunch**.

Example pattern:

```
Helios20%%!
```

The `%` placeholder represents digits, allowing Crunch to generate every matching password combination automatically.

This produces a focused password list that is significantly smaller and more efficient than generic password dictionaries. :contentReference[oaicite:2]{index=2}

---

### Final Output

At the end of the cleaning process, three primary files are available:

- `words_clean.txt` – Clean directory and keyword wordlist
- `users.txt` – Clean username list
- `pass_helios.txt` – Pattern-based password list

These optimized files are ready for practical use during enumeration and authentication attacks.

---

## Skills Practiced

- Wordlist Cleaning
- Data Normalization
- Linux Command Line
- Crunch
- Username Generation
- Password List Creation
- Penetration Testing

---

## Key Takeaways

- Cleaning wordlists removes unnecessary entries and improves efficiency.
- Normalization ensures consistent formatting across all entries.
- Duplicate removal reduces wasted processing time.
- Crunch generates highly targeted password lists when password patterns are known.
- Clean, optimized wordlists significantly improve the performance of tools such as Hydra and ffuf. :contentReference[oaicite:3]{index=3}