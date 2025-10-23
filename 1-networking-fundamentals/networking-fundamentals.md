([go-home](../README.md))

# Networking Fundamentals

## Introduction to Networking
Networking in today’s world is the foundation that holds our modern digital systems together. It’s what lets our phones, laptops, and wearable devices connect seamlessly - not just to the internet, but to each other and the environments around us. From Bluetooth headphones and smart watches to entire data centers, **networking is the discipline of connecting computers and devices into unified systems**. These systems let us communicate, share, and synchronize information faster and more reliably than ever before. As technology advances, networks become smaller, smarter, and more integrated - often invisible to the user. But behind that seamless experience lies engineering complexity: devices negotiating protocols, switching packets, maintaining state, and balancing traffic across millions of nodes.

> **A look to the future:** As computing becomes more advanced and distributed, the need for rock-solid networking fundamentals only grows. Systems must scale from a single device to entire global grids. The stronger your grasp of networking’s building blocks, the better you’ll adapt to - and help build - the next generation of connected technologies.

## What is Networking? 
Networking is how computers and systems exchange information. The concept is often compared to a **postal system**: data (the “letters”) are wrapped into **packets**, labeled with source and destination addresses, and passed through routers (“postal centers”) that forward them until they reach their destination.  

In modern systems, this exchange happens through different mediums:
- **Wired:** Ethernet, Fiber  
- **Wireless:** Wi-Fi, 4G, 5G, Bluetooth, Satellite  

Each network uses **signals** (electrical, optical, or radio) to encode and transmit data. These signals carry information such as:  
> “Send this email to user@gmail.com...”  
> “Load this website...”  
> “Play this video stream...”

At its core, networking is built on **protocols** - sets of agreed rules that ensure devices can “speak the same language.” Think of it like grammar for computers. Without shared standards, communication would be impossible.  

> **Why It Matters:** Understanding networking helps you think like an engineer rather than a user. You’ll know *why* things break, *where* to look, and *how* to fix them. It also gives you the insight to design systems that are faster, more secure, and more reliable.

Knowing how data moves across networks helps you:
- **Fix problems faster.** When something doesn’t connect, you’ll know where to start.  
- **Communicate better.** Terms like *IP*, *DNS*, and *ping* will have meaning.  
- **Build secure systems.** You’ll recognize weak points before they become threats.  
- **Understand the cloud.** Even the “cloud” runs on physical wires and routing tables.

## Core Network Components
Networking devices are specialized pieces of hardware or software designed to serve distinct roles. Just as a city relies on streets, intersections, and traffic lights, networks rely on these devices to manage data flow and connectivity.

| Component | Description |
|------------|-------------|
| **Router** | Directs traffic between networks using IP addressing. |
| **Switch** | Connects devices within a LAN and forwards frames based on MAC addresses. |
| **Hub** | Repeats signals to all connected devices (legacy, rarely used). |
| **Firewall** | Controls traffic based on defined security policies. |
| **Access Point** | Connects wireless devices to a wired network. |

> 💡 *Tip:* Routers operate at **Layer 3**, switches at **Layer 2**, and firewalls can span **Layers 3-7**.

## Topologies
A **network topology** defines how devices are physically or logically arranged. Each design offers trade-offs between reliability, scalability, and cost.

| Topology | Description |
|-----------|--------------|
| **Point-to-Point (P2P)** | Two devices connected directly - simplest form of communication. |
| **Star** | Devices connect to a central switch or hub. Easy to manage but depends on a single center node. |
| **Bus** | All devices share a single communication line - simple but prone to collisions. |
| **Mesh** | Every device connects to many others for maximum redundancy and reliability. |
| **Hybrid / Hub-and-Spoke** | Combines multiple topologies; common in enterprise and cloud networks. |

> As networks grow, topology choices impact performance, fault tolerance, and security segmentation. The architecture determines how data flows - and how resilient the network is to failure.

## OSI & TCP/IP Models
The **OSI (Open Systems Interconnection)** model helps visualize how data moves from an application down through hardware layers, across a network, and up to another device. Each layer has a specific role - and adds or removes headers as data flows. The OSI model maps closely to the modern **TCP/IP stack**, which merges some layers for practical use.

| # | Layer | Function | Example |
|--|--|--|--|
| 7 | Application | Interfaces with user applications | HTTP, FTP, DNS |
| 6 | Presentation | Translates and encrypts data | SSL/TLS |
| 5 | Session | Manages connections between hosts | NetBIOS, RPC |
| 4 | Transport | Handles data delivery | TCP, UDP |
| 3 | Network | Manages logical addressing | IP, ICMP |
| 2 | Data Link | Physical addressing and framing | Ethernet, VLAN |
| 1 | Physical | Actual transmission media | Cables, fiber, radio |

> 🧠 *Mnemonic:* “All People Seem To Need Data Processing.”  

When troubleshooting, start from the bottom:
- **Layer 1:** Is the cable connected or signal present?  
- **Layer 3:** Does the device have an IP address?  
- **Layer 7:** Is the application working?

## IP Addressing & Subnetting
Every device on a network needs a unique **IP address**, much like every home has a unique street address. This address identifies the sender and receiver of data packets and allows routers to move those packets across networks efficiently.

### IPv4 vs IPv6
There are two main versions of IP addresses in use today:

- **IPv4:** Uses a 32-bit format written as four numbers (e.g., `192.168.1.1`).  
  Each number ranges from 0 to 255, giving about 4.3 billion total addresses.
- **IPv6:** Uses a 128-bit format written in hexadecimal (e.g., `2001:0db8:85a3::8a2e:0370:7334`).  
  IPv6 was introduced because IPv4 addresses were running out. It provides virtually unlimited unique addresses and includes built-in security and auto-configuration.

> 💡 **Tip:** IPv4 and IPv6 can coexist. Many modern networks use both at the same time during the transition period.

Checkout: [IP Addressing Cheat Sheet](..\9-troubleshooting-and-tools\cheat-sheets\ip-addressing-cheat-sheet.md)

### Private and Public IP Ranges
IP addresses fall into two categories:

| Range | Type | Common Use |
|--------|------|-------------|
| `10.0.0.0 - 10.255.255.255` | Private | Large enterprise networks |
| `172.16.0.0 - 172.31.255.255` | Private | Virtual machines, testing, labs |
| `192.168.0.0 - 192.168.255.255` | Private | Home and small-office routers |
| Everything else | Public | Internet-facing services and websites |

Private IPs are used inside internal networks and are **not routable** on the public internet. Routers use **Network Address Translation (NAT)** to let many private devices share one public IP when they go online.

### Subnetting
**Subnetting** divides a larger network into smaller, more manageable sections called *subnets*. This helps improve performance, security, and scalability by limiting broadcast traffic and keeping groups of devices isolated.

| Example | CIDR | Total Addresses | Usable | Description |
|----------|------|----------------|---------|--------------|
| `192.168.1.0/24` | `/24` | 256 | 254 | Common home network |
| `192.168.1.0/25` | `/25` | 128 | 126 | Splits one network into two halves |
| `10.0.0.0/16` | `/16` | 65,536 | 65,534 | Large organization or campus |

> **Remember:** The smaller the `/` number, the larger the network. `/8` means millions of hosts; `/30` only supports two devices. Subnetting keeps traffic organized—like assigning departments in a building their own floors so everyone isn’t talking in the same hallway.

### CIDR Notation
**CIDR (Classless Inter-Domain Routing)** tells us how many bits of an IP address identify the network portion. For example, in `192.168.1.0/24`, the `/24` means the first 24 bits define the network, leaving 8 bits for hosts.

> **Analogy:** The *street name* represents the network, and the *house number* represents the host. CIDR simply tells us how long the “street name” part is.

## Subnets in Action
A **subnet**, short for “sub-network,” is just a smaller network inside a bigger one. It allows you to group devices logically—by department, location, or function.

**Example:**  
A school network (`192.168.1.0/24`) can be divided into:
- `192.168.1.0/25` → Teachers  
- `192.168.1.128/25` → Students  

| CIDR | Total IPs | Common Use |
|------|------------|-------------|
| /30 | 4 | Point-to-point links |
| /29 | 8 | Small offices |
| /24 | 256 | Standard local network |
| /16 | 65,536 | Large enterprise |

## DNS Basics
Humans use names; computers use numbers. **DNS (Domain Name System)** translates domain names like `www.google.com` into IP addresses that machines understand. Without DNS, every connection would require typing raw IPs - a nearly impossible task for humans.

When you type a website name:
1. Your computer sends a query to a **DNS resolver**.
2. The resolver checks cached records or contacts other DNS servers.
3. The server responds with the matching IP address.
4. Your browser connects to that address.

| Record | Purpose | Example |
|--------|----------|----------|
| **A** | IPv4 record | `example.com → 93.184.216.34` |
| **AAAA** | IPv6 record | `example.com → 2606:2800::1946` |
| **CNAME** | Alias for another name | `www.example.com → example.com` |
| **MX** | Mail exchange | `example.com → mail.example.com` |

## Routing
Routing is the process of moving data packets from one network to another along the best possible path. Physical routers analyze each packet’s destination IP and decide the next hop based on routing tables and metrics. This same principle extends beyond hardware - in modern software systems, application routers direct web requests (like URLs or API calls) to the right function or endpoint, applying the same logic of efficient and organized delivery.

> **Analogy:** Routers are like GPS navigation systems for data - they calculate the fastest route and redirect if there’s congestion or failure.

### Static Routing
- Routes are configured manually by an administrator.  
- Simple, predictable, and good for small environments.  
- Does **not** automatically adjust to network changes.

### Dynamic Routing
Routers automatically learn and share routes using **routing protocols**.  
This makes large networks adaptive and fault-tolerant.

Common examples:
- **RIP (Routing Information Protocol):** Simple, distance-based routing.  
- **OSPF (Open Shortest Path First):** Fast, link-state protocol used inside organizations.  
- **EIGRP (Enhanced Interior Gateway Routing Protocol):** Cisco-proprietary hybrid protocol.  
- **BGP (Border Gateway Protocol):** Core protocol of the internet; manages routing between different organizations.

### NAT (Network Address Translation)
**NAT** lets multiple private devices share a single public IP address.  
When a device sends traffic out, the router replaces its private IP with the public one, then keeps track of who sent what.

| Type | Description |
|------|--------------|
| **Static NAT** | One device ↔ One public IP |
| **Dynamic NAT** | Pool of public IPs shared among devices |
| **PAT (Port Address Translation)** | Many devices share one public IP (most common) |

> 💡 **Example:** Your home Wi-Fi network uses PAT - your laptop, phone, and TV all appear online as one IP.

## Common Ports & Protocols
Ports act like doors on a computer—each service listens on a specific number.  
Firewalls and routers use port numbers to allow or block specific traffic types.

| Port | Protocol | Purpose |
|------|-----------|----------|
| 20–21 | FTP | File transfers |
| 22 | SSH | Secure remote login |
| 25 | SMTP | Send email |
| 53 | DNS | Resolve domain names |
| 80 | HTTP | Unsecured web traffic |
| 443 | HTTPS | Secure web traffic |
| 3389 | RDP | Remote desktop |
| 161 | SNMP | Network monitoring |

Checkout: [Ports & Protocols Cheat Sheet](..\9-troubleshooting-and-tools\cheat-sheets\ports-and-protocols-cheat-sheet.md)

## Final Thoughts
Networking is everywhere - homes, schools, hospitals, satellites, and even wearables. Learning how it all works turns the “internet” from a mystery into a system you can understand, control, and build upon. Once you grasp these fundamentals - **addressing, routing, DNS, and OSI layers** - you can: (1) Design small networks confidently, (2) Troubleshoot issues methodically, (3) Communicate better with other engineers, (4) Understand how every cloud service ultimately relies on these same physical and logical layers.

## Next 
Continue: [Cloud Overview](..\2-cloud-overview\cloud-overview.md)









