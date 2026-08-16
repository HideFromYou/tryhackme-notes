# RFID and NFC Security

## RFID

**Radio-Frequency Identification (RFID)** uses electromagnetic fields to identify and track tags.

An RFID system consists of:

- Reader / interrogator
- RFID tag

### Passive RFID

A passive tag has no internal power source.

It receives energy from the reader's electromagnetic field and responds with stored data.

Advantages:

- Low cost
- Long lifespan

Disadvantage:

- Limited range

### Active RFID

An active tag contains its own battery.

This allows greater communication range but increases cost and limits the lifespan of the device.

## NFC

**Near-Field Communication (NFC)** is a short-range wireless technology operating at **13.56 MHz**.

NFC generally operates within approximately **5 cm** and supports bidirectional communication.

Common uses include:

- Contactless payments
- Transit cards
- Device pairing
- Access control

## RFID vs NFC

| Technology | Typical Range | Main Uses |
|---|---|---|
| RFID | Can reach much greater distances depending on implementation | Identification, tracking, access control |
| NFC | Approximately 5 cm | Payments, transit, pairing |

## Security Risks

### Eavesdropping

An attacker intercepts communication when a card is scanned.

### Cloning

Data from a legitimate card is copied onto another card.

### Relay Attack

Communication between a legitimate card and reader is forwarded through attacker-controlled devices.

This can bypass the normal physical distance limitation.

### Unauthorised Scanning / Skimming

An attacker secretly scans a card without the owner's knowledge.

### Lost or Stolen Cards

A lost access card may still provide access if its permissions have not been revoked.

## Security Measures

- Use cards supporting encryption
- Limit sensitive data stored on cards
- Use tokenisation where appropriate
- Immediately deactivate lost or stolen cards
- Use protective sleeves such as Faraday pouches where appropriate
- Regularly update access controls
- Use secondary biometric authentication where possible

## Key Takeaway

RFID and NFC provide convenient wireless identification and transactions, but their physical accessibility creates risks involving interception, cloning, relay attacks and unauthorised scanning.