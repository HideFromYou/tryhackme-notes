
**03-Wi-Fi-Security**:

```markdown
# Wi-Fi Security

## IEEE 802.11

Wi-Fi is based on the IEEE 802.11 family of standards.

The room covers the evolution of Wi-Fi standards and the security mechanisms used to protect wireless communication.

## Wi-Fi Generations

| Standard | Generation | Frequency | Key Characteristics |
|---|---|---|---|
| 802.11 | — | 2.4 GHz | Original Wi-Fi standard |
| 802.11b | — | 2.4 GHz | First widely adopted standard |
| 802.11g | — | 2.4 GHz | Higher speed and backward compatibility |
| 802.11n | Wi-Fi 4 | 2.4 / 5 GHz | Dual-band and MIMO |
| 802.11ac | Wi-Fi 5 | 5 GHz | Higher throughput and MU-MIMO |
| 802.11ax | Wi-Fi 6 / 6E | 2.4 / 5 / 6 GHz | High efficiency and OFDMA |
| 802.11be | Wi-Fi 7 | 2.4 / 5 / 6 GHz | Extremely High Throughput and Multi-Link Operation |

## Wi-Fi Security Protocols

### WEP

Wired Equivalent Privacy was the original Wi-Fi security protocol.

It is deprecated because of fundamental weaknesses in its RC4-based encryption that allow attackers to recover the network key.

### WPA

Wi-Fi Protected Access was introduced as an improvement over WEP.

It used TKIP and was later superseded by stronger standards.

### WPA2

WPA2 improved wireless security by using AES-based encryption.

It became the widely deployed successor to WPA and provides stronger protection for Wi-Fi traffic.

### WPA3

WPA3 is the successor to WPA2.

A key improvement is the use of **SAE (Simultaneous Authentication of Equals)**, which provides stronger protection against offline dictionary attacks.

## Important Security Concepts

### Encryption

Protects wireless traffic from being read by unauthorised parties.

### Authentication

Determines whether a device or user is allowed to connect to the wireless network.

### Pre-Shared Key

Used in WPA/WPA2-Personal networks to authenticate clients.

### SAE

Used by WPA3-Personal as a more resistant authentication and key-exchange mechanism.

## Wireless Threats

Wireless networks can be exposed to attacks involving:

- Weak encryption
- Weak passwords
- Authentication weaknesses
- Rogue access points
- Man-in-the-Middle attacks
- Eavesdropping
- Offline password attacks
- Protocol weaknesses

## Defensive Measures

- Use WPA2 or WPA3 instead of deprecated protocols
- Prefer WPA3 where supported
- Use strong wireless passwords
- Disable obsolete security mechanisms
- Monitor for rogue access points
- Keep wireless infrastructure updated
- Segment wireless networks appropriately

## Key Takeaway

Wireless security depends on both the security protocol and its configuration.

WEP should not be considered secure, WPA is legacy technology, WPA2 provides stronger AES-based protection, and WPA3 introduces SAE to improve resistance against password-based attacks.