([go-home](../README.md))

# 🧪 Deployment Labs

Goal: Practice end-to-end cloud deployments (network + app + cost) using **Portal**, **Cloud Shell (PowerShell/Azure CLI)**, **Bicep**, **Terraform**, and a simple app stack (**Next.js** + **FastAPI** + **PostgreSQL**).  
We’ll keep labs short, affordable, and easy to tear down.

---

## 🧭 How to Use These Labs

Each lab includes:
- **What you build** (small scenario)
- **Networking focus** (VNet, Private Endpoint, gateways, global routing)
- **App pieces** (Next.js, FastAPI, Postgres)
- **Tool choices** (Portal / CLI / Bicep / Terraform)
- **Test plan** (what to click/run to prove it works)
- **Cost window & teardown** (stay under budget)

> We’ll keep the page minimal. Sample templates and tiny scripts can live in a future repo:
> **`/labs/<lab-name>/`** with short READMEs. (Placeholder link for later)

---

## 💰 Cost Guardrails (do this first every time)

- **One Resource Group per lab:** `rg-lab-<name>-<date>`  
- **Tags:** `env=lab`, `owner=me`, `expires=YYYY-MM-DD`  
- **Budget alert:** set a **$5–$15** budget with an **80%** alert  
- **Small SKUs:** App Service **B1**, Postgres **Basic/Dev**, Container Apps (scale to 0), AKS only if needed  
- **Teardown rule:** delete the **entire Resource Group** when finished

---

## 🧰 Quick Tool Switchboard

Choose one per lab (mix and match across labs to learn):
- **Azure Portal:** fastest to see what’s happening
- **Cloud Shell (PowerShell/Azure CLI):** no installs, repeatable steps
- **Bicep:** Azure-native IaC, readable
- **Terraform:** multi-cloud IaC, good comparison with Bicep

> Tip: Do **Lab 1** in Portal, then repeat **Lab 1** with Bicep or Terraform later.

---

## ⏱️ Time & Cost Planner (ballpark)

| Lab | Active Time | Approx Cost / Hour | Test Window |
|-----|-------------|--------------------|-------------|
| L1 App Service + VNet + Postgres (PE) | 60–90 min | $0.10–$0.25 | same day |
| L2 Terraform repeat of L1 | 45–75 min | $0.10–$0.25 | same day |
| L3 Front Door + light traffic | 30–60 min | $0.20–$2.00* | same day |
| L4 Private API via APIM (internal) | 45–90 min | $0.80–$1.50 | same day |
| L5 Container Apps (or AKS) | 60–120 min | $0.10–$0.60** | same day |

\* depends on traffic volume/egress  
\** AKS costs more; Container Apps is cheaper for labs

---

## 🧪 Lab 1 — “Hello Web/API” (App Service + VNet + Postgres)

**What you build:**  
- VNet with **web** and **data** subnets  
- **App Service** for **Next.js** (web) and **FastAPI** (API)  
- **Azure Database for PostgreSQL Flexible Server** with **Private Endpoint**  
- Web → API (public), API → DB (private)

**Tool choices:** Portal _or_ Cloud Shell _or_ Bicep

**Test plan:**  
- Visit web URL (home page loads)  
- Call API `/health` (200 OK)  
- Verify DB connection from API (one simple read/write)

**Cost window:** ~**$0.10–$0.25/hr**  
**Teardown:** delete the Resource Group

---

## 🧪 Lab 2 — Same as Lab 1, but with Terraform

**Goal:** Learn Terraform’s flow (init → plan → apply) using the same architecture.  
**Tip:** Keep variables minimal (location, names, SKUs).  
**Outcome:** You can recreate L1 from code, then destroy it safely.

**Cost window:** similar to L1  
**Teardown:** `terraform destroy` or delete the RG

---

## 🧪 Lab 3 — Global Entry (Front Door) + Safe Traffic

**What you build:**  
- **Azure Front Door** in front of your web app for global routing/caching  
- (Optional) **WAF** managed rules (prevention or detection)

**Networking focus:** global anycast, origin routing, health probes

**Traffic test (no scripts needed):**  
- Open the Front Door endpoint in a browser from two networks (mobile + Wi-Fi)  
- Refresh a few times; confirm Front Door reports healthy origin  
- Optional: use a simple load tool from your laptop for 2–3 minutes

**Cost window:** **$0.20–$2** depending on traffic volume/time  
**Teardown:** delete Front Door + RG if dedicated

---

## 🧪 Lab 4 — Private API with APIM (Internal Mode)

**What you build:**  
- **API Management** in **internal** mode  
- **Private Endpoint** for the API app; **Private DNS**  
- Web calls API **through APIM**; API is not public

**Networking focus:** private data path, name resolution, zero-trust design

**Test plan:**  
- From web app (or a jumpbox in the VNet), call the API route exposed by APIM  
- Confirm public access fails, private path succeeds

**Cost window:** **$0.80–$1.50/hr** (APIM dev tier)  
**Teardown:** delete RG

---

## 🧪 Lab 5 — Containers: Container Apps (or AKS) + Service Bus

**What you build:**  
- FastAPI as a container; small background worker container  
- **Azure Container Apps** environment (attach to VNet)  
- **Service Bus** queue for async messages (API → queue → worker)

**Networking focus:** internal endpoints, egress control, private DNS

**Test plan:**  
- Post a message to API (enqueues)  
- Worker processes and logs completion  
- Confirm scale to 0 works when idle (Container Apps)

**Cost window:** **cents → a few dollars/day** if left running; near-zero at idle  
**Teardown:** delete RG (Container Apps) or delete AKS cluster if you chose AKS

---

## 🔌 Hybrid Lab — Local App + Azure Database

**What you build:**  
- Next.js + FastAPI on your laptop (or Docker Compose)  
- Use **Azure Postgres** as the database  
- Optional: **Point-to-Site VPN** for Private Endpoint testing

**Networking focus:** private access from client machine, VPN routing, DNS

**Test plan:**  
- Connect from local API to Azure DB  
- Insert/read one record  
- Disconnect VPN and confirm private DB becomes unreachable (expected)

**Cost window:** Postgres **~$0.05–$0.15/hr** while active  
**Teardown:** delete DB or entire RG

---

## 🧠 Networking Combos (pick & mix)

| Goal | Suggested Combo |
|------|------------------|
| Simple public site | App Service (web) + public API |
| Global performance | Front Door → App Service (web) |
| Private backend | Web (public) → **APIM (internal)** → API (private) → DB (private) |
| Microservices taste | Container Apps (VNet) + Service Bus + Private Endpoints |
| Strong zero-trust | Front Door + App Gateway (WAF) + APIM (internal) + Private Endpoints |

---

## 📈 Observability Pack (add to any lab)

- **Application Insights** on web and API  
- **Log Analytics Workspace** + alerts (5xx spike, p95 latency, CPU)  
- **Network Watcher** connection monitor (web → API, API → DB)

**Cost:** cents for 1–2 hours of testing

---

## ✅ Minimal App Checks (no code dump)

- **API `/health`** returns OK  
- **API `/echo`** returns what you sent  
- **Frontend** shows “API status: OK” on a simple status page  
- **DB** proves read/write once (e.g., create a “pings” table, insert one row)

> You can keep tiny examples in a future repo under `/labs/common/` and link them here later.

---

## 🧹 Teardown Checklist (do every time)

- Delete the **Resource Group** used by the lab  
- Verify no shared resources were left behind (DBs, DNS zones, Front Door)  
- Clear budgets/alerts if they were one-off for the lab

---

## 🧭 Ethics & Safety

- Only test **your** endpoints.  
- Keep traffic low and time-boxed.  
- Tag everything with an **expiry** date.  
- Tear down after learning.

---

## 📚 Resources to Add Later
- [ ] Public sample repo with per-lab folders and tiny templates  
- [ ] Front Door vs App Gateway vs APIM quick chooser  
- [ ] Cost calculator presets for each lab  
- [ ] “One-click” cleanup (RG delete) snippet  
- [ ] Mini traffic toolkit notes (k6/hey/autocannon)

---

_Last updated: {{ insert date }}_