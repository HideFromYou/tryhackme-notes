# 01 - Wireless Security


## Overview


Wireless technologies have played a key role in enabling connectivity between devices, allowing data exchange without physical connections.


However, these technologies may introduce security weaknesses that attackers can exploit to compromise sensitive data.


This room covers the fundamentals of wireless networking, common wireless technologies, their use cases, security risks, attack vectors, and basic security measures.


## Learning Objectives


By the end of this room, you should be able to:


- Understand the fundamentals of wireless networking, including how devices communicate over radio frequencies
- Identify common wireless technologies such as Wi-Fi, Bluetooth, NFC, and RFID
- Recognise common security risks and attack vectors associated with wireless technologies
- Apply basic security measures to protect wireless networks from common threats


## Prerequisites


A basic understanding of networking concepts is recommended.


---


# 01 - Introduction


## Wireless Frequency Spectrum


Wireless technologies operate across different parts of the radio-frequency spectrum.


| Technology | Frequency | Use |
|---|---|---|
| RFID | 125 KHz – 960 MHz | Asset tracking and access control |
| NFC | 13.56 MHz | Contactless payments and data transfer |
| Bluetooth | 2.4 GHz | Short-range device pairing and data exchange |
| Wi-Fi | 2.4 GHz & 5 GHz | Wireless LAN connectivity using 802.11 standards |


### Frequency and Range


```text
Lower Frequency
      ↓
Longer Range


Higher Frequency
      ↓
Shorter Range

Bluetooth and Wi-Fi both use the 2.4 GHz frequency band, which can cause interference between devices.

Wireless technologies allow modern environments to exchange data without physical connections, but understanding how they operate is important because their wireless nature can introduce additional attack surfaces.

02 - Wi-Fi Network Fundamentals

Wi-Fi allows devices to connect to the Internet and communicate using radio signals instead of physical cables.

It is commonly found in:

Homes
Offices
Coffee shops
Airports
Wi-Fi Components
Access Point (AP)

The Access Point broadcasts the Wi-Fi signal and acts as a bridge between wireless devices and the wired network behind it.

A home router is an example of an AP.

Clients

Clients are devices connecting to an AP to access internal resources or the Internet.

Examples:

Mobile phones
Laptops
Tablets
Printers
Smart devices

Each device has a wireless Network Interface Card (NIC) responsible for sending and receiving radio signals.

Wi-Fi Identifiers
SSID

Service Set Identifier

The human-readable network name displayed when searching for available Wi-Fi networks.

Example:

Office_WiFi
BSSID

Basic Service Set Identifier

The unique identifier of an Access Point, usually represented by the MAC address of its wireless interface.

Example:

00:1A:2B:3C:4D:5E
Wi-Fi Frequency Bands
2.4 GHz

Advantages:

Better range
Can pass through walls and floors more easily
Up to around 45 metres indoors
Speeds up to around 600 Mbps

Disadvantages:

More congested
Microwave ovens can interfere
Bluetooth devices can interfere
Baby monitors can interfere
Other Wi-Fi networks can interfere
5 GHz

Advantages:

Faster
Less congested
Up to around 1300 Mbps

Disadvantages:

Shorter range
More affected by physical obstacles
Around 15 metres indoors
Association Process

When a device joins a Wi-Fi network, the general process is:

1. Scan
   ↓
2. Select & Associate
   ↓
3. Authenticate
   ↓
4. Key Exchange
   ↓
5. Transmit
1. Scan

The device scans the area for available networks.

2. Select & Associate

The device selects a network and sends an association request.

3. Authenticate

The device and AP exchange authentication details.

4. Key Exchange

Encryption keys are negotiated so traffic can be protected.

5. Transmit

Data transmission begins.

Open System Authentication

With Open System Authentication, the AP does not actually verify credentials during the authentication step.

This occurs in:

WPA2-Personal
WPA2-Enterprise

With WPA2-Personal, the device then uses the 4-way handshake to prove that it knows the pre-shared key.

With WPA2-Enterprise using 802.1X, the device associates first and is then handed off to an authentication server such as RADIUS for credential-based authentication.

Factors Affecting Wi-Fi Signals
Physical Barriers

Walls, floors and ceilings weaken Wi-Fi signals.

Concrete and metal have particularly strong effects.

Distance

The further a device is from the AP, the weaker and less reliable the connection becomes.

Interference

Electronic devices operating on similar frequencies can disrupt wireless signals.

Examples:

Microwave ovens
Bluetooth devices
Other Wi-Fi networks
Channel Congestion

Multiple networks operating on overlapping channels can cause performance issues due to signal congestion and competition.

Signal Leakage

Wireless signals can extend beyond intended physical boundaries and reach:

Streets
Parking lots
Adjacent offices

This increases exposure if the network is not properly managed.

03 - Wi-Fi Security

Wi-Fi follows the IEEE 802.11 standards, which define how wireless devices connect and communicate.

IEEE 802.11 Standards
Standard	Generation	Year	Frequency	Key Improvement
802.11	—	1997	2.4 GHz	First Wi-Fi standard, 2 Mbps
802.11b	—	1999	2.4 GHz	First widely adopted standard, 11 Mbps
802.11g	—	2003	2.4 GHz	Improved speed, 54 Mbps, backward compatible with 802.11b
802.11n	Wi-Fi 4	2009	2.4 / 5 GHz	Dual-band, MIMO, up to 600 Mbps
802.11ac	Wi-Fi 5	2013	5 GHz	Up to 6.9 Gbps, MU-MIMO
802.11ax	Wi-Fi 6 / 6E	2021	2.4 / 5 / 6 GHz	OFDMA, up to 9.6 Gbps, designed for dense environments
802.11be	Wi-Fi 7	2024	2.4 / 5 / 6 GHz	Multi-Link Operation, 320 MHz channels, up to 46 Gbps

Wi-Fi 5 and Wi-Fi 6 are commonly deployed in enterprises because they work well with modern laptops, smartphones and access points.

Authentication and Encryption

Secure Wi-Fi communication relies on two key components:

Authentication
      +
Encryption
Authentication

Controls who can connect to the network.

Encryption

Protects transmitted data.

Wi-Fi Security Protocols
Protocol	Encryption	Status	Description
WEP	RC4	BROKEN	Uses RC4 with short, reused IVs, allowing the encryption key to be recovered
WPA	RC4 + TKIP	DEPRECATED	Introduced TKIP to improve WEP key management
WPA2	AES-CCMP	WIDELY USED	Replaced TKIP with AES-based encryption
WPA3	AES-GCMP	RECOMMENDED	Uses SAE and provides stronger protection against password-based attacks
WEP

WEP is considered insecure.

Its weaknesses include:

RC4 stream cipher
Short IVs
Reused IVs
Key recovery
WPA

WPA was introduced to address major weaknesses in WEP.

It uses:

RC4 + TKIP
WPA2

WPA2 replaced TKIP with:

AES-CCMP

It remains widely deployed.

WPA3

WPA3 introduces:

SAE

Simultaneous Authentication of Equals provides stronger protection against offline dictionary attacks.

Common Wi-Fi Weaknesses
Outdated security protocols such as WEP
Weak passwords
Unnecessary WPS
Default administrative credentials
Common Wi-Fi Attack Concepts
Password Attacks

Brute-forcing or cracking weak Wi-Fi passwords.

Rogue Access Point

An unauthorised access point connected to a network without the knowledge of the network administrator.

It can be:

Intentionally deployed by an attacker
Accidentally introduced by an employee
Evil Twin Attack

A fake access point that mimics a legitimate network by using the same SSID.

Unlike a rogue access point, an evil twin operates independently and relies on tricking users into connecting to it.

Possible objectives include:

Traffic interception
Credential capture
Deauthentication Attack

Forcing devices to disconnect from a network.

Traffic Interception

Attempting to capture wireless traffic when encryption is weak or improperly configured.

Protecting Wi-Fi Networks
Use WPA2 or WPA3

Use strong passphrases to protect against unauthorised network access.

Turn Off WEP

Avoid outdated protocols with known encryption weaknesses.

Turn Off WPS if Not Required

WPS allows alternative authentication methods such as an 8-digit PIN.

Change Default Administrative Credentials

Prevents attackers from gaining administrative control using publicly known default usernames and passwords.

Network Segmentation

Separate guest or untrusted devices from sensitive organisational resources.

Update Access Point Firmware

Apply security patches and fixes released by manufacturers.

04 - Bluetooth Security

Bluetooth enables wireless communication between devices through direct pairing.

Bluetooth operates at:

2.4 GHz

It is designed for short-range communication.

Common Bluetooth devices include:

Wireless keyboards
Wireless mice
Headphones
Speakers
Smartwatches
Fitness trackers
Vehicle infotainment systems
IoT and smart-home devices
Classic Bluetooth vs Bluetooth Low Energy

There are two main Bluetooth variants:

Classic Bluetooth
Bluetooth Low Energy (BLE)
Classic Bluetooth

Handles heavier tasks such as:

Audio streaming
File transfers
Bluetooth Low Energy

BLE is designed for devices that send small amounts of data occasionally.

Examples:

Fitness trackers
Smart locks
Beacons
Bluetooth Pairing

Classic Bluetooth uses:

Secure Simple Pairing (SSP)

SSP uses methods such as:

Numeric Comparison
Passkey Entry

BLE supports:

LE Legacy Pairing
LE Secure Connections

LE Legacy Pairing is cryptographically weak and vulnerable to passive eavesdropping.

LE Secure Connections is stronger and uses ECDH key exchange.

Bluetooth Security Differences
Aspect	Classic Bluetooth	BLE
Pairing	SSP with Numeric Comparison / Passkey	LE Legacy Pairing / LE Secure Connections
Advertising	Not continuously broadcast	Continuous advertising
Encryption	Varies depending on version	AES-CCM
Privacy	Fixed MAC historically	MAC randomisation
MITM protection	Better with SSP verification	"Just Works" provides no user verification
Attack Surface	Smaller	Larger, especially for always-on IoT devices
BLE Advertising

BLE devices can continuously broadcast advertising packets.

These can expose:

Device information
Service UUIDs
Sometimes unencrypted sensor data
Bluetooth Tracking

Classic Bluetooth traditionally uses fixed MAC addresses, making devices easier to track.

BLE supports MAC address randomisation to reduce long-term tracking.

"Just Works"

"Just Works" pairing is common in low-cost IoT devices.

It provides no user verification, leaving the connection open to Man-in-the-Middle attacks.

Bluetooth Security Risks
Unnecessary Discoverability

Discoverable devices announce themselves to nearby devices.

Weak Pairing

Older devices may use simple PIN-based pairing.

Unauthorised Pairing

Attackers may attempt to pair with devices when user approval controls are weak.

Bluejacking

Sending unsolicited messages to Bluetooth-enabled devices.

Bluesnarfing

Accessing data from a Bluetooth device without authorisation.

Bluebugging

Exploiting a Bluetooth vulnerability to gain control over certain device functions.

Outdated Devices

Older Bluetooth implementations may contain known vulnerabilities.

Bluetooth Security Recommendations
Disable Bluetooth when not in use
Avoid leaving devices discoverable
Use modern Bluetooth versions
Require user approval for pairing
Avoid pairing in public places
Remove unused paired devices
Keep devices updated
Monitor BLE advertising data
Avoid "Just Works"-only devices in sensitive environments
05 - RFID and NFC Security
RFID

Radio-Frequency Identification (RFID) uses electromagnetic fields to identify and track tags attached to objects.

RFID can transmit over significantly greater distances than NFC, depending on the tag type and frequency band.

NFC

Near-Field Communication (NFC) is a closely related wireless standard.

NFC operates at:

13.56 MHz

and normally works within approximately:

5 cm

NFC supports bidirectional communication.

How RFID Works

An RFID system consists of:

Reader
   ↓
RF Field
   ↓
Tag
   ↓
Stored Data

The reader emits radio waves.

When a tag enters the reader's field, it responds with stored data.

Passive RFID Tags
Have no internal power source
Draw energy from the reader's electromagnetic field
Have shorter range
Are inexpensive
Have a long lifespan
Active RFID Tags
Contain their own battery
Can transmit over greater distances
Are more expensive
Have a limited lifespan
How NFC Works

NFC uses the 13.56 MHz RFID frequency and supports two-way communication.

Common use cases include:

Contactless payments
Transit cards
Device pairing
Access control
Identification
Common RFID and NFC Uses
Employee badges
Warehouse inventory tags
Hotel key cards
Payment terminals
Access control
RFID and NFC Security Risks
Eavesdropping

Intercepting communication when an access card is being scanned.

Cloning

Copying data from one card to another.

Relay Attacks

Forwarding communication between a legitimate card and a reader to bypass normal distance limitations.

Unauthorised Scanning / Skimming

Secretly scanning a card without the owner's knowledge to steal data.

Lost or Stolen Cards

A lost employee badge could be used to enter a building if its access rights have not been revoked.

Relay Attack

A relay attack can involve two attacker-controlled devices:

Victim's Card
     ↓
Attacker Device 1
     ↓
   Relay
     ↓
Attacker Device 2
     ↓
Payment Terminal

The communication is forwarded in real time, making the terminal believe that the legitimate card is physically present.

RFID and NFC Security Measures
Use cards that support encryption
Limit sensitive data stored on cards
Use tokenisation
Immediately deactivate lost or stolen cards
Use protective sleeves such as Faraday pouches
Update access controls regularly
Implement secondary biometric authentication where possible
06 - Other Wireless Technologies

Modern environments and IoT systems use several wireless technologies in addition to Wi-Fi, Bluetooth, NFC and RFID.

Zigbee

Zigbee is:

Low power
Short range
Mesh based

It is commonly used in:

Smart lights
Sensors
Smart plugs

Each device can relay data to neighbouring devices, extending the overall range.

Zigbee Security Risk

When a device without a pre-configured key joins a Zigbee network, the coordinator may transmit the network encryption key protected only by a well-known default link key.

An attacker monitoring the pairing process can recover the network key and decrypt subsequent traffic.

The mesh topology can amplify the impact because a compromised device can relay malicious commands to other devices.

A Philips Hue smart bulb attack demonstrated how a compromised Zigbee device could be used to compromise the Hue bridge and gain access to the wider home network.

Security Measure

Use install codes for Zigbee device pairing.

This derives a unique link key for each device.

Z-Wave

Z-Wave is commonly used in home automation systems.

Examples include:

Thermostats
Blinds
Lights
Security sensors
S0

The original Z-Wave security framework, S0, encrypted the exchanged key using a static value of all zeroes.

This makes interception possible.

S2

The newer S2 framework uses Diffie-Hellman key exchange.

However, devices supporting both S0 and S2 can potentially be forced into a downgrade from S2 to S0 because the pairing handshake is unauthenticated.

This type of downgrade attack has been demonstrated against smart locks.

Security Measure

Turn off S0 backward compatibility on Z-Wave controllers.

If backward compatibility is required, require explicit user confirmation before accepting an S0 connection.

LoRa

LoRa (Long Range) is designed for:

Long-distance communication
Low-power operation
Small amounts of data

It is used in:

Environmental monitoring
Agricultural sensors
Smart street lighting

Devices can communicate over distances of several kilometres.

ABP

Activation by Personalisation (ABP) uses static session keys.

These keys remain unchanged unless manually rotated.

If the frame counter resets after an overflow or device reboot, an attacker who previously captured traffic may replay old messages within the accepted counter window.

Remote deployments can also be physically accessible for tampering and key extraction.

Security Measure

Prefer:

OTAA

Over-The-Air Activation

OTAA generates fresh session keys for each join.

Where ABP is unavoidable:

Rotate keys regularly
Monitor frame counters
Cellular IoT

Examples:

LTE-M
NB-IoT

These technologies allow devices to communicate over existing mobile networks.

Common uses:

Smart meters
Vehicle trackers
Remote industrial sensors

LTE-M and NB-IoT benefit from:

SIM-based authentication
Standardised encryption

However, devices are often deployed in remote locations, which can make physical tampering and firmware extraction possible.

Other risks include:

Difficult patching
Default credentials
Vulnerable gateway management interfaces
Injection flaws
Denial-of-service attacks
Data interception
Security Measures
Restrict cellular IoT gateway management interfaces
Change default credentials
Use a VPN or private APN where appropriate
Apply firmware updates
Infrared

Infrared uses light signals for:

Short-range communication
Line-of-sight communication

Common examples:

Television remotes
Air-conditioner remotes
Projectors
Infrared Security Risks

Infrared signals provide:

No authentication
No encryption

An attacker can capture and replay commands.

Protocols such as:

NEC
RC5

are publicly documented.

This means an attacker can construct valid commands without first capturing a signal.

Security Measure

Deactivate unused infrared receivers on network-connected devices.

Avoid placing infrared-responsive devices where they can be accessed from outside windows or doors.

IoT Network Segmentation

IoT devices should be placed on dedicated network segments.

This isolates wireless devices from systems that handle sensitive data and limits the impact of a compromised device.

IoT / Wireless Devices
          ↓
   Dedicated Network
          ↓
   Internal Systems
07 - Knowledge Test

The room contains a final knowledge test covering the wireless technologies and security concepts discussed throughout the room.

Questions and Answers
Question 1

A homeowner installs smart lights and motion sensors that communicate with a central hub using a low-power mesh network.

Answer:

Zigbee
Question 2

Between S0 and S2, which Z-Wave security framework is vulnerable to key interception due to its use of an all-zero encryption key?

Answer:

S0
08 - Conclusion

This room covered the fundamentals of wireless networking at a high level, including the different types of wireless technologies in wide use today.

It also covered the security risks associated with these technologies and measures that can be used to reduce their exposure to threats.

The foundational knowledge from this room prepares for rooms that explore wireless attack scenarios in greater depth.

Recommended Follow-Up Rooms
Wi-Fi Hacking 101
Intro to IoT Pentesting
Key Terms
Term	Definition
SSID	Service Set Identifier. The human-readable name of a Wi-Fi network.
BSSID	Basic Service Set Identifier. The MAC address of a wireless access point.
WEP	Wired Equivalent Privacy. The original Wi-Fi security protocol, now deprecated because of fundamental weaknesses in its RC4-based encryption.
WPA	Wi-Fi Protected Access. An intermediate security protocol introduced as a replacement for WEP, using TKIP for encryption.
WPA2	Wi-Fi Protected Access 2. A security protocol that uses AES encryption to protect Wi-Fi traffic.
WPA3	Wi-Fi Protected Access 3. The successor to WPA2, introducing SAE to resist offline dictionary attacks.
MITM	Man-in-the-Middle. An attack in which an adversary secretly intercepts and potentially alters communication between two parties.
SAE	Simultaneous Authentication of Equals. The key exchange mechanism used in WPA3.
BLE	Bluetooth Low Energy. A power-efficient variant of Bluetooth designed for IoT devices that transmit small amounts of data intermittently.
SSP	Secure Simple Pairing. A Bluetooth pairing mechanism introduced in version 2.1.
RFID	Radio-Frequency Identification. A technology that uses electromagnetic fields to identify and track tags attached to objects.
NFC	Near-Field Communication. A short-range wireless standard operating at 13.56 MHz that supports bidirectional communication within approximately 5 cm.
Zigbee	A low-power, short-range mesh networking protocol used in smart-home devices such as lights and sensors.
Z-Wave	A wireless protocol for home automation using a standardised frequency band and the S2 security framework for encrypted device communication.
LoRa	Long Range. A low-power wireless technology designed for transmitting small amounts of data over distances of several kilometres in IoT deployments.
Infrared	A wireless communication method using light signals for short-range, line-of-sight data transmission.
Final Takeaways

The room demonstrates that wireless security is broader than Wi-Fi.

The technologies covered include:

Wi-Fi
Bluetooth
BLE
RFID
NFC
Zigbee
Z-Wave
LoRa
Cellular IoT
Infrared

Each technology has its own:

Communication method
Frequency or transmission mechanism
Authentication model
Encryption model
Attack surface
Security considerations

The main security lesson is that wireless connectivity introduces additional exposure that must be understood and managed as part of a security assessment.