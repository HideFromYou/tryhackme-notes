# Gathering Information for Custom Wordlists

## Overview

Building an effective custom wordlist begins with **information gathering**. While generic wordlists provide broad coverage, they often miss organization-specific terminology, usernames, technologies, and naming conventions. By collecting publicly available information through **Open Source Intelligence (OSINT)**, penetration testers can create highly targeted wordlists that significantly improve the effectiveness of enumeration and password attacks.

This lesson demonstrates how to gather information from multiple OSINT sources, extract useful words and usernames, and prepare data for later wordlist generation. The process is commonly referred to as **harvesting**. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the importance of OSINT in wordlist creation
- Identify valuable public information sources
- Collect company-specific keywords and usernames
- Use common reconnaissance tools
- Generate username permutations from harvested information

---

## Main Content

### Why Gather Information?

Custom wordlists are most effective when they contain words that are relevant to the target organization.

A good custom wordlist combines:

- Company-specific keywords
- Technology-specific keywords
- Generic directories and endpoints

This approach improves the likelihood of discovering hidden resources, valid usernames, and realistic passwords during penetration testing.

---

### Common OSINT Sources

Several publicly available sources provide valuable information for building targeted wordlists.

These include:

- Professional networking platforms (LinkedIn)
- Company websites
- Social media accounts
- Job advertisements
- Public documentation

Information gathered from these sources may reveal:

- Employee names
- Product names
- Internal projects
- Technologies
- Naming conventions

---

### Basic Reconnaissance Methods

The lesson introduces several reconnaissance techniques commonly used during OSINT.

#### WHOIS

WHOIS lookups provide:

- Domain registration details
- Nameservers
- Contact information

These details help identify infrastructure associated with the target.

---

#### Subdomain Enumeration

Public tools and certificate transparency logs can reveal:

- Existing subdomains
- Email addresses
- Historical domain names

This information expands the attack surface and contributes additional words for custom lists.

---

#### Site Crawling

Website crawling extracts visible words from webpages.

The lesson introduces **CeWL**, which spiders websites and collects useful words and email addresses automatically.

Example output includes:

- Company terminology
- Navigation labels
- Product names
- Employee email addresses

---

#### Technology Fingerprinting

Identifying the technologies used by a target helps generate technology-specific wordlists.

Examples include:

- WordPress
- Laravel
- React
- AWS

Knowing the technology stack allows penetration testers to use specialized wordlists from collections such as **SecLists**.

---

### Gathering Words with CeWL

CeWL is used to crawl the target website and generate:

- `cewl_words.txt`
- `emails.txt`

Useful command options include:

- Crawl depth
- Minimum word length
- Lowercase conversion
- Email extraction
- Output files

These outputs provide organization-specific keywords and email addresses for later processing.

---

### Extracting Information from Documents

Publicly available PDF documents often contain valuable information.

The lesson demonstrates how to:

- Download PDF files using `wget`
- Extract readable strings
- Search documents for email addresses
- Build additional wordlists from document contents

Internal terminology found within documents often improves custom password and directory lists.

---

### Harvesting Usernames

Employee names are collected from the organization's social webpage.

Using `curl`, `grep`, and `awk`, several common username formats are generated, including:

- `firstname.lastname`
- `firstinitiallastname`
- `firstnamelastinitial`

Converting usernames to lowercase improves compatibility with authentication systems.

---

### Generated Files

By the end of the reconnaissance phase, several useful files have been created:

- `cewl_words.txt`
- `emails.txt`
- `raw_words.txt`
- `emails_docs.txt`
- `names.txt`
- `users_first.last.txt`
- `users_flast.txt`
- `users_firstl.txt`
- `users_from_emails.txt`

These files become the foundation for creating clean, customized wordlists in the next stage.

---

## Skills Practiced

- OSINT
- Information Gathering
- CeWL
- Website Crawling
- WHOIS
- Username Enumeration
- Linux Command Line
- Penetration Testing

---

## Key Takeaways

- Effective custom wordlists begin with thorough information gathering.
- OSINT sources such as company websites, LinkedIn, social media, job advertisements, and public documents provide valuable target-specific information.
- CeWL automates website crawling and extracts keywords and email addresses.
- Public documents often contain useful terminology and employee information that can enrich custom wordlists.
- Generating multiple username formats increases the likelihood of discovering valid accounts during authentication attacks.
