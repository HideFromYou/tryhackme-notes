# Web Application Fundamentals

## Overview

This section covers the core concepts required to understand how modern web applications function before moving into web exploitation. It focuses on reconnaissance, HTTP communication, content discovery, application architecture, web technologies, and server identification.

The rooms in this module build a solid foundation for web application penetration testing by teaching how to identify technologies, understand application behaviour, and recognise common attack surfaces through structured enumeration rather than blind exploitation.

---

## Learning Objectives

After completing this module, you should be able to:

- Understand how web applications communicate over HTTP
- Perform passive and active web reconnaissance
- Identify common web technologies and frameworks
- Discover hidden application content
- Fingerprint web servers and technology stacks
- Recognise common server misconfigurations
- Understand Windows and Linux web hosting environments
- Build an evidence-driven web enumeration methodology

---

## Rooms Covered

| # | Room | Topics |
|---|------|--------|
| 01 | Walking in Web Applications | Browser Developer Tools, HTML, JavaScript, Cookies, Storage, Network Analysis |
| 02 | Content Discovery | Manual Enumeration, OSINT, Search Engines, Git Repositories, Gobuster, Virtual Hosts |
| 03 | Stack Fingerprinting | MERN, Express, React, Next.js, Django, LAMP, Nikto |
| 04 | Web Server Fingerprinting | Apache, Nginx, Python HTTP Server, Express, Server Identification |
| 05 | Attacking IIS | IIS Enumeration, WebDAV, ASP.NET, Windows Authentication, IIS Misconfigurations |

---

## Skills Practiced

### Web Fundamentals

- HTTP & HTTPS
- Request / Response Analysis
- Browser Developer Tools
- Client-Server Architecture
- Web Technologies

### Reconnaissance

- Passive Reconnaissance
- Active Reconnaissance
- Content Discovery
- Directory Enumeration
- Virtual Host Discovery
- OSINT
- Technology Fingerprinting

### Web Servers

- Apache HTTP Server
- Nginx
- Python HTTP Server
- Microsoft IIS
- Node.js (Express)

### Web Frameworks

- Express.js
- React
- Next.js
- Django
- LAMP Stack

### Security Assessment

- HTTP Header Analysis
- Server Fingerprinting
- Stack Identification
- Configuration Review
- Information Disclosure Analysis
- Authentication Enumeration
- WebDAV Assessment

### Automation

- Nmap
- Nmap NSE Scripts
- Nikto
- curl
- Browser Developer Tools

---

## Methodology

Throughout this module, a consistent methodology is followed:

1. Identify the target technology.
2. Gather information using passive techniques.
3. Validate findings through controlled enumeration.
4. Identify exposed services and configurations.
5. Research framework-specific behaviours.
6. Perform focused security assessments based on collected evidence.

This structured workflow reduces unnecessary noise while improving the quality of penetration testing.

---

## Key Takeaways

- Reconnaissance is the foundation of every successful web assessment.
- Accurate fingerprinting enables targeted vulnerability research.
- Modern web applications rely on diverse technologies that expose unique characteristics.
- Understanding web servers and frameworks improves both offensive and defensive security skills.
- Manual analysis and automated tooling complement one another and should be used together.
- Effective penetration testing begins with understanding how an application works before attempting to exploit it.

---

## Tools Used Throughout This Module

- Browser Developer Tools
- curl
- Nmap
- Nmap NSE
- Nikto
- Gobuster
- Search Engines
- Git Repositories
- HTTP Header Inspection

---

## Overall Outcome

By completing **Web Application Fundamentals**, you gain the practical knowledge required to confidently enumerate modern web applications, identify their underlying technologies, analyse their behaviour, and prepare for more advanced web exploitation techniques covered in later learning paths.