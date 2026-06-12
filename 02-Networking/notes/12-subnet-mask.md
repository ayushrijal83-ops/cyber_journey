# 🎭 Subnet Mask — Complete Guide

> **Phase:** Networking | **Topic:** 09 | **Status:** ✅ Completed
> **Source:** NetworkChuck FREE CCNA — What is a Subnet Mask?

---

## What is a Subnet Mask?

A subnet mask tells you two critical things about an IP address:
- Which part is the **network** (fixed — same for all devices on this network)
- Which part is the **host** (variable — different for each device)

```
IP Address:   192.168.1.5
Subnet Mask:  255.255.255.0

In Binary:
IP:   11000000.10101000.00000001.00000101
Mask: 11111111.11111111.11111111.00000000
             │                   │
          Network part        Host part
       (1s = fixed)         (0s = changeable)
```

---

## The Golden Rule

```
1 = Network bit  →  FIXED — same for every device on the network
0 = Host bit     →  VARIABLE — changes for each device
```

This is the most important thing to understand about subnet masks.

---

## How to Count Available IP Addresses

### The Formula

```
2^(number of host bits) = total possible addresses
```

### Example — /24 Subnet (255.255.255.0)

```
Subnet mask: 11111111.11111111.11111111.00000000
                                         │
                                    8 zeros = 8 host bits

2^8 = 256 total addresses
```

But wait — 2 addresses are always reserved:
- **Network address** (first IP) — identifies the network
- **Broadcast address** (last IP) — sends to all devices

```
Total addresses:     256
Minus reserved:       -2
                    ────
Usable hosts:        254
```

### Your Notes Had a Small Error 😄

You wrote 224 usable addresses — the correct answer is **254.**  
(256 - 2 = 254, not 224)

---

## Visual Breakdown — /24 Network

```
Network: 192.168.1.0/24

192.168.1.0    → Network address    ❌ reserved
192.168.1.1    → First usable host  ✅
192.168.1.2    → Usable host        ✅
...
192.168.1.254  → Last usable host   ✅
192.168.1.255  → Broadcast address  ❌ reserved

Total usable: 254 addresses
```

---

## How to Get More IP Addresses — Flipping Bits

If you need more IPs, you **flip a 1 to a 0** in the subnet mask.  
This moves a bit from the network portion to the host portion — giving you more host addresses.

### Example — Going from /24 to /23

```
/24:  11111111.11111111.11111111.00000000  →  255.255.255.0  →  254 hosts
/23:  11111111.11111111.11111110.00000000  →  255.255.254.0  →  510 hosts
```

You flipped one bit → doubled your available addresses!

```
/24 → 2^8  - 2 = 254 hosts
/23 → 2^9  - 2 = 510 hosts
/22 → 2^10 - 2 = 1022 hosts
/21 → 2^11 - 2 = 2046 hosts
```

Every time you flip one more bit → double the addresses.

---

## Subnet Mask Cheat Sheet

| CIDR | Subnet Mask | Binary (last octet) | Host Bits | Total IPs | Usable Hosts |
|---|---|---|---|---|---|
| /24 | 255.255.255.0 | 00000000 | 8 | 256 | 254 |
| /25 | 255.255.255.128 | 10000000 | 7 | 128 | 126 |
| /26 | 255.255.255.192 | 11000000 | 6 | 64 | 62 |
| /27 | 255.255.255.224 | 11100000 | 5 | 32 | 30 |
| /28 | 255.255.255.240 | 11110000 | 4 | 16 | 14 |
| /29 | 255.255.255.248 | 11111000 | 3 | 8 | 6 |
| /30 | 255.255.255.252 | 11111100 | 2 | 4 | 2 |
| /16 | 255.255.0.0 | — | 16 | 65536 | 65534 |
| /8  | 255.0.0.0 | — | 24 | 16777216 | 16777214 |

---

## How Subnet Mask Works With IP — AND Operation

Your computer uses a **bitwise AND** operation to find the network address:

```
IP Address:   192.168.1.5
              11000000.10101000.00000001.00000101
AND
Subnet Mask:  255.255.255.0
              11111111.11111111.11111111.00000000
                                         ↓
Result:       11000000.10101000.00000001.00000000
              = 192.168.1.0  ← This is the Network Address
```

AND rules:
```
1 AND 1 = 1
1 AND 0 = 0
0 AND 1 = 0
0 AND 0 = 0
```

This is how your device knows which network it belongs to.

---

## Subnetting — Splitting a Network

Subnetting means taking a large network and **dividing it into smaller ones.**

### Why Subnet?

- Security — isolate departments
- Performance — reduce broadcast traffic
- Organization — separate HR from Engineering from Finance

### Example — Splitting 192.168.1.0/24

```
Original /24 network: 254 hosts

Split into 4 subnets using /26:
├── 192.168.1.0/26    → hosts .1  to .62   (62 hosts)
├── 192.168.1.64/26   → hosts .65 to .126  (62 hosts)
├── 192.168.1.128/26  → hosts .129 to .190 (62 hosts)
└── 192.168.1.192/26  → hosts .193 to .254 (62 hosts)
```

---

## Finding Network & Broadcast Address

For any IP with CIDR:

```
Network address  = IP AND subnet mask
Broadcast address = Network address with all host bits set to 1
First host = Network address + 1
Last host  = Broadcast address - 1
```

### Example — 192.168.1.100/26

```
/26 = subnet mask 255.255.255.192 = last octet 11000000

Network:   192.168.1.64   (100 AND 192 = 64)
Broadcast: 192.168.1.127  (64 + 63 = 127, or set all host bits to 1)
First host: 192.168.1.65
Last host:  192.168.1.126
Usable:     62 hosts
```

---

## Quick Reference — Key Formulas

```
Number of usable hosts = 2^(host bits) - 2
Number of subnets      = 2^(subnet bits borrowed)
Host bits              = 32 - CIDR number
```

---

## 🔐 Why This Matters in Hacking

- **Nmap scanning:** `nmap -sn 192.168.1.0/24` scans all 254 hosts — subnet mask defines your scan range
- **Scope calculation:** pentest scopes use CIDR — `/24` means 254 targets, `/16` means 65,534 targets
- **Network segmentation bypass:** understanding subnets helps you identify which networks you can and cannot reach during a pentest
- **Pivot planning:** when you land on 10.10.10.5/24 — you know 10.10.10.0–10.10.10.255 is your local network
- **VLAN hopping:** subnets are often mapped to VLANs — understanding subnet boundaries helps plan VLAN attacks
- **Internal recon:** `ip a` shows your subnet — instantly tells you the network range to scan for other hosts
- **CTF machines:** almost every HackTheBox and TryHackMe machine involves identifying the correct subnet to scan
