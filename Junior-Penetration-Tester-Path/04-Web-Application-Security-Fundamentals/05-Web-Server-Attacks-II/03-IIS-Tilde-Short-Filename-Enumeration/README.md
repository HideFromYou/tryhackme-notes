# IIS Tilde (Short Filename) Enumeration

## Overview

Windows file systems support legacy 8.3 short filenames for compatibility purposes. Under certain IIS configurations, these shortened names may unintentionally reveal the existence of files and directories that are not directly accessible through standard browsing.

Understanding this behaviour helps security professionals identify hidden resources during reconnaissance.

---

## Learning Objectives

- Understand Windows 8.3 filenames
- Learn the purpose of short filename enumeration
- Recognise information disclosure risks
- Understand why hidden files may still be discoverable

---

## Short Filenames

Windows may generate abbreviated filenames consisting of:

- A shortened file name
- A tilde (`~`)
- A numeric identifier

These legacy names allow compatibility with older applications.

---

## Information Disclosure

If improperly configured, IIS may reveal:

- Hidden directories
- Backup files
- Configuration files
- Application resources

This information can significantly improve later reconnaissance.

---

## Why It Matters

Hidden resources often contain:

- Documentation
- Backup copies
- Configuration data
- Development artifacts

Discovering these files provides additional context without directly accessing sensitive content.

---

## Defensive Considerations

Administrators should:

- Disable unnecessary legacy features
- Remove obsolete files
- Restrict directory exposure
- Review IIS configuration regularly

---

## Skills Practiced

- IIS enumeration
- Information disclosure analysis
- Windows reconnaissance
- Attack surface identification

---

## Key Takeaways

- Legacy filename compatibility can expose useful information.
- Hidden resources may still be discoverable.
- Information disclosure supports further reconnaissance.
- Proper server configuration reduces unnecessary exposure.
- Enumeration should remain systematic and evidence-based.