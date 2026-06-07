# 🏗️ Network Design — Bad, 2-Tier & 3-Tier Architecture

> **Phase:** Networking | **Topic:** 04 | **Status:** ✅ Completed

---

## What We Learn Here

Three types of network designs based on:
- Use case
- Size of organization
- How much reliability is needed

| Design | Used For | Reliability |
|---|---|---|
| Bad (1 device) | Home network | ❌ Single point of failure |
| 2-Tier | Small business | ✅ Good |
| 3-Tier | Large enterprise | ✅✅ Excellent |

---

## Bad Network Design — Home Network

### What it looks like

One single router that does everything:
- Acts as a **router**
- Acts as a **switch**
- Acts as a **WAP** (Wireless Access Point)

### The Problem

```
One router does EVERYTHING
        ↓
Router breaks or gets attacked
        ↓
Entire network goes down ❌
```

This is called a **Single Point of Failure** — one device failing kills the whole network.

### Why It's Bad for Security

- Everything goes through one device — one exploit = full network access
- No segmentation — all devices on same network
- No redundancy — no backup if it fails

> This is basically every home network. Fine for home, terrible for business.

---

## 2-Tier Network Design

### What it looks like

```
         [Layer 3 Switch] ←→ [Layer 3 Switch]   ← Tier 2
                ↓↓↓↓
    [Switch] [Switch] [Switch]                   ← Tier 1
       ↓↓       ↓↓       ↓↓
  [Devices]  [Devices]  [Devices]
```

### What is a Layer 3 Switch?

A Layer 3 switch = **Router + Switch combined in one device**
- Handles large amounts of traffic
- Routes between VLANs (virtual networks)
- Faster than using separate router + switch
- Suitable for **small to medium businesses**

### Why It's Better

- Two Layer 3 switches connected to each other
- If **one switch fails** → other keeps working ✅
- Smooth data flow between both switches
- More devices can connect without slowing down

### The Two Tiers

| Tier | What's Here | Job |
|---|---|---|
| Tier 2 | Layer 3 Switches | Routing + switching + redundancy |
| Tier 1 | Access Switches | Connect end devices (PCs, printers) |

---

## 3-Tier Network Design

### What it looks like

```
    [Router] ←→ [Router]                         ← Tier 3 (Core Layer)
          ↓↓↓↓
[L3 Switch] ←→ [L3 Switch]                       ← Tier 2 (Distribution Layer)
      ↓↓↓↓
[Switch] [Switch] [Switch]                        ← Tier 1 (Access Layer)
    ↓↓       ↓↓       ↓↓
[Devices]  [Devices]  [Devices]
```

### The Three Tiers Explained

| Tier | Layer Name | Devices | Job |
|---|---|---|---|
| Tier 3 | Core Layer | 2 Routers | Connect to internet, route between networks |
| Tier 2 | Distribution Layer | 4 Layer 3 Switches | Route between VLANs, apply policies |
| Tier 1 | Access Layer | Multiple Switches | Connect end user devices |

### Why It's the Best Design

- **2 routers** — if one fails, other takes over automatically
- **4 Layer 3 switches** — maximum redundancy
- Even if **multiple devices fail** — network keeps running
- Used by **large enterprises**, banks, data centers, hospitals
- Fully segmented — different departments on different network segments

### Redundancy Example

```
Router 1 fails
        ↓
Router 2 automatically handles all traffic
        ↓
Network continues working ✅ — nobody notices
```

---

## Full Comparison

| Feature | Bad Design | 2-Tier | 3-Tier |
|---|---|---|---|
| Devices | 1 router | 2 L3 switches + switches | 2 routers + 4 L3 switches + switches |
| Redundancy | ❌ None | ✅ Some | ✅✅ Full |
| Single point of failure | ✅ Yes | ❌ No | ❌ No |
| Suitable for | Home | Small business | Large enterprise |
| Cost | Cheap | Medium | Expensive |
| Security | ❌ Weak | ✅ Better | ✅✅ Best |

---

## Key Terms to Know

| Term | Meaning |
|---|---|
| Layer 3 Switch | Device that works as both router and switch |
| WAP | Wireless Access Point — provides WiFi |
| Redundancy | Having backup devices so network never goes down |
| Single Point of Failure | One device whose failure kills everything |
| VLAN | Virtual Local Area Network — segments a network logically |
| Core Layer | Top tier — connects to internet |
| Distribution Layer | Middle tier — routes between segments |
| Access Layer | Bottom tier — connects end devices |

---

## 🔐 Why This Matters in Hacking

- **Single point of failure = hacker's dream:** compromising the home router = controlling the entire network — all traffic, all devices
- **Network mapping:** understanding 2-tier and 3-tier designs helps you map out enterprise networks during a pentest
- **Lateral movement:** in 3-tier networks, different tiers are segmented — understanding this helps you plan how to move from one segment to another
- **Targeting routers first:** in a 3-tier network, compromising a core layer router gives you visibility over all traffic
- **VLAN hopping attack:** in 2/3-tier designs, VLANs separate departments — VLAN hopping lets you bypass that segmentation
- **Redundancy awareness:** attacking one router in a 3-tier design won't take down the network — you need to hit both
- **Access layer = easiest entry:** physical access to an access layer switch is the easiest way into an enterprise network — always check for unlocked network ports during physical pentests
