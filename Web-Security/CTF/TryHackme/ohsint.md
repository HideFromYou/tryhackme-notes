# TryHackMe - OhSINT

## Overview
Completed the OhSINT TryHackMe challenge room, focusing on Open Source Intelligence (OSINT), metadata analysis, social media investigation, WiFi geolocation, and digital footprint analysis.

This challenge simulated a realistic reconnaissance workflow where publicly accessible information was used to build a complete intelligence profile from a single image.

---

## Skills Practiced

- OSINT methodology
- Metadata extraction
- Username pivoting
- Social media investigation
- WiFi geolocation
- Public information correlation
- Hidden content discovery
- Digital footprint analysis
- Reconnaissance methodology

---

## Methodology

### Initial Artifact Analysis
The investigation began with analysis of the provided image file.

Metadata extraction was performed to identify useful embedded information.

Key discovery:

- author / copyright metadata
- unique username identifiers

This provided the initial pivot point.

---

### Username Pivoting
The discovered username was used across public platforms to identify linked accounts.

Investigation expanded into:

- social media profiles
- public code repositories
- personal web presence

This allowed correlation of multiple public identities.

---

### Social Media Investigation
Public social profiles exposed useful intelligence, including:

- profile imagery
- wireless access point identifiers
- personal clues
- location-related information

This provided additional pivot opportunities.

---

### WiFi Geolocation
A discovered wireless BSSID was used for public WiFi intelligence lookup.

This enabled:

- access point identification
- SSID discovery
- location correlation

This demonstrated real-world wireless OSINT techniques.

---

### Public Profile Enumeration
Additional public platforms revealed:

- email addresses
- geographic location
- platform-linked identifiers

This demonstrated the importance of digital footprint awareness.

---

### Website Investigation
A personal blog exposed further intelligence.

Investigation included:

- public content analysis
- source code inspection
- hidden content discovery

This revealed sensitive information embedded within page source.

---

## Tools Used

- exiftool
- Google dorking
- Wigle.net
- Browser developer tools
- curl
- Twitter investigation
- GitHub investigation
- WordPress/blog analysis
- public OSINT methodology
- TryHackMe challenge environment

---

## Security Lessons Learned

### Metadata Exposure
Files often contain sensitive hidden metadata.

Best practices:

- strip metadata before publishing
- review uploaded media
- minimize exposed author information

---

### Digital Footprint Awareness
Small public clues across multiple platforms can be chained into complete intelligence profiles.

Best practices:

- reduce unnecessary public exposure
- review linked accounts
- separate personal identities where appropriate

---

### Hidden Information Exposure
Sensitive data hidden in page source is still publicly accessible.

Best practices:

- never store secrets in client-side content
- review published HTML source
- secure sensitive application data

---

## Key Takeaways

This room reinforced practical understanding of:

- OSINT investigation workflows
- metadata intelligence gathering
- username pivoting
- digital footprint analysis
- wireless geolocation intelligence
- real-world reconnaissance methodology
