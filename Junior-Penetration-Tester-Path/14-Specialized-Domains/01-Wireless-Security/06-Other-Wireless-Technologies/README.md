# Other Wireless Technologies

## Overview

Beyond Wi-Fi, Bluetooth, NFC and RFID, many other wireless technologies are used in IoT, smart-home and connected infrastructure environments.

## Zigbee

Zigbee is a low-power, short-range wireless protocol commonly used for:

- Smart lights
- Sensors
- Smart plugs

It uses a **mesh topology**, allowing devices to relay traffic to neighbouring devices.

### Security Risk

During device joining, a network key may be transmitted protected by a well-known default link key.

An attacker monitoring the pairing process may recover the network key.

A compromised device can also relay malicious commands through the mesh.

### Security Measure

Use install codes for Zigbee pairing so each device receives a unique link key.

## Z-Wave

Z-Wave is used in home automation systems such as:

- Thermostats
- Blinds
- Lights
- Security sensors

### S0

The older S0 security framework used a static all-zero value to protect the exchanged encryption key, making interception possible.

### S2

S2 introduced stronger protection using Diffie-Hellman key exchange.

However, devices supporting both S0 and S2 may be vulnerable to downgrade attacks if S0 compatibility remains enabled.

### Security Measure

Disable S0 backward compatibility where possible.

## LoRa

**LoRa (Long Range)** provides low-power, long-distance communication.

It is commonly used for:

- Environmental monitoring
- Agricultural sensors
- Smart street lighting
- IoT deployments

### Security Risks

ABP (Activation by Personalisation) can use static session keys.

Replay attacks may also become possible if frame counters reset or are mishandled.

### Security Measure

Prefer OTAA (Over-The-Air Activation), which generates fresh session keys for each join.

## Cellular IoT

Technologies such as:

- LTE-M
- NB-IoT

allow IoT devices to communicate through cellular networks.

Examples include:

- Smart meters
- Vehicle trackers
- Remote industrial sensors

### Security Risks

- Physical tampering
- Firmware extraction
- Difficult patching
- Default credentials
- Vulnerable management interfaces

### Security Measures

- Change default credentials
- Restrict management interfaces
- Use VPNs or private APNs where appropriate
- Apply firmware updates

## Infrared

Infrared uses light signals for short-range, line-of-sight communication.

Common examples:

- Television remotes
- Air-conditioner remotes
- Projectors

### Security Risks

Infrared communication may lack authentication and encryption.

An attacker can capture and replay commands or construct commands using publicly documented protocols.

### Security Measure

Disable unused infrared receivers on network-connected devices where possible.

## IoT Network Segmentation

Wireless IoT devices should be placed on dedicated network segments.

Segmentation limits the impact of a compromised wireless device and prevents direct access to sensitive systems.

## Key Takeaway

Wireless technologies beyond Wi-Fi and Bluetooth introduce their own attack surfaces.

Security testing should consider:

- Pairing mechanisms
- Key management
- Authentication
- Replay protection
- Firmware security
- Physical access
- Network segmentation