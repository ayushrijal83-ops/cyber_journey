# 🔌 Switches, Hubs & Access Points

> **Phase:** Networking | **Status:** ✅ Completed

---

## What Are These Devices?

These are all **network connecting devices** — they allow multiple devices to communicate with each other. But they work in very different ways.

| Device | Smart? | How it sends packets |
|---|---|---|
| Switch | ✅ Smart | Only to the destination device |
| Hub | ❌ Dumb | To ALL connected devices |
| Access Point | ❌ Dumb | To ALL devices (wirelessly) |

---

## Switch — The Smart One

A switch is a network device that connects multiple devices together and is **smart enough to send packets only to the right destination.**

### How Does a Switch Work?

1. When a device connects, the switch records its **MAC address**
2. It stores all MAC addresses in a **MAC address table**
3. When a packet arrives, it checks the destination MAC address
4. It sends the packet **only** to that specific device — nobody else sees it

### What is a MAC Address?

- MAC = Media Access Control
- Every network device has a unique MAC address
- It is a **physical layer address** (Layer 2 of the OSI model)
- Format example: `00:1A:2B:3C:4D:5E`

### Cisco Commands — View MAC Address Table

```bash
# Enter privileged mode first
enable

# View all captured MAC addresses
show mac-address-table
```

Output shows:
- VLAN number
- MAC Address
- Type (dynamic/static)
- Port it's connected to

### Why Switch is Smart

```
Device A wants to send packet to Device B
         ↓
Switch checks MAC address table
         ↓
Finds Device B is on port 3
         ↓
Sends packet ONLY to port 3
         ↓
Device C and D never see the packet ✅
```

---

## Hub — The Dumb One

A hub also connects multiple devices — but it has **no brain.**

### How a Hub Works

1. Device A sends a packet
2. Hub receives it
3. Hub sends it to **ALL connected devices** — no exceptions
4. Every device has to check if the packet is for them

### Why Hub is Dangerous

```
Device A sends a private packet
         ↓
Hub receives it
         ↓
Sends to ALL devices — B, C, D, E
         ↓
Everyone can see everyone's traffic ❌
```

This is why hubs are considered **insecure and obsolete** — nobody uses them in modern networks. But they're important to understand for hacking.

---

## Access Point — Wireless But Dumb

An access point converts a **wired network into wireless** — letting WiFi devices connect.

### The Problem

It behaves **exactly like a hub** — it broadcasts packets to all wirelessly connected devices. No intelligence about where to send traffic.

### In Simple Terms

```
Switch  = Smart + Wired
Hub     = Dumb  + Wired
Access Point = Dumb + Wireless
```

---

## Switch vs Hub vs Access Point — Full Comparison

| Feature | Switch | Hub | Access Point |
|---|---|---|---|
| Connection type | Wired | Wired | Wireless |
| Remembers MACs | ✅ Yes | ❌ No | ❌ No |
| Sends to all? | ❌ No | ✅ Yes | ✅ Yes |
| Speed | Fast | Slow | Medium |
| Security | ✅ More secure | ❌ Insecure | ❌ Insecure |
| Still used today? | ✅ Yes | ❌ Obsolete | ✅ Yes |

---

## OSI Layer Reference

| Device | OSI Layer |
|---|---|
| Hub | Layer 1 — Physical |
| Switch | Layer 2 — Data Link |
| Router | Layer 3 — Network |

---

## Quick Summary

- **Switch** — smart, remembers MAC addresses, sends packets only to destination
- **Hub** — dumb, sends packets to everyone, obsolete and insecure
- **Access Point** — wireless version of a hub, same dumb broadcast behavior

---

## 🔐 Why This Matters in Hacking

- **Hub = free sniffing:** if a network uses hubs, anyone connected can capture ALL traffic with Wireshark — passwords, cookies, everything in plain sight
- **Switch MAC flooding attack:** sending thousands of fake MAC addresses to overflow the switch's MAC table — when full, it behaves like a hub and broadcasts everything — this is called a **CAM table overflow attack**
- **ARP spoofing on switches:** even smart switches can be tricked by poisoning the ARP table — makes traffic go through the attacker's machine
- **Access point attacks:** since APs broadcast like hubs, WiFi sniffing is easy on unencrypted networks — WEP cracking, PMKID attacks
- **show mac-address-table:** during a pentest, if you access a switch, this command maps out every device on the network instantly
