# Ports & Protocols Cheat Sheet
A complete reference for **network communication ports and protocols** used across modern systems, applications, and services.

## What Are Ports?
Ports act like numbered **doors** on a computer or network device.  
Each port identifies a specific process or service that handles network traffic.

- The **IP address** identifies *which device* to talk to.  
- The **port number** identifies *which application or service* on that device.

Example:  
`192.168.1.10:443` → HTTPS service on that host.

## Port Number Ranges

| Range | Type | Description |
|--------|------|-------------|
| **0-1023** | **Well-known ports** | Assigned by IANA for core protocols (HTTP, SSH, DNS, etc.) |
| **1024-49151** | **Registered ports** | Used by software vendors for applications (MySQL, Docker, etc.) |
| **49152-65535** | **Dynamic / Private ports** | Used temporarily for client connections (called *ephemeral ports*) |

> 💡 Example: When you open a web page, your browser uses a random *ephemeral port* (like `54732`) to connect to the server’s well-known port (`443`).

---

## Common TCP and UDP Protocols

| Port | Protocol | Transport | Description | Common Use |
|------|-----------|------------|--------------|-------------|
| **20** | FTP (Data) | TCP | Transfers file data between client and server | File transfer sessions |
| **21** | FTP (Control) | TCP | Manages FTP session commands | File management |
| **22** | SSH | TCP | Encrypted remote login and file transfer (SCP/SFTP) | Secure shell access |
| **23** | Telnet | TCP | Plain-text remote login (insecure, legacy) | Old network devices |
| **25** | SMTP | TCP | Sends email between servers | Outbound mail delivery |
| **53** | DNS | UDP/TCP | Resolves hostnames to IP addresses | Internet name resolution |
| **67-68** | DHCP | UDP | Assigns IP addresses to clients | Automatic IP configuration |
| **69** | TFTP | UDP | Lightweight file transfer (no authentication) | Firmware, PXE booting |
| **80** | HTTP | TCP | Unencrypted web traffic | Websites and APIs |
| **110** | POP3 | TCP | Downloads email from server | Legacy email clients |
| **123** | NTP | UDP | Synchronizes device clocks | Time sync for systems |
| **135** | RPC / EPM | TCP/UDP | Microsoft Remote Procedure Calls | Windows networking |
| **137-139** | NetBIOS | TCP/UDP | Windows file and printer sharing (SMB v1) | Legacy LAN communication |
| **143** | IMAP | TCP | Retrieves email, supports multiple folders | Modern mail clients |
| **161-162** | SNMP | UDP | Network device monitoring and management | Routers, switches, servers |
| **389** | LDAP | TCP/UDP | Directory lookups for users and devices | Active Directory queries |
| **443** | HTTPS | TCP | Secure web traffic (TLS/SSL) | Websites and APIs |
| **445** | SMB | TCP | Windows file sharing over TCP | File servers |
| **465** | SMTPS | TCP | Secure email sending (SSL/TLS) | Encrypted mail transfer |
| **514** | Syslog | UDP | Logs messages from network devices | Central log collection |
| **636** | LDAPS | TCP | Secure directory queries | Encrypted Active Directory |
| **853** | DNS over TLS | TCP | Encrypted DNS resolution | Secure DNS lookups |
| **993** | IMAPS | TCP | Secure email retrieval | Encrypted IMAP |
| **995** | POP3S | TCP | Secure POP3 | Encrypted email download |
| **1433** | MS SQL Server | TCP | Database service | Microsoft SQL connections |
| **1521** | Oracle DB | TCP | Oracle database listener | Oracle apps |
| **2049** | NFS | TCP/UDP | Network file system | Unix/Linux shares |
| **3306** | MySQL | TCP | Database connections | Web app databases |
| **3389** | RDP | TCP | Remote Desktop access | Windows remote management |
| **5432** | PostgreSQL | TCP | Database service | Web, analytics backends |
| **5900** | VNC | TCP | Remote desktop (cross-platform) | GUI remote control |
| **6379** | Redis | TCP | In-memory data store | Caching, messaging |
| **8080** | HTTP Alternate | TCP | Secondary HTTP service | Proxies, dev servers |
| **8443** | HTTPS Alternate | TCP | Secondary secure web service | Admin consoles |
| **9000-9999** | App ports | TCP | Common for developer tools | APIs, testing services |

## TCP vs UDP

| Feature | **TCP** | **UDP** |
|----------|----------|----------|
| **Full name** | Transmission Control Protocol | User Datagram Protocol |
| **Connection type** | Connection-oriented | Connectionless |
| **Reliability** | Guarantees delivery (ACKs) | No delivery guarantee |
| **Speed** | Slower (due to error checking) | Faster (low overhead) |
| **Use case** | File transfers, web traffic, email | Streaming, VoIP, DNS, gaming |

> 🧠 *Think of TCP as certified mail with a receipt, and UDP as a fast postcard - no confirmation, but quick and light.*

## Common Port Categories

| Category | Typical Ports | Example |
|-----------|----------------|----------|
| **Web Services** | 80 (HTTP), 443 (HTTPS), 8080, 8443 | Websites, APIs |
| **Email Services** | 25 (SMTP), 110/995 (POP3), 143/993 (IMAP) | Mail servers |
| **File Transfer** | 20–21 (FTP), 22 (SFTP), 69 (TFTP), 445 (SMB), 2049 (NFS) | Moving data |
| **Remote Access** | 22 (SSH), 23 (Telnet), 3389 (RDP), 5900 (VNC) | Admin control |
| **Database Access** | 1433 (MSSQL), 1521 (Oracle), 3306 (MySQL), 5432 (Postgres) | Backend services |
| **Network Management** | 161/162 (SNMP), 514 (Syslog), 123 (NTP) | Monitoring & sync |
| **Directory / Auth** | 389/636 (LDAP), 88 (Kerberos), 464 (kpasswd) | User identity |

## Troubleshooting Tips

| Tool | Purpose | Example |
|------|----------|----------|
| `ping` | Tests basic connectivity | `ping 8.8.8.8` |
| `tracert` / `traceroute` | Maps hops along a route | `tracert google.com` |
| `telnet <ip> <port>` | Tests if a port is open | `telnet 192.168.1.1 22` |
| `netstat -an` | Lists active connections | Check for listening ports |
| `nmap <ip>` | Scans for open ports | `nmap -p 1-1024 10.0.0.1` |
| `curl` | Tests web requests | `curl -v https://example.com` |

> 🔐 **Security Tip:** Unused open ports = attack surface. Always close or block unused services in firewalls or security groups.

## Memorization Helpers

- **Web:** `80/443` → Browsing  
- **Mail:** `25/110/143` (add 465/995/993 for secure)  
- **Remote:** `22 (SSH)`, `23 (Telnet)`, `3389 (RDP)`  
- **Files:** `20/21 (FTP)`, `445 (SMB)`, `69 (TFTP)`  
- **Databases:** `3306 (MySQL)`, `1433 (MSSQL)`, `5432 (Postgres)`  
- **DNS:** `53`, **DHCP:** `67/68`, **NTP:** `123`

> **Remember:**  
> Ports are the “addresses” of applications.  
> Protocols are the “languages” they use to talk.  
> Together, they make network communication possible — from local devices to global cloud systems.
