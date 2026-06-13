# 📘 Subnetting Your Home Network – Complete Guide

## Based on Network Chuck’s EP6 + Corrections & Deep Dive

---

## 🧠 What is Subnetting?

Subnetting is the process of dividing a single network into smaller, manageable networks (subnets).  
It helps improve performance, security, and organization.

---

## 🏠 Starting Point – Your Home Network

Most home routers use a **private Class C IP range** automatically:

| Network Address | Subnet Mask | CIDR |
|----------------|-------------|------|
| `192.168.1.0`  | `255.255.255.0` | `/24` |

> The `192.168.1.0` is **chosen by the router** – you don’t calculate it. It’s from the reserved private range `192.168.x.x`.

---

## 📐 The Subnetting Goal

> “I want **4 networks** from my home network.”

Original: `192.168.1.0/24` (1 network)  
Target: 4 subnets

---

## 🔧 Step-by-Step – How to Create 4 Subnets

### 1. How many bits to borrow?
- Formula: \( 2^n \geq \) number of subnets needed
- Need 4 subnets → \( 2^2 = 4 \) → **borrow 2 bits** from the host portion.

### 2. New subnet mask in binary
Original mask (`/24`):  
`11111111.11111111.11111111.00000000`

Borrow 2 bits (turn them from 0 to 1):  
`11111111.11111111.11111111.11000000`

### 3. New subnet mask in decimal
Use the “big bro” table (128,64,32,16,8,4,2,1):

| Bit value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----------|-----|----|----|----|---|---|---|---|
| Our bits  | 1   | 1  | 0  | 0  | 0 | 0 | 0 | 0 |

Add: `128 + 64 = 192`  
So the last octet becomes `192` → new mask: **`255.255.255.192`**

### 4. New CIDR notation
Count all network bits: `8 + 8 + 8 + 2 = 26` → **`/26`**

✅ New network: `192.168.1.0/26`

### 5. Block size (increment between subnets)
Formula: `256 – new_subnet_mask_last_octet`  
`256 – 192 = 64`

Each subnet starts 64 apart.

### 6. List all 4 subnets (Network → Broadcast)

| Subnet | Network Address | Usable Hosts | Broadcast Address |
|--------|----------------|--------------|-------------------|
| 1      | `192.168.1.0`  | `192.168.1.1 – 192.168.1.62`  | `192.168.1.63` |
| 2      | `192.168.1.64` | `192.168.1.65 – 192.168.1.126` | `192.168.1.127` |
| 3      | `192.168.1.128`| `192.168.1.129 – 192.168.1.190`| `192.168.1.191` |
| 4      | `192.168.1.192`| `192.168.1.193 – 192.168.1.254`| `192.168.1.255` |

### 7. How many usable hosts per subnet?
- Host bits left: `32 – 26 = 6` bits
- Total addresses: \( 2^6 = 64 \)
- Subtract network address + broadcast address → `64 – 2 = 62` usable IPs ✅

---

## ❌ Common Mistakes (and how to fix them)

| Mistake | Why it’s wrong | Correct way |
|---------|----------------|--------------|
| Writing `225.225.225.0` instead of `255.255.255.0` | Typo – 225 is not a valid subnet mask octet | Always use 255 for full network octets |
| Saying broadcast addresses are usable | Broadcast is reserved for sending to all devices | Never assign broadcast IP to a device |
| Mixing up CIDR when starting from a subnetted network | You must add borrowed bits to the *current* CIDR, not back to /24 | Example: from `/26` borrow 3 bits → `/29`, not `/27` |
| Forgetting to subtract 2 for usable hosts | Network & broadcast addresses can’t be assigned | Always do \( 2^{\text{host bits}} - 2 \) |

---

## 🧪 Pop Quiz – You Try!

**Question:**  
> Can you assign `192.168.1.63` to a computer?

**Answer:**  
❌ No. `192.168.1.63` is the **broadcast address** of the first subnet (`192.168.1.0/26`).  
It’s used to send a message to *all* devices in that subnet, not to a single computer.

---

## 🔥 Challenge Problem (with your mistake + correction)

### Problem:
Start with `192.168.1.0/26` (already subnetted from `/24`).  
You need **8 subnets** from this `/26` network.

### ❌ Your first attempt:
- Borrow 3 bits ✅
- New CIDR = `/27` ❌
- New mask = `255.255.255.224` ❌

### ✅ Correct way:

- Current CIDR: `/26` (26 network bits, 6 host bits)
- Need 8 subnets → \( 2^3 = 8 \) → borrow **3 more bits**
- New network bits = `26 + 3 = 29` → **CIDR = `/29`**
- New subnet mask: `/29` = `11111111.11111111.11111111.11111000` = `255.255.255.248`
- Block size: `256 – 248 = 8`
- Usable hosts per subnet: \( 2^3 - 2 = 8 - 2 = 6 \)

### 📊 Correct subnets from `192.168.1.0/29`:
(Just the first few as example)

| Subnet | Network | Usable | Broadcast |
|--------|---------|--------|-----------|
| 1 | `192.168.1.0` | `.1 – .6` | `.7` |
| 2 | `192.168.1.8` | `.9 – .14` | `.15` |
| 3 | `192.168.1.16` | `.17 – .22` | `.23` |
| … | … | … | … |

> 💡 **Key lesson:** Always add borrowed bits to your *current* prefix, not the original classful /24.

---

## 📚 Quick Reference Card

| What you want | Borrow bits | New CIDR | New Mask | Block Size | Usable Hosts |
|---------------|-------------|----------|----------|------------|--------------|
| 4 subnets from /24 | 2 | /26 | 255.255.255.192 | 64 | 62 |
| 8 subnets from /24 | 3 | /27 | 255.255.255.224 | 32 | 30 |
| 16 subnets from /24 | 4 | /28 | 255.255.255.240 | 16 | 14 |
| 8 subnets from /26 | 3 | /29 | 255.255.255.248 | 8 | 6 |
| 4 subnets from /28 | 2 | /30 | 255.255.255.252 | 4 | 2 |

---

## ✅ You’re Ready!

You now understand:
- Where the base IP comes from (router, not calculation)
- How to borrow bits to create subnets
- How to find network, broadcast, usable hosts
- How to avoid common mistakes

🎉 Happy subnetting!