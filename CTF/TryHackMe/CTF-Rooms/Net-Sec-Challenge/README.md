# THM: Net Sec Challenge

## 1. Room Information

- **Name:** Net Sec Challenge
- **Difficulty:** Medium
- **Estimated Time:** 60 min
- **Platform:** TryHackMe
- **Focus:** Network enumeration, service discovery, banner grabbing, FTP brute forcing, and Nmap IDS evasion

---

## 2. Introduction

This room focused on practical network enumeration and identifying information exposed by different network services.

My main objectives were to:

- Identify open TCP ports.
- Enumerate services and their versions.
- Grab service banners.
- Discover information exposed through HTTP and SSH.
- Brute-force FTP credentials using Hydra.
- Access files through an FTP service running on a non-standard port.
- Perform an Nmap scan while attempting to evade IDS detection.

---

# 3. Enumeration

## 3.1 Scanning Ports 1-10,000

I started by scanning the first 10,000 TCP ports:

```bash
nmap TARGET -p 1-10000
```

The highest open port below 10,000 was:

```text
8080
```

### Finding

**Answer:** `8080`

---

## 3.2 Scanning Ports Above 10,000

I then scanned the higher port range:

```bash
nmap TARGET -p 10000-65535
```

This revealed another open port:

```text
10021
```

### Finding

**Answer:** `10021`

This was interesting because the service was running outside the common top 1000 TCP ports, so a default Nmap scan would not necessarily identify it.

---

## 3.3 Number of Open TCP Ports

After completing the scans, I identified a total of:

```text
6
```

open TCP ports.

### Finding

**Answer:** `6`

---

# 4. HTTP Banner Grabbing

## 4.1 Connecting to Port 80

Since HTTP was running on port 80, I used Telnet to manually interact with the service:

```bash
telnet TARGET 80
```

I then sent an HTTP request:

```http
GET HTTP/1.1
```

After pressing Enter twice, the server returned its HTTP response headers.

One of the headers contained the room flag.

### Finding

```text
THM{web_server_25352}
```

**Answer:** `THM{web_server_25352}`

### What I Learned

A web server can expose useful information through its HTTP response headers. Manually connecting to a service with tools such as Telnet is a simple way to perform basic banner grabbing and understand exactly what the server returns.

---

# 5. SSH Banner Grabbing

## 5.1 Connecting to Port 22

I repeated the same idea against the SSH service:

```bash
telnet TARGET 22
```

The SSH server immediately returned its banner, which contained another flag.

### Finding

```text
THM{946219583339}
```

**Answer:** `THM{946219583339}`

### What I Learned

Some network services send information immediately after establishing a TCP connection. This is why manually connecting to a service can sometimes reveal information before authentication is even attempted.

---

# 6. FTP Enumeration

## 6.1 Identifying the FTP Version

The FTP service was running on a non-standard port, so I used Nmap service/version detection:

```bash
nmap TARGET -p- -sV
```

Since I already knew the relevant port range, I could also scan it directly:

```bash
nmap TARGET -p 1-10021 -sV
```

The FTP service was identified as:

```text
vsftpd 3.0.5
```

### Finding

**FTP Version:** `vsftpd 3.0.5`

### What I Learned

Port numbers alone do not tell me what service is actually running. Using `-sV` allows me to fingerprint the service and obtain version information, which can later be useful when researching vulnerabilities or deciding how to interact with the service.

---

# 7. FTP Credential Attacks

## 7.1 Brute-Forcing `eddie`

The challenge provided two usernames obtained through social engineering:

```text
eddie
quinn
```

I first attempted to brute-force `eddie's` password using Hydra and the `rockyou.txt` wordlist.

Because FTP was running on port `10021`, I had to specify the custom port with Hydra's `-s` option:

```bash
hydra -l eddie -P /usr/share/wordlists/rockyou.txt TARGET -s 10021 ftp
```

Hydra successfully recovered the password:

```text
jordan
```

I then connected to the FTP service:

```bash
ftp eddie@TARGET 10021
```

After authenticating, I listed the contents:

```text
ls
```

The directory was empty, so `eddie` did not contain the flag I was looking for.

---

## 7.2 Brute-Forcing `quinn`

I then repeated the same attack against `quinn`:

```bash
hydra -l quinn -P /usr/share/wordlists/rockyou.txt TARGET -s 10021 ftp
```

Hydra recovered the password:

```text
andrea
```

I connected using:

```bash
ftp quinn@TARGET 10021
```

After authentication, I listed the directory:

```text
ls
```

This time, I found:

```text
ftp_flag.txt
```

I downloaded the file:

```text
get ftp_flag.txt
```

I then viewed the downloaded file locally.

### Finding

```text
THM{321452667098}
```

**Answer:** `THM{321452667098}`

### What I Learned

This part reinforced the importance of checking non-standard service ports and testing credentials when the challenge provides valid usernames.

The important details were:

- FTP was running on port `10021`.
- Hydra needed the custom port specified.
- `eddie` had a valid password but no useful file.
- `quinn` had access to the directory containing the flag.

---

# 8. Nmap IDS Evasion

## 8.1 The Challenge on Port 8080

Browsing to:

```text
http://TARGET:8080
```

displayed another challenge.

The objective was to perform network enumeration while avoiding detection by the IDS.

This changed my approach from simply finding open ports to considering **how the scan itself could be detected**.

---

## 8.2 TCP Null Scan

I used the following Nmap command:

```bash
nmap TARGET -f -Pn -sN
```

The important options were:

### `-f`

Fragments IP packets when sending them.

The idea is to make packet inspection more difficult for some network security devices.

### `-Pn`

Tells Nmap to skip host discovery and treat the target as already online.

Since I already knew the target was reachable, there was no need to perform a separate ping discovery phase.

### `-sN`

Performs a TCP Null scan.

The TCP packets are sent without any TCP flags set.

The response behavior can then be used to determine whether ports are open or closed.

---

## 8.3 Result

The scan successfully completed the challenge and revealed the final flag:

```text
THM{f7443f99}
```

**Answer:** `THM{f7443f99}`

### What I Learned

This was the most interesting part of the room because it introduced the idea that **enumeration itself can be detected**.

When performing a penetration test, I should not only think:

> "How do I find the open ports?"

I should also think:

> "What will the target's defensive controls see while I am doing it?"

Different scan techniques generate different network traffic patterns, and understanding those differences is important when performing realistic assessments.

---

# 9. Attack / Enumeration Flow

My overall workflow for the room was:

```text
Port Enumeration
       |
       +--> 1-10000
       |      |
       |      +--> Port 8080
       |
       +--> 10000-65535
              |
              +--> Port 10021
                     |
                     +--> FTP
                     |
                     +--> Service Version
                     |      |
                     |      +--> vsftpd 3.0.5
                     |
                     +--> Credential Attack
                            |
                            +--> eddie
                            |      |
                            |      +--> jordan
                            |
                            +--> quinn
                                   |
                                   +--> andrea
                                          |
                                          +--> ftp_flag.txt

Port 80
   |
   +--> Telnet
          |
          +--> HTTP Banner
                 |
                 +--> THM{web_server_25352}

Port 22
   |
   +--> Telnet
          |
          +--> SSH Banner
                 |
                 +--> THM{946219583339}

Port 8080
   |
   +--> IDS Evasion Challenge
          |
          +--> Nmap Fragmentation
          +--> TCP Null Scan
                 |
                 +--> THM{f7443f99}
```

---

# 10. Key Findings

| Technique | Result |
|---|---|
| TCP port scanning | Identified 6 open TCP ports |
| High-port enumeration | Found FTP on port 10021 |
| Service fingerprinting | Identified vsftpd 3.0.5 |
| HTTP banner grabbing | Retrieved `THM{web_server_25352}` |
| SSH banner grabbing | Retrieved `THM{946219583339}` |
| FTP brute force | Recovered credentials for `eddie` and `quinn` |
| FTP enumeration | Retrieved `ftp_flag.txt` |
| IDS evasion | Completed challenge using Nmap packet fragmentation and TCP Null scanning |

---

# 11. Flags

```text
HTTP:
THM{web_server_25352}

SSH:
THM{946219583339}

FTP:
THM{321452667098}

IDS Evasion:
THM{f7443f99}
```

---

# 12. Key Takeaways

This room reinforced several practical enumeration techniques that I want to remember during a pentest:

- Do not rely only on the default Nmap top-1000 scan.
- Always consider scanning the full TCP range when the scope allows it.
- Use `-sV` to identify service versions.
- Manually interact with services when banner information may be exposed.
- Remember that services can run on non-standard ports.
- Hydra can be useful for testing weak credentials when valid usernames are known.
- Always enumerate the contents available to successfully authenticated accounts.
- Think about how scanning traffic appears from the defender's perspective.
- Different Nmap scan types produce different network behavior.
- Enumeration is not always invisible; IDS/IPS controls can detect aggressive or recognizable scanning patterns.

The main lesson I took from this room is that **good reconnaissance is not just about finding services — it is about understanding what each service exposes, how I can interact with it, and how my own activity may be detected.**