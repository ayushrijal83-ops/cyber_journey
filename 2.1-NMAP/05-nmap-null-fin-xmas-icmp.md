# 🎄 Nmap — NULL, FIN, Xmas & ICMP Scans

> **Phase:** Networking | **Topic:** 12 | **Status:** ✅ Completed
> **Source:** TryHackMe Further Nmap

---

## ⚠️ Important Note

These scan types (NULL, FIN, Xmas) are **less reliable on modern systems.** Windows often doesn't respond correctly to them, and modern firewalls/IDS can detect them. They work best on **older Linux/Unix systems.** Still good to know — but don't rely on them 100%.

---

## TCP Flags — Quick Refresher

Before understanding these scans, know these two flags:

### PSH (Push Flag)
**Meaning:** "Send data immediately"
- Normally TCP buffers data and sends in chunks
- With PSH = 1 → data is pushed instantly, no waiting
- **Real example:** real-time chat, SSH keypresses

### URG (Urgent Flag)
**Meaning:** "This data is urgent — handle first"
- Marks part of the packet as high priority
- Uses something called the **Urgent Pointer**
- Tells receiver: handle this part before normal data

**Memory trick:**
```
PSH → Push now
URG → Important now
```

---

## 1. Xmas Scan (`-sX`)

### How It Works

Sends a packet with **FIN + PSH + URG** flags all set to 1 — like a Christmas tree with multiple lights lit up 🎄

```
FIN + PSH + URG = 1
```

This creates a weird, abnormal packet that looks like "urgent + push + closing connection" all at once — which is exactly why it confuses some firewalls and IDS systems.

### Response Interpretation

| Response | Port State |
|---|---|
| No reply | Open / Filtered |
| RST reply | Closed |

### Use Case
- Stealth scanning — bypasses some older firewalls
- Works best on Unix/Linux systems

```bash
nmap -sX target_ip
```

---

## 2. FIN Scan (`-sF`)

### How It Works

Sends **only the FIN flag** — normally FIN is used to close an already established connection. Sending it without a connection ever being opened confuses the target.

### Response Interpretation

| Response | Port State |
|---|---|
| No reply | Open / Filtered |
| RST reply | Closed |

### Use Case
- Stealthy probing
- Avoids appearing in normal connection logs (since no full handshake ever happens)

```bash
nmap -sF target_ip
```

---

## 3. NULL Scan (`-sN`)

### How It Works

Sends a packet with **no flags set at all** — completely empty TCP header flags.

### Response Interpretation

| Response | Port State |
|---|---|
| No reply | Open / Filtered |
| RST reply | Closed |

### Use Case
- Same stealth purpose as FIN and Xmas
- Exploits how TCP/IP stacks react to malformed/abnormal packets

```bash
nmap -sN target_ip
```

---

## Why These Scans Work

They all exploit **inconsistent TCP/IP stack behavior.** Different operating systems respond differently to malformed packets that don't follow the normal handshake process — this inconsistency is what helps (sometimes) detect open ports silently.

---

## Quick Comparison Table

| Scan Type | Flag | Flags Used | Stealth | Reliability |
|---|---|---|---|---|
| Xmas | `-sX` | FIN + PSH + URG | High | Medium |
| FIN | `-sF` | FIN only | High | Medium |
| NULL | `-sN` | No flags | High | Medium |

---

## Important Reality Check

- Modern Windows systems often **don't respond correctly** → unreliable results
- IDS/Firewalls **can still detect** these scans despite being "stealthy"
- Works **best in Linux/Unix environments**
- Don't rely on these as your primary scan method — use them as supplementary techniques

---

## 4. ICMP Scan / Ping Sweep (`-sn`)

### What is an ICMP Scan?

ICMP scan finds out **if a host is alive** — it works at the **Network Layer** (Layer 3). Think of it like a ping, but performed in bulk across an entire range of IP addresses at once.

This bulk version is called a **ping sweep.**

### Why Ping Sweep Matters

When you first connect to a target network (black box assignment), your first objective is to get a **map of the network** — which IPs have active hosts and which don't.

### How It Works

```
Nmap sends ICMP echo packet to EVERY possible IP in the range
        ↓
If response received → mark IP as "alive"
        ↓
If no response → mark IP as possibly down (not always accurate)
```

### The Command

```bash
# Using hyphen notation
nmap -sn 192.168.0.1-254

# Using CIDR notation
nmap -sn 192.168.0.0/24
```

### What `-sn` Actually Does

The `-sn` switch tells Nmap **not to scan any ports** — it relies on:
1. **ICMP echo packets** (the ping itself)
2. **ARP requests** (if run as root/sudo, on local network)
3. **TCP SYN packet to port 443** (additional check)
4. **TCP ACK packet to port 80** (or SYN if not root) — additional check

So even though it's called a "ping scan," it actually uses **multiple techniques together** to determine if a host is alive — not just ICMP alone.

### Important Accuracy Note

Ping sweep results are **not always 100% accurate.** Some hosts block ICMP but are still alive — always treat this as a **baseline**, not a final answer.

### Example — Scan a /16 Network

For the 172.16.x.x network with netmask 255.255.0.0:

```bash
nmap -sn 172.16.0.0/16
```

`/16` because netmask 255.255.0.0 = 16 network bits.

---

## Quick Reference — All Scan Types Together

```bash
nmap -sS target          # SYN scan (stealthy, most common)
nmap -sT target          # TCP Connect scan (full handshake)
nmap -sU target           # UDP scan
nmap -sX target          # Xmas scan (FIN+PSH+URG)
nmap -sF target           # FIN scan
nmap -sN target           # NULL scan (no flags)
nmap -sn target_range     # Ping sweep — find alive hosts only
```

---

## 🔐 Why This Matters in Hacking

- **Ping sweep is always step 1:** before scanning ports on an entire network, `nmap -sn 192.168.1.0/24` tells you which hosts are even worth scanning
- **NULL/FIN/Xmas for firewall evasion:** older or misconfigured firewalls sometimes let these through when they'd block a normal SYN scan
- **Inconsistent OS responses = fingerprinting:** the way a target responds (or doesn't) to these unusual scans can help identify the OS
- **ICMP blocked ≠ host is down:** many real targets block ICMP but still have services running — always combine with port scans, don't rely on ping alone
- **Stealth vs reliability tradeoff:** these scans are stealthier but less reliable — in CTFs use them as a backup if SYN scans get blocked
- **CIDR for network sweeps:** understanding `/16`, `/24` etc lets you correctly scope your ping sweep to the entire target network
