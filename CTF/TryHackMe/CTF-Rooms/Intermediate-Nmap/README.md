# Intermediate Nmap

## Overview

This room focused mainly on using Nmap effectively and then combining the information discovered during enumeration with other tools.

The main attack chain was:

    Nmap
      ↓
    Identify unusual ports/services
      ↓
    Enumerate port 31337
      ↓
    Discover username/password
      ↓
    Test SSH services
      ↓
    SSH on port 22
      ↓
    Enumerate filesystem/users
      ↓
    Find another user's directory
      ↓
    Read flag

---

## 1. Nmap Enumeration

I started with a full TCP scan with service and default-script detection:

    nmap -sV -sC -p- 10.10.250.121

### Nmap Options

- `-sV` → Detect service versions
- `-sC` → Run default Nmap scripts
- `-p-` → Scan all TCP ports

The scan revealed:

- Port `22` → SSH
- Port `2222` → SSH
- Port `31337` → Unknown/unusual service

The Nmap output also exposed login information associated with the service on port `31337`:

    Username: ubuntu
    Password: Dafdas!!/str0ng

### Observation

The unusual port `31337` immediately stood out because there was no clear service identification.

The Nmap output itself also provided credentials, so I had something concrete to investigate.

---

## 2. Enumerating Port 31337

I connected directly to the unknown service using Netcat:

    nc 10.10.250.121 31337

The response confirmed that the service was accessible.

This also matched the information observed during the Nmap scan.

### Observation

When Nmap identifies an unusual/unknown service, manually connecting to the port with a tool such as `nc` can provide additional information.

---

## 3. Testing SSH on Port 2222

Since I had credentials for:

    ubuntu : Dafdas!!/str0ng

I first tested them against the non-standard SSH port:

    ssh ubuntu@10.10.250.121 -p 2222

The login failed because the SSH service on port `2222` required public-key authentication.

### Observation

Having valid credentials does not necessarily mean they can be used against every service.

The authentication method also matters.

---

## 4. Testing SSH on Port 22

I then tried the same credentials against the standard SSH port:

    ssh ubuntu@10.10.250.121 -p 22

This time the credentials worked and I obtained shell access as:

    ubuntu

---

## 5. Local Enumeration

After gaining SSH access, I inspected the filesystem and looked for interesting files and other users.

My own directory did not contain anything useful.

I then searched for other users on the system.

Another user was present, so I investigated that user's home directory.

---

## 6. Finding the Flag

Inside the other user's directory I found the flag.

The flag was:

    flag{251f309497a18888dde5222761ea88e4}

---

## Attack Chain

    nmap -sV -sC -p-
            ↓
    22 / 2222 / 31337
            ↓
    Investigate unusual port 31337
            ↓
    nc <TARGET_IP> 31337
            ↓
    Discover ubuntu credentials
            ↓
    Test SSH :2222
            ↓
    Public-key authentication required
            ↓
    Test SSH :22
            ↓
    SSH access as ubuntu
            ↓
    Enumerate filesystem/users
            ↓
    Find another user's directory
            ↓
    Find flag

---

## Tools Used

### Nmap

    nmap -sV -sC -p- <TARGET_IP>

Used for:

- Full port enumeration
- Service detection
- Version detection
- Default NSE scripts

### Netcat

    nc <TARGET_IP> 31337

Used to manually interact with the unusual service discovered on port `31337`.

### SSH

    ssh ubuntu@<TARGET_IP> -p 2222
    ssh ubuntu@<TARGET_IP> -p 22

Used to test the discovered credentials against the available SSH services.

---

## Key Takeaways

- `-p-` scans all TCP ports, including non-standard ones.
- `-sV` helps identify services and their versions.
- `-sC` runs Nmap's default scripts and can sometimes reveal useful information.
- Do not ignore unusual ports just because Nmap cannot clearly identify the service.
- When Nmap reveals credentials, test them against the relevant services.
- Different SSH ports can have different authentication configurations.
- If one authentication method fails, investigate the other exposed services instead of assuming the credentials are invalid.
- After obtaining shell access, continue with local enumeration and look for other users and interesting files.