# Manual Discovery - Common Files

## Overview

Before using automated tools, a significant amount of information can be gathered through manual exploration. Many web applications expose standard files that provide valuable insight into the application's structure, search engine indexing, and publicly accessible resources.

---

## Learning Objectives

- Understand the purpose of common web files
- Learn how to manually inspect a website
- Identify resources useful during reconnaissance
- Discover information that assists later enumeration

---

## Common Files

Several files are commonly found in the root directory of a web application.

Examples include:

- robots.txt
- sitemap.xml
- favicon.ico
- security.txt
- humans.txt

These files may reveal hidden directories, important URLs, or details about the application.

---

## robots.txt

The `robots.txt` file provides instructions to search engine crawlers regarding which resources should or should not be indexed.

Although intended for search engines, it often exposes:

- Administrative directories
- Development pages
- Backup folders
- Restricted content

Its contents should always be reviewed during reconnaissance.

---

## sitemap.xml

The `sitemap.xml` file lists pages that website owners want search engines to index.

Useful information may include:

- Public endpoints
- Archived content
- Hidden pages
- API documentation
- Application structure

Large applications often expose hundreds of URLs through their sitemap.

---

## favicon.ico

Every website usually includes a favicon.

Although small, it can help identify:

- Web frameworks
- CMS platforms
- Default application installations
- Third-party products

Fingerprinting favicons can provide additional context about the target technology.

---

## Other Public Files

Additional files sometimes encountered include:

- README files
- CHANGELOG files
- Backup files
- Configuration samples
- Documentation

Although not always present, they may reveal valuable operational information.

---

## Why Manual Discovery Matters

Manual inspection is quick, requires no specialised tools, and often uncovers resources that guide later automated discovery.

It also helps analysts understand the application's overall structure before generating large numbers of requests.

---

## Skills Practiced

- Manual web reconnaissance
- Directory inspection
- Public file discovery
- Attack surface identification

---

## Key Takeaways

- Standard files often expose valuable information.
- robots.txt and sitemap.xml should always be inspected.
- Favicons can assist with technology fingerprinting.
- Manual discovery provides context before automated enumeration.
- Small findings frequently lead to larger discoveries.