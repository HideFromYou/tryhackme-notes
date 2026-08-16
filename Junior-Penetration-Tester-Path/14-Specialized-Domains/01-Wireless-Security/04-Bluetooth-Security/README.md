# Bluetooth Security

## Overview

Bluetooth is a short-range wireless technology operating on the **2.4 GHz** frequency band.

It is commonly used by:

- Wireless keyboards and mice
- Headphones and speakers
- Smartwatches
- Fitness trackers
- Vehicle infotainment systems
- IoT and smart-home devices

## Classic Bluetooth vs BLE

There are two main Bluetooth variants:

### Classic Bluetooth

Designed for heavier workloads such as:

- Audio streaming
- File transfers
- Continuous connections

Classic Bluetooth uses a pairing process where devices establish a shared key.

### Bluetooth Low Energy (BLE)

Designed for low-power devices that transmit small amounts of data intermittently.

Common examples include:

- Fitness trackers
- Smart locks
- Beacons
- IoT devices

## Pairing

Bluetooth devices must establish a relationship before communicating securely.

Pairing mechanisms can provide different levels of protection.

### Secure Simple Pairing (SSP)

Classic Bluetooth uses Secure Simple Pairing in modern implementations.

Pairing methods can include:

- Numeric comparison
- Passkey entry

These mechanisms can provide protection against Man-in-the-Middle attacks.

### BLE "Just Works"

BLE devices may use the **Just Works** pairing method.

This does not provide user verification during pairing and can therefore expose the connection to Man-in-the-Middle attacks.

## Bluetooth Security Risks

### Eavesdropping

An attacker may intercept wireless communication if security protections are insufficient.

### Man-in-the-Middle

An attacker positions themselves between two devices and attempts to intercept or manipulate the communication.

### Bluesnarfing

An attacker gains unauthorised access to data stored on a Bluetooth device, such as contacts or messages.

### Device Discovery

Bluetooth devices that remain discoverable can expose their presence to nearby attackers.

### BLE Advertising

BLE devices continuously transmit advertising packets that may expose:

- Device information
- Service UUIDs
- Potentially unencrypted sensor information

## Security Recommendations

- Disable Bluetooth when it is not required
- Avoid leaving devices permanently discoverable
- Use modern Bluetooth versions
- Require user approval for pairing
- Avoid pairing devices in public locations
- Remove unused paired devices
- Keep Bluetooth firmware updated
- Monitor BLE advertising data
- Avoid devices that rely only on "Just Works" pairing in sensitive environments

## Key Takeaway

Bluetooth's short range does not make it inherently secure.

A vulnerable Bluetooth device can expose sensitive information or provide an attacker with a foothold into a wider environment.