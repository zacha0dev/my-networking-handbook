([go-home](../README.md))

# Networking Fundamentals 

# 🌐 Networking Fundamentals

Goal: Learn the basic ideas that make computers talk to each other, and have a quick place to look things up when you forget.

---

## 🧭 What Is Networking?

Networking is the invisible glue that holds our digital world together.  
It’s how your phone connects to a friend’s device, how your laptop reaches the internet, and how companies share data across the globe.  
Every photo upload, online game, or video call you make depends on a chain of connected machines passing messages back and forth.

You can think of a network like a **postal system for data**:
- **IP addresses** are like house numbers that identify each device.
- **Routers** are the mail sorters that decide where to send information next.
- **Packets** are the envelopes carrying small pieces of your data.
- And the **internet** is the collection of all these postal routes combined.

Whenever your device connects to Wi-Fi, joins a cellular tower, or uses Bluetooth, it becomes part of a network — and every network needs a set of rules to make communication clear and reliable. Those rules are called **protocols**, and the most common one for the internet is **TCP/IP**.

---

## 💡 Why It Matters

Understanding networking might seem technical, but it’s actually one of the most practical tech skills you can learn.  
Knowing how data moves across the internet helps you:
- **Fix problems faster.** When something doesn’t connect, you’ll know where to look first.
- **Communicate better with tech teams.** Terms like *IP*, *DNS*, and *ping* will make sense.
- **Build safer systems.** You’ll recognize weak spots that hackers might exploit.
- **Understand the cloud.** Every cloud app still relies on physical networks underneath.

In short, if you understand how one computer talks to another, you can understand almost any modern technology — from smart homes to AI servers.

---

## 🧱 IP Addressing

Every device on a network needs an **address** so others can find it.  
Without one, your laptop wouldn’t know where to send or receive information.  
These addresses are called **IP addresses**, and they come in two main versions.

### IPv4 vs IPv6

| Type | Looks Like | Notes |
|------|-------------|-------|
| IPv4 | `192.168.1.10` | Most common, uses 32 bits |
| IPv6 | `2001:0db8::1` | Newer, uses 128 bits (almost unlimited) |

IPv4 has been around since the early days of the internet. It uses four numbers separated by dots, giving about 4.3 billion possible addresses — which seemed like plenty in the 1980s but is nowhere near enough today.  
That’s why IPv6 was introduced: it provides a *massive* number of possible addresses and is built to handle the future of billions of connected devices.

---

### CIDR Notation

CIDR, or **Classless Inter-Domain Routing**, is a way of writing how big or small a network is.  
It looks like this: `192.168.1.0/24`.  
The `/24` means “the first 24 bits are for the network.”  
That leaves 8 bits for devices, which equals 254 usable addresses.

If that sounds confusing, picture a neighborhood:
- The **street name** (network) stays the same for all houses.
- The **house number** (host) changes for each home.

CIDR simply says how long the “street name” part is.

---

### Private vs Public IPs

Some IP addresses are **private**, meaning they only work inside your local network.  
Others are **public**, which means they can be reached over the internet.

| Range | Type | Example Use |
|-------|------|--------------|
| 10.0.0.0 – 10.255.255.255 | Private | Large companies |
| 172.16.0.0 – 172.31.255.255 | Private | Mid-sized networks |
| 192.168.0.0 – 192.168.255.255 | Private | Homes and small offices |
| Others | Public | Websites and cloud servers |

Private IPs keep home and company devices hidden from the outside world.  
Routers act like doormen — they know who’s allowed in or out.

---

## 🧩 Subnets

A **subnet**, short for “sub-network,” slices a larger network into smaller groups.  
This helps reduce congestion and keeps devices organized.  
For example, a school might give teachers one subnet and students another to keep their traffic separate.

**Example:**  
`192.168.1.0/24` (one large network)  
can be split into:  
- `192.168.1.0/25` → for teachers  
- `192.168.1.128/25` → for students  

| CIDR | Total IPs | Common Use |
|------|------------|-------------|
| /30 | 4 | Point-to-point links |
| /29 | 8 | Small offices |
| /24 | 256 | Standard local network |
| /16 | 65,536 | Big organizations |

Subnets are a bit like apartment floors — you can manage each one separately but they all share the same building (the larger network).

---

## 🌍 DNS Basics

Typing `www.google.com` is easy. Typing `142.250.191.142` is not.  
That’s why we have **DNS**, or the **Domain Name System** — it’s like the phone book of the internet.

When you enter a website name:
1. Your computer asks a **DNS server** what IP address belongs to that name.
2. The DNS server replies with the answer.
3. Your browser connects to that address and loads the page.

| Record | What It Does | Example |
|--------|---------------|----------|
| A | IPv4 address | `example.com → 93.184.216.34` |
| AAAA | IPv6 address | `example.com → 2606:2800::1946` |
| CNAME | Alias for another name | `www.example.com → example.com` |
| MX | Tells email where to go | `example.com → mail.example.com` |

Without DNS, you’d have to memorize every site’s number — which would make the internet impossible to use.

---

## 🚦 Routing

Routing is how data finds its way from one network to another.  
When you send an email, your message might pass through ten or more routers before reaching its destination — each one deciding the best next step.

Think of routers like air-traffic controllers, directing packets along the safest, fastest route.

### Static Routing
In static routing, routes are entered manually.  
It’s simple but only practical for small setups.

✅ Easy to control  
❌ Doesn’t adapt when networks change

### Dynamic Routing
Dynamic routing uses protocols — special languages routers speak — to learn paths automatically.

Common examples:
- **OSPF (Open Shortest Path First):** used within organizations  
- **BGP (Border Gateway Protocol):** used between organizations and across the internet

These protocols help keep global traffic flowing even when some routes fail or slow down.

---

### NAT (Network Address Translation)

**NAT** is what lets multiple devices share a single public IP address.  
Your home router uses NAT every time you connect your phone, laptop, or game console to Wi-Fi.

| Type | Description |
|------|--------------|
| Static NAT | One device ↔ One public IP |
| Dynamic NAT | Pool of public IPs shared between devices |
| PAT (Port Address Translation) | Many devices share one public IP (most common) |

NAT works like a receptionist: it keeps track of who made which request so when the response comes back, it goes to the right device.

---

## ⚙️ The OSI Model

Networking follows a layered design called the **OSI Model (Open Systems Interconnection)**.  
Each layer has a different job, from physical cables to the apps we see on screen.

| Layer | Name | What It Does | Example |
|-------|------|---------------|----------|
| 7 | Application | What the user interacts with | Web browser, email app |
| 6 | Presentation | Formats or encrypts data | SSL/TLS |
| 5 | Session | Manages conversations | Keeps login sessions active |
| 4 | Transport | Moves data reliably | TCP, UDP |
| 3 | Network | Finds the path to destination | IP, ICMP |
| 2 | Data Link | Moves data between devices | Ethernet, Wi-Fi |
| 1 | Physical | Hardware that sends signals | Cables, fiber, radio |

Understanding these layers helps troubleshoot.  
If a website won’t load, ask yourself:  
“Is the cable connected?” (Layer 1)  
“Does Wi-Fi have an IP?” (Layer 2–3)  
“Is the site responding?” (Layer 7)

---

## 🧰 Common Ports

Ports act like doors on a computer.  
Each type of service uses its own port number so traffic knows where to go.

| Port | Purpose |
|------|----------|
| 80 | HTTP – normal web traffic |
| 443 | HTTPS – secure web traffic |
| 22 | SSH – secure remote login |
| 3389 | RDP – remote desktop |
| 53 | DNS – name lookups |
| 25 | SMTP – email sending |
| 161 | SNMP – device monitoring |

Firewalls open or close these “doors” to control what’s allowed through.

---

## 📚 Final Thoughts

Networking is everywhere — in homes, schools, hospitals, cars, even smart watches.  
Learning the fundamentals gives you a superpower: you stop seeing the internet as “magic” and start seeing it as a set of systems working together.  

Once you understand IPs, DNS, and routing, you can:
- Set up your own small network.
- Troubleshoot slow Wi-Fi or connection errors.
- Understand how cloud apps communicate behind the scenes.

The next time your internet cuts out, you’ll know whether to check the cable, the router, or the DNS — not just reboot everything and hope for the best.

---

## 📎 Resources to Add Later
- [ ] Diagram: “How data travels across the internet”  
- [ ] Subnet and CIDR cheat sheet  
- [ ] DNS resolution visual  
- [ ] Practice quiz: match each OSI layer to an example  
- [ ] Real-world case: how your home Wi-Fi connects to the cloud  

---

_Last updated: {{ insert date }}_