([go-home](../README.md))

# 🔒 Security & Access

Goal: Learn the basic ideas that keep networks, systems, and data safe — and understand how security and access control work together in the cloud.

---

## 🧭 What Is Security in Tech?

Security in technology means **protecting what matters** — your information, your systems, and the people who use them.  
Every app, website, and network faces the same challenge: how to make things accessible to the right people but invisible to everyone else.

Think of a secure system like a building:
- The **doors and keys** represent authentication (who gets in).  
- The **locks and alarms** represent authorization and monitoring (what they can do).  
- The **guards and cameras** represent detection and response (how problems are found and stopped).

Security isn’t a one-time setup — it’s a **constant process** of prevention, detection, and response.

---

## 💡 The Three Pillars of Security (CIA Triad)

Every security plan — whether for a school computer or a global cloud system — is built on three simple goals:

| Principle | Meaning | Example |
|------------|----------|----------|
| **Confidentiality** | Keep information private | Encrypt data, use passwords |
| **Integrity** | Keep data correct and unchanged | Use checks, version control |
| **Availability** | Keep systems working when needed | Backups, redundancy, uptime planning |

If one of these pillars breaks, users lose trust. A strong design balances all three.

---

## 🧱 Access Control: Who Gets In and What They Can Do

Access control is how systems decide **who can do what**.  
It starts with **identity**, then adds **permissions**, and finally enforces **boundaries**.

### Step 1: Authentication (Proving Who You Are)
Authentication means confirming identity.  
Common methods:
- **Password + Username** — the classic way.  
- **Multi-Factor Authentication (MFA)** — adds a phone or app code.  
- **Certificates / Keys** — used by apps or servers instead of people.

In Azure, this is handled through **Microsoft Entra ID (formerly Azure Active Directory)** — a global identity system that connects users, devices, and apps.

---

### Step 2: Authorization (Controlling What You Can Do)
Once identity is verified, the system checks what actions are allowed.

| Model | Description | Example |
|--------|--------------|----------|
| **Role-Based Access Control (RBAC)** | Assigns roles like *Reader* or *Owner* | User A can view logs, User B can edit resources |
| **Least Privilege** | Give only what’s needed | Developers don’t need billing access |
| **Separation of Duties** | Split responsibilities | One person deploys, another reviews |

Azure uses RBAC across almost everything — from resource groups to virtual machines — making it easy to assign fine-grained permissions.

---

### Step 3: Auditing and Monitoring
Even good systems need visibility.  
Monitoring tells you *who did what* and *when* — essential for accountability and detecting attacks.

- **Azure Monitor** and **Log Analytics** track events.  
- **Microsoft Defender for Cloud** looks for suspicious behavior.  
- **Activity Logs** show changes across subscriptions.

Auditing isn’t about blame — it’s about clarity.

---

## 🔐 Encryption: Protecting Data

Encryption is how we make information unreadable to anyone without the right key.

There are two main types:

### Data in Transit
Protects information **while it’s moving** between devices.  
Example: HTTPS uses SSL/TLS so no one can spy on your web traffic.

### Data at Rest
Protects information **where it’s stored**.  
Example: Azure automatically encrypts your storage accounts and databases using strong keys managed in **Azure Key Vault**.

Key Vault stores:
- Encryption keys  
- Passwords  
- Secrets  
- Certificates  

It’s the digital version of a locked safe.

---

## 🌐 Network Security Layers in Azure

Cloud security follows the idea of **defense in depth** — multiple layers of protection stacked together so that even if one fails, others hold strong.

### 1. Perimeter Protection
- **Azure Firewall** filters traffic between networks.  
- **DDoS Protection** shields against massive traffic floods.  
- **Application Gateway (with WAF)** protects web apps from common attacks like SQL injection.

### 2. Network Segmentation
- **Virtual Networks (VNets)** and **Subnets** separate resources.  
- **Network Security Groups (NSGs)** allow or deny traffic using rules (like “Allow HTTPS,” “Deny all else”).

### 3. Private Connections
- **Private Endpoints** connect to Azure services through private IPs — avoiding the public internet.  
- **VPN Gateway / ExpressRoute** connect on-premises systems to Azure securely.

### 4. Identity and Access
Even if attackers reach the network, they still need to prove identity before touching sensitive data.

---

## 🧠 Common Threats and How They’re Handled

| Threat | Description | Typical Defense |
|---------|--------------|-----------------|
| **Phishing** | Trick users into sharing credentials | MFA, user training |
| **Malware** | Harmful software on devices | Endpoint protection |
| **DDoS (Distributed Denial of Service)** | Overwhelms systems with traffic | Azure DDoS Standard |
| **Data Breach** | Unauthorized data access | Encryption, RBAC, monitoring |
| **Insider Threats** | Abuse of permissions | Least privilege, activity logs |

Security isn’t only technical — it’s also **human behavior**.  
Good training and awareness often stop attacks before they start.

---

## 🧭 Shared Responsibility in the Cloud

One of the biggest misunderstandings about cloud security is thinking the provider handles everything.  
In reality, security in Azure follows a **shared responsibility model**:

| Layer | Microsoft’s Responsibility | Your Responsibility |
|-------|-----------------------------|----------------------|
| Physical Data Centers | Hardware, facilities, power | None |
| Network Infrastructure | Global connectivity, backbone | Configure access correctly |
| Platform Services | OS patching, core runtime | Manage app security and data |
| Customer Data & Identities | — | You control user access, encryption, governance |

Azure gives you secure foundations — but it’s up to you to build securely on top of them.

---

## 🧰 Security Tools and Services in Azure

| Service | Purpose |
|----------|----------|
| **Microsoft Defender for Cloud** | Unified threat protection and compliance insights |
| **Sentinel (SIEM)** | Collects and analyzes logs across environments |
| **Key Vault** | Protects secrets, keys, and certificates |
| **Security Center Dashboards** | Show recommendations and risk levels |
| **Azure Policy** | Enforces rules like “All storage must be encrypted” |
| **Monitor + Alerts** | Tracks anomalies and sends notifications |

These tools give visibility and control — helping detect issues early before they become incidents.

---

## ⚙️ Designing Systems with Security in Mind

Security shouldn’t be added later — it should be part of the design from the start.  
This approach is called **Security by Design**.

### Practical Guidelines:
1. **Start with Identity:** Use strong authentication and role-based access.  
2. **Segment Networks:** Isolate critical systems in separate VNets/subnets.  
3. **Encrypt Everything:** At rest, in transit, and when possible, in use.  
4. **Monitor Constantly:** Use alerts for sign-ins, network spikes, and failed logins.  
5. **Plan for Incidents:** Backups, failover, and disaster recovery must be ready before they’re needed.

This mindset turns security from a barrier into a foundation for confidence.

---

## 🧩 Zero Trust: Modern Security Thinking

Traditional security assumed everything inside your network was safe.  
Modern cloud security flips that idea.

**Zero Trust** means:
- Never trust, always verify.  
- Authenticate every request.  
- Assume breach and minimize impact.

Azure supports Zero Trust through:
- Conditional Access policies  
- Identity Protection  
- Continuous monitoring and least-privilege enforcement

It’s a mindset, not a single tool — a way of building systems that expect change and risk.

---

## 🧭 Ethics in Security

Ethical security focuses on **protection, not control**.  
It’s about defending people’s rights while maintaining safety and performance.

Guidelines:
- Protect users’ privacy — only collect what’s necessary.  
- Be transparent about data use and storage.  
- Never exploit vulnerabilities for personal gain.  
- Follow laws, regulations, and responsible disclosure practices.  
- Remember: good security empowers trust, not fear.

---

## 📎 Bringing It All Together

Security and access are not just about passwords or firewalls — they’re about **trust**.  
Trust that data will stay private, systems will stay available, and people will be treated with fairness.

When designed well:
- **Networking** connects everything.  
- **Cloud infrastructure** gives it a home.  
- **System design** shapes how it works.  
- **Security & access** make sure it stays safe.

A secure system is an ethical system — one that respects users, protects information, and operates with integrity.

---

## 📚 Resources to Add Later
- [ ] Diagram: “How Zero Trust works in the cloud”  
- [ ] Comparison: Azure RBAC vs IAM in other platforms  
- [ ] Table: Encryption methods (TLS, AES, RSA) simplified  
- [ ] Example: Building least-privilege access plan  
- [ ] Checklist: Security by Design principles  

---

_Last updated: {{ insert date }}_