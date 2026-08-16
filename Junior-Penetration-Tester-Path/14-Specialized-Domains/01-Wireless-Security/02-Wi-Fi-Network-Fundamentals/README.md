# Wi-Fi Network Fundamentals

## Wi-Fi Network Components

A Wi-Fi network consists primarily of:

### Access Point (AP)

The device broadcasting the wireless signal and providing connectivity between wireless clients and the underlying network.

### Clients

Devices connecting to an access point, such as:

- Phones
- Laptops
- Tablets
- Printers
- Smart devices

Clients use a wireless Network Interface Card (NIC) to transmit and receive radio signals.

## Wi-Fi Identifiers

### SSID

**Service Set Identifier**

The human-readable name of a wireless network.

Example:

```text
Office_WiFi
BSSID

Basic Service Set Identifier

The unique identifier of an access point, normally represented by the MAC address of its wireless interface.

Example:

00:1A:2B:3C:4D:5E
Wi-Fi Frequency Bands
2.4 GHz

Advantages:

Greater range
Better penetration through walls and floors

Disadvantages:

More congestion
Interference from Bluetooth, microwaves and other devices
Lower maximum speeds compared with 5 GHz
5 GHz

Advantages:

Higher speeds
Less congestion

Disadvantages:

Shorter range
More affected by physical obstacles
Wi-Fi Association Process

When a device connects to a wireless network, the general process involves:

Scanning for available networks
Selecting a network
Authentication and association
Negotiating encryption keys
Beginning data transmission

The exact order can vary depending on the security protocol.

WPA2-Personal

The device uses the four-way handshake to prove knowledge of the pre-shared key.

WPA2-Enterprise

The device associates with the access point and authentication is handled through an authentication server such as RADIUS using 802.1X.

Factors Affecting Wi-Fi Coverage
Physical Barriers

Walls, floors and ceilings can weaken signals. Concrete and metal can have a particularly significant effect.

Distance

Signal strength decreases as the client moves further from the access point.

Interference

Other devices operating on similar frequencies can disrupt wireless communication.

Examples include:

Bluetooth
Microwaves
Other Wi-Fi networks
Channel Congestion

Multiple networks operating on overlapping channels can compete for the same wireless spectrum.

Signal Leakage

Wireless signals may extend outside the intended physical boundaries of an organisation, potentially exposing the network to attackers in nearby areas.

Key Takeaway

Understanding Wi-Fi fundamentals is essential before performing wireless security testing.

Important concepts include:

AP
Client
SSID
BSSID
2.4 GHz
5 GHz
Association
Authentication
Encryption
Interference
Channel congestion
Signal leakage