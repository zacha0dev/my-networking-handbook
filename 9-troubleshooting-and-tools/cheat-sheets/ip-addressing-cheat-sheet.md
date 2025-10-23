# IP Addressing Cheat Sheet
A quick reference for **IPv4 and IPv6** - structure, ranges, rules, and usage.  
Use this when configuring networks, troubleshooting connectivity, or preparing for certification.

## Overview

| Feature | IPv4 | IPv6 |
|----------|------|------|
| **Bit length** | 32 bits | 128 bits |
| **Format** | Dotted decimal (`192.168.1.10`) | Hexadecimal (`2001:0db8::1`) |
| **Total addresses** | ≈ 4.3 billion | ≈ 3.4 × 10³⁸ (virtually unlimited) |
| **Address example** | `192.168.0.10` | `2001:0db8:85a3::8a2e:0370:7334` |
| **Notation** | `x.x.x.x` (4 octets) | 8 groups of 16-bit hex, separated by `:` |
| **Introduced** | 1981 | 1999 |
| **Used for** | Most networks today | Modern, expanding deployments |
| **Configuration** | Manual / DHCP | Stateless (SLAAC) or DHCPv6 |
| **Security** | Add-on (IPSec optional) | IPSec built-in |
| **Header size** | 20 bytes | 40 bytes |

## IPv4 Fundamentals

### Address Structure
- 4 octets = 32 bits  
- Each octet = 8 bits = values 0–255  
- Written in dotted-decimal notation

Example:  
`11000000.10101000.00000001.00001010` → **192.168.1.10**

### Legacy Address Classes
| Class | Range | Default Mask | Max Hosts | Typical Use |
|--------|--------|--------------|------------|--------------|
| A | 1.0.0.0 - 126.255.255.255 | 255.0.0.0 (/8) | ~16 million | Very large orgs |
| B | 128.0.0.0 - 191.255.255.255 | 255.255.0.0 (/16) | ~65 k | Medium networks |
| C | 192.0.0.0 - 223.255.255.255 | 255.255.255.0 (/24) | 254 | Small networks |
| D | 224.0.0.0 - 239.255.255.255 | N/A | N/A | Multicast |
| E | 240.0.0.0 - 255.255.255.255 | N/A | N/A | Research / Experimental |

> 💡 Modern networks use **CIDR** (Classless Inter-Domain Routing) instead of fixed classes.

### Private vs Public IPv4 Ranges
| Range | Type | Notes |
|--------|------|-------|
| 10.0.0.0 - 10.255.255.255 | Private | Large enterprises |
| 172.16.0.0 - 172.31.255.255 | Private | Labs, VMs |
| 192.168.0.0 - 192.168.255.255 | Private | Homes & SOHO |
| Others | Public | Routable on internet |

Routers use **NAT (Network Address Translation)** so multiple private devices can share one public IP.

### CIDR & Subnetting Quick Reference
| CIDR | Mask | Total IPs | Usable Hosts |
|------|------|-----------|--------------|
| /30 | 255.255.255.252 | 4 | 2 |
| /29 | 255.255.255.248 | 8 | 6 |
| /28 | 255.255.255.240 | 16 | 14 |
| /27 | 255.255.255.224 | 32 | 30 |
| /26 | 255.255.255.192 | 64 | 62 |
| /25 | 255.255.255.128 | 128 | 126 |
| /24 | 255.255.255.0 | 256 | 254 |
| /16 | 255.255.0.0 | 65 536 | 65 534 |
| /8 | 255.0.0.0 | 16 777 216 | 16 777 214 |

## IPv6 Fundamentals

### Structure
- 128 bits total → 8 groups × 16 bits  
- Written in **hexadecimal** with colons:  
  `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Leading zeros and consecutive groups of zeros can be **compressed**:
  - `2001:0db8:0000:0000:0000:ff00:0042:8329`
  - → `2001:db8::ff00:42:8329`

### Address Types
| Type | Prefix | Purpose |
|-------|--------|----------|
| **Unicast** | (various) | One-to-one communication |
| **Multicast** | ff00::/8 | One-to-many |
| **Anycast** | (assigned) | One-to-nearest node |
| **Link-local** | fe80::/10 | Auto-assigned within a single network segment |
| **Unique Local (ULA)** | fc00::/7 | Similar to private IPv4; not globally routable |
| **Global Unicast** | 2000::/3 | Publicly routable IPv6 internet space |

### Special IPv6 Addresses
| Address | Function |
|----------|-----------|
| `::1` | Loopback (like 127.0.0.1 in IPv4) |
| `::` | Unspecified (no address assigned) |
| `fe80::/10` | Link-local autoconfig range |
| `ff00::/8` | Multicast range |
| `fc00::/7` | Unique Local (private) |
| `2000::/3` | Global Unicast (internet) |

### Prefix Lengths (IPv6 Subnets)
CIDR notation still applies - `/64` is the **standard subnet size** for most networks.

| Prefix | # of Addresses | Common Use |
|---------|----------------|-------------|
| /128 | 1 | Single host |
| /64 | 18 quintillion | Standard LAN/WAN segment |
| /48 | 65 k × /64 subnets | Enterprise site |
| /32 | ISP allocation | Large provider range |

### Stateless Auto-Configuration (SLAAC)
IPv6 hosts can generate their own addresses:
1. Listen for **Router Advertisements (RA)**.  
2. Combine advertised prefix + interface ID.  
3. Verify uniqueness via **Duplicate Address Detection (DAD)**.

This means IPv6 networks often require **no DHCP** at all.

### Dual Stack & Tunneling
Because IPv4 still dominates, most systems run **dual stack** (both v4 and v6 enabled).  
When IPv6 isn’t available end-to-end, tunneling methods (like **6to4** or **Teredo**) wrap IPv6 packets inside IPv4 for transport.

### Quick Comparison Summary
| Feature | IPv4 | IPv6 |
|----------|------|------|
| Address length | 32 bits | 128 bits |
| Written in | Decimal | Hexadecimal |
| Broadcast | Yes | No (replaced by multicast) |
| NAT | Common | Rarely needed |
| Auto-config | DHCP, manual | SLAAC, DHCPv6 |
| Fragmentation | Routers + hosts | Hosts only |
| Header | Variable | Fixed |
| IPSec | Optional | Mandatory support |

## Useful Commands

| Platform | Command | Purpose |
|-----------|----------|----------|
| Windows | `ipconfig /all` | View IPs & adapters |
| Linux / macOS | `ifconfig` or `ip addr show` | Display addresses |
| All | `ping 8.8.8.8` / `ping -6 google.com` | Test IPv4 / IPv6 connectivity |
| All | `tracert` / `traceroute` | Show path packets take |
| All | `nslookup example.com` | DNS resolution |
| All | `netstat -an` | View open connections & ports |

> **Tip:** Mastering IPv4 and IPv6 together lets you design, secure, and troubleshoot any modern network—from home labs to global enterprise systems.
