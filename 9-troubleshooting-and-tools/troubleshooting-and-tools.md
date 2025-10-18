([go-home](../README.md))

#### Page Contents

- [Troubleshooting Mindset](#troubleshooting-mindset)
- [Simple Troubleshooting Framework](#simple-troubleshooting-framework)
- [OSI Model Quick Reference](#osi-model-quick-reference)
- [Understanding Latency, Bandwidth & Throughput](#understanding-latency-bandwidth--throughput)
- [Tools Reference Library](#tools-reference-library)

</br>
</br>

# Troubleshooting & Tools 
A quick reference guide for diagnosing issues across networks, applications, and services, along with commonly used tools in modern environments.

</br>

## Troubleshooting Mindset 
When troubleshooting, the goal is to solve an error, restore a service, or determine root cause with simplicity and speed. </br>
The **goal** should be: Observe → Isolate → Test → Verify → Resolve → Document.

## Simple Troubleshooting Framework 
1. **Identify the Problem** - Start with the symptom, not the assumption; clarify what’s broken, when it last worked, and what changed.
2. **Define Scope** - Determine if the issue is local or global, and identify the affected layer (network, system, app, identity, or cloud).
3. **Reproduce the Issue** - Confirm the problem is consistent and repeatable using simple validation commands (ping, curl, traceroute).
4. **Isolate the Fault** - Eliminate components layer by layer until you find the boundary where normal operation stops.
5. **Form and Test Hypothesis** - Change one variable at a time, validate results, and confirm whether the action affects the outcome.
6. **Implement Resolution** - Apply the smallest effective fix, verify recovery, and monitor for stability.
7. **Document Findings** - Capture root cause, resolution, and lessons learned to prevent future recurrence.

</br>

## OSI Model Quick Reference
The OSI model helps you visualize where communication might break down. Each layer handles a different part of how systems talk - from physical signals to the applications users interact with. When tracing an issue, think layer by layer to pinpoint whether the fault is in the wire, a network device, or the software stack.

| Layer | Name | Description | Common Protocols / Examples |
|:------|:------|:-------------|:-----------------------------|
| **7** | **Application** | User-facing layer where services run and data is displayed. | HTTP, HTTPS, DNS, FTP, SMTP, SSH |
| **6** | **Presentation** | Translates and secures data (encryption, compression, encoding). | SSL/TLS, JSON, XML, JPEG |
| **5** | **Session** | Manages communication sessions between systems. | RPC, NetBIOS, SQL Session |
| **4** | **Transport** | Controls reliable delivery and ports for communication. | TCP, UDP |
| **3** | **Network** | Handles IP addressing, routing, and logical paths. | IP, ICMP, IPSec |
| **2** | **Data Link** | Moves data between devices on the same network segment. | Ethernet, ARP, VLAN, PPP |
| **1** | **Physical** | Transmits raw bits over cables, fiber, or wireless. | Cables, NICs, Hubs, Wi-Fi |

### Memory Tip
> **Please Do Not Throw Sausage Pizza Away**  
> _(Physical → Data Link → Network → Transport → Session → Presentation → Application)_

</br>

## Understanding Latency, Bandwidth & Throughput
| Concept | Meaning | Example |
|----------|----------|----------|
| **Latency** | Time it takes for one packet to reach destination (delay). | Measured in milliseconds (ms). |
| **Bandwidth** | Maximum data capacity of a connection path. | Like the width of a highway lane. |
| **Throughput** | Actual data rate achieved in real time. | Affected by congestion, loss, or TCP windowing. |
| **Jitter** | Variation in packet delay between transmissions. | Can cause call or video quality issues. |
| **Packet Loss** | Dropped packets during transmission. | Leads to retransmissions and slowdowns. |

**Tip:** Always test **latency**, **throughput**, and **packet loss** before assuming where a slowdown originates.

### Quick Diagnostic Flow
> **Symptom → Scope → Reproduce → Isolate → Test → Resolve → Verify → Document**

</br>

## Tools Reference Library
A growing list of practical tools, commands, and utilities used across real troubleshooting workflows - from networking to coding and automation.  
Each entry links to its own focused page for syntax, examples, and quick testing commands.

### Cloud & Development Tools
| Tool | Type | Use For |
|------|------|---------|
| **AzCopy** | Cloud / Storage | High-performance CLI for copying data to and from Azure Storage. Ideal for large data migrations. |
| **Azure CLI** | Cloud | Manage Azure resources and services from any shell using `az` commands. Ideal for scripting, IaC validation, and diagnostics. |
| **Azure Network Watcher** | Cloud / Networking | Monitor, capture, and analyze traffic flows, NSGs, and connectivity between Azure resources. |
| **Azure PowerShell** | Cloud / Automation | PowerShell `Az` module for managing Azure via cmdlets and scripts. Great for hybrid Windows + cloud workflows. |
| **Azure Storage Explorer** | Cloud GUI | Visual management tool for Azure Blob, Queue, and Table storage — inspect data, upload/download blobs, and debug access. |
| **Bicep CLI** | IaC (Azure Native) | Deploy Azure resources with a clean, declarative syntax instead of raw ARM templates. |
| **Git** | Source Control | Distributed version control for managing repositories, branches, and commits locally or remotely. |
| **Git Credential Manager (GCM)** | Auth Utility | Handles HTTPS credential caching for Git and GitHub CLI. Required for seamless push/pull operations. |
| **GitHub CLI (`gh`)** | DevOps / Collaboration | Manage GitHub repos, pull requests, and issues directly from terminal — integrates with CI/CD flows. |
| **Microsoft Graph CLI** | Cloud / API | Command-line access to Microsoft 365 and Azure AD APIs for automation and integration scripting. |
| **Python** | Scripting / Automation | Automate data collection, build CLI tools, and integrate APIs (used across your GreenPlate & Infinite Two environments). |
| **Terraform** | IaC (Infrastructure-as-Code) | Build, modify, and version infrastructure predictably using declarative `.tf` files. |
| **Visual Studio Code (VS Code)** | Editor / Dev | Core IDE for coding, debugging, and integrated terminal work across all project stacks. |

</br>

### Networking, Security & Troubleshooting Tools
| Tool | Type | Use For |
|------|------|---------|
| **Command Prompt (CMD)** | Shell | Native Windows terminal for quick commands and legacy diagnostics (`ipconfig`, `netstat`, `tracert`). |
| **Curl** | Web / API | Test HTTP/HTTPS endpoints, APIs, and service health. Useful for backend verification and authentication checks. |
| **Fiddler / Microsoft Network Monitor** | Web Proxy / Capture | Inspect HTTP(S) traffic between client and server for debugging APIs or auth flows. |
| **iPerf / PsPing Bandwidth Mode** | Performance | Measure network throughput and bandwidth across endpoints. Useful for VPN and latency testing. |
| **jq** | CLI Parser | Lightweight JSON processor for filtering and transforming CLI/API output (pairs well with `az` and `curl`). |
| **Nmap** | Security / Network Discovery | Scan networks and ports to identify reachable hosts and exposed services. |
| **NSLookup / Dig** | DNS | Query DNS records, verify name resolution, and troubleshoot domain or endpoint issues. |
| **Ping** | Network | Basic connectivity test to check if a host or IP is reachable and measure latency (ICMP). |
| **PowerShell** | Shell / Automation | Cross-platform shell for Windows, Linux, and macOS — automate, query APIs, and manage system state. |
| **PsPing** | Network | Sysinternals network test tool — measures latency, bandwidth, and port reachability for TCP/UDP. |
| **SSH / OpenSSH** | Connectivity | Securely connect to remote servers or Raspberry Pi devices for configuration and tunneling. |
| **Sysinternals Suite** | Windows Utilities | Deep Windows diagnostics (Process Explorer, TCPView, PsPing, Autoruns). |
| **Tcpdump** | Packet Capture (CLI) | CLI packet sniffer for quick network capture and analysis (Linux/macOS). |
| **Tracert / Traceroute** | Network | Maps hop-by-hop path between systems to identify where connectivity fails. |
| **Wireshark** | Packet Analysis | Capture and analyze packets in real time for deep troubleshooting and network forensics. |

</br>
</br>

_Last updated: October 18th, 2025_