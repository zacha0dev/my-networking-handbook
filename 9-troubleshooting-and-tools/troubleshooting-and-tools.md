([go-home](../README.md))

# 🧰 Troubleshooting & Tools

Goal: Build a strong, repeatable mindset for troubleshooting networks, apps, and services — with a focus on **Azure-based systems** and **common real-world tools** that every engineer should know.  
This section serves as a quick reference you can return to daily at work or during labs.

---

## 🧭 The Mindset

Troubleshooting isn’t guesswork — it’s **structured investigation**.  
At its core, it’s about answering one question:  
> “Where is the problem — and what data proves it?”

**Good troubleshooters:**
- Observe symptoms before making changes.  
- Isolate each layer (physical → network → service → app).  
- Collect logs and evidence first, not assumptions.  
- Verify fixes with data, not “it feels faster.”  

---

## 🧱 Network Troubleshooting Flow

| Layer | What to Check | Example Questions |
|--------|----------------|------------------|
| **1. Physical / Link** | Cables, NICs, Wi-Fi, link lights | Is the device actually connected? |
| **2. Network (IP)** | IP address, gateway, subnet mask | Can I reach the next hop? |
| **3. Transport (Ports)** | TCP/UDP reachability | Is the port open? Is something blocking it? |
| **4. Application** | API, web page, authentication | Is the app responding correctly? |
| **5. Performance** | Latency, throughput, packet loss | Is it slow or dropping data? |
| **6. Cloud Routing** | VNet peering, NSGs, UDRs, Firewalls | Are routes and rules correct? |
| **7. Identity / Access** | Permissions, managed identities | Does the request even have rights to connect? |

Troubleshoot **from the bottom up** (connectivity → function → performance → permissions), and confirm each layer before moving on.

---

## ⚙️ Common Misunderstandings

| Myth | Reality |
|------|----------|
| “Ping works, so everything’s fine.” | Ping only checks ICMP, not app traffic. TCP/UDP can still fail. |
| “It’s slow, so it must be the network.” | Often the issue is DNS, CPU, or backend delay — not bandwidth. |
| “Throughput equals speed.” | High bandwidth doesn’t mean low latency; 10 Gbps can still feel slow. |
| “Azure VNets automatically talk to each other.” | Not without **VNet peering** or **Private Link**. |
| “Private Endpoint means private DNS automatically works.” | You still need a **Private DNS Zone** mapped correctly. |
| “Traceroute always works in the cloud.” | ICMP may be filtered — use **Network Watcher** or TCP-based tools instead. |

---

## 📡 Understanding Latency, Bandwidth & Throughput

| Concept | Meaning | Example |
|----------|----------|----------|
| **Latency** | Time it takes for one packet to reach destination (delay) | Measured in milliseconds (ms) |
| **Bandwidth** | Maximum data capacity of a path | Like lane width on a highway |
| **Throughput** | Actual data rate achieved | Affected by congestion, packet loss, TCP windowing |
| **Jitter** | Variation in packet delay | Can cause call/video issues |
| **Packet Loss** | Dropped packets during transmission | Leads to retransmissions and slowdown |

**Tip:** Always test both **latency** and **throughput** before assuming where slowness comes from.

---

## 🧠 Azure Tools for Troubleshooting

| Azure Tool | Focus Area | What It Helps You See |
|-------------|-------------|------------------------|
| **Network Watcher** | Connectivity, flow logs, packet capture | Path visibility, NSG or route misconfigurations |
| **Connection Monitor** | Ongoing reachability testing | Tracks endpoint health across regions |
| **NSG Flow Logs** | Ingress/Egress logging | Shows allowed/denied traffic |
| **Azure Monitor / Insights** | Performance & availability | Aggregated metrics, alerts, dashboards |
| **App Insights** | Application-level tracing | Response time, dependency failures |
| **Diagnostic Settings** | Logging across resources | Stream logs to Log Analytics or Storage |
| **Front Door / Traffic Manager metrics** | Global traffic routing | Endpoint health, latency by region |

> Cloud-native tools are your **first stop** before jumping into CLI or third-party captures.

---

## 🧰 Core Networking & Diagnostic Tools

A strong network specialist knows both **cloud** and **OS-level** tools.  
Here’s a quick lookup table organized by function.

| Tool | OS | Use / Description |
|------|----|-------------------|
| **ping** | Win/Linux/macOS | Check reachability (ICMP echo) |
| **tracert / traceroute** | Win/Linux/macOS | Show path to target, identify hops or blocks |
| **nslookup / dig** | All | DNS resolution checks |
| **ipconfig / ifconfig / ip addr** | Win/Linux/macOS | Show interface config & IPs |
| **netstat** | All | List active connections and listening ports |
| **telnet / Test-NetConnection / tnc** | Windows/PowerShell | Check port reachability (TCP) |
| **psping** | Windows | Advanced ping (TCP, UDP, latency and throughput) |
| **tcping** | Windows/Linux | Quick TCP port checks |
| **iperf / iperf3** | All | Measure network bandwidth and throughput |
| **pathping** | Windows | Hybrid of ping + traceroute + loss %
| **Wireshark** | All | Deep packet inspection (GUI-based capture) |
| **tcpdump** | Linux/macOS | CLI packet capture for analysis |
| **netcat (nc)** | Linux/macOS | Test sockets and port listening easily |
| **PowerShell Cloud Shell (az / pwsh)** | Azure / Web | Run Azure CLI or PowerShell directly from portal |
| **az network watcher test-connectivity** | Azure CLI | Check reachability between Azure resources |
| **az network watcher packet-capture** | Azure CLI | Trigger capture remotely on VMs |
| **Log Analytics (KQL)** | Azure Portal | Query NSG flow logs, connection events |
| **Wireshark + ETL (Event Trace Log)** | Windows | Local trace for TCP/SMB/HTTP diagnostics |
| **Azure Resource Graph** | Azure | Query resource relationships & dependencies |

> Each of these can be expanded later into its own micro-guide with screenshots, examples, and safe testing procedures.

---

## 🧭 General Troubleshooting Approach

1. **Define the problem clearly.**  
   What user, system, or process is affected? When did it start?
2. **Verify connectivity.**  
   Ping or test the next-hop (gateway, DNS, or endpoint).
3. **Check routing & access.**  
   Review NSGs, firewalls, VPNs, and peering paths.
4. **Validate app layer.**  
   Curl or browser test (for APIs, use `/health` endpoints).
5. **Check DNS resolution.**  
   Wrong or missing records often break private endpoint traffic.
6. **Gather logs.**  
   NSG flows, app logs, and Azure Monitor metrics — timestamped.
7. **Correlate events.**  
   Match network logs to app metrics or user reports.
8. **Reproduce & confirm fix.**  
   After changes, retest to prove restoration.

> Save logs privately and share only with authorized troubleshooters — protecting sensitive IPs and credentials.

---

## 💡 Key Azure-Specific Scenarios

| Symptom | Likely Checkpoints |
|----------|-------------------|
| VM can’t reach API | NSG rules, UDR route, private endpoint DNS |
| App Service can’t reach DB | VNet integration subnet, DNS zone mapping |
| Private Endpoint not resolving | Missing or wrong private DNS zone link |
| VNet peering not working | Use “Allow forwarded traffic” on both sides |
| Intermittent latency | Cross-region hops, bandwidth throttling, noisy neighbor, or App Service Plan under power |
| “Site down” alerts with 200 OK responses | WAF or Front Door caching stale responses |

---

## 📊 Performance Metrics to Watch

| Metric | Normal Range | When to Investigate |
|--------|---------------|--------------------|
| **Ping latency** | < 50 ms (in-region) | > 100 ms consistent |
| **Packet loss** | 0–1 % | Any > 2 % sustained |
| **Throughput** | 80–90 % of link cap | Drops < 50 % unexpectedly |
| **Jitter** | < 10 ms | Spikes cause video/VoIP issues |
| **DNS resolution time** | < 100 ms | Long lookups indicate DNS chaining |

---

## 🧩 Collecting Evidence Ethically

Always follow these when capturing data:
- Mask sensitive IPs or usernames when sharing logs.  
- Use test networks or anonymized environments when possible.  
- Don’t run packet captures on production traffic unless approved.  
- Delete captured data after analysis or retention period.  
- Never export customer or private data off secured systems.

> The goal is to **empower anyone** — even non-network specialists — to gather useful, non-sensitive data for experts to review.

---

## 🔄 Next Expansion Plan

Later, we’ll extend this chapter with:
- Individual tool mini-guides (Wireshark, tcpdump, iperf, etc.)  
- Walkthroughs for **Azure Network Watcher captures**  
- Step-by-step examples of **“circular captures”** for intermittent events  
- Deep-dive scenarios: DNS delay, TCP reset tracing, latency correlation  
- Example scripts to collect logs safely and reproducibly  

These will form a **practical toolkit** for both cloud engineers and support teams to diagnose network and app issues confidently.

---

## 📚 Resources to Add Later
- [ ] Azure Network Watcher documentation & tutorials  
- [ ] Microsoft “Troubleshoot Network Connectivity” learning path  
- [ ] Wireshark official user guide + sample filters  
- [ ] iperf3 documentation & usage calculator  
- [ ] Ethical data collection & privacy checklist  

---

_Last updated: {{ insert date }}_