# 🛡️ Nmap — Firewall & IDS Evasion Techniques

> **Phase:** Networking | **Topic:** 14 | **Status:** ✅ Completed
> **Source:** TryHackMe Further Nmap

---

## The Problem — Windows Firewall Blocks ICMP

By default, a typical **Windows host firewall blocks all ICMP packets** (ping packets).

This creates a real problem because:
- We often use `ping` manually to check if a target is alive
- **Nmap does the same thing by default** — it pings before scanning
- If ICMP is blocked → Nmap thinks the host is **dead**
- A "dead" host gets **skipped entirely** — Nmap won't even bother scanning its ports

So a perfectly alive, fully running machine can look completely invisible to Nmap just because it blocks ping.

---

## The Solution — `-Pn` Flag

Nmap gives us a way around this:

```bash
nmap -Pn target_ip
```

### What `-Pn` Does

- Tells Nmap **not to bother pinging** the host before scanning
- Nmap will **always treat the target as alive**, regardless of ICMP response
- This effectively **bypasses the ICMP block**

### The Trade-off

⚠️ This comes at a cost — **potentially much slower scans.**

If the host genuinely IS dead (not just blocking ICMP), Nmap will still:
- Check every single specified port
- Wait for timeouts on each one
- Take significantly longer to complete

```
With ping check:    Dead host → skipped instantly
With -Pn:           Dead host → every port checked anyway → slow
```

So `-Pn` trades **speed** for **certainty** — use it when you suspect ICMP is blocked but you still want a real answer about the ports.

---

## Bonus — ARP for Local Networks

If you're already **directly on the local network** (same LAN as the target), Nmap has another trick available:

- It can use **ARP requests** instead of ICMP to determine if a host is alive
- ARP works at Layer 2 (Data Link) — many firewalls don't block this since it's needed for basic local network communication
- This happens automatically in certain scan modes when Nmap detects you're on the same subnet

This is why local network scans are often more reliable than scanning a host across the internet — ARP gives you a backup method ICMP-blocking firewalls can't easily stop.

---

## Other Firewall Evasion Switches

Nmap has several other switches specifically designed for firewall and IDS evasion. The official, more exhaustive reference list lives at:
```
nmap.org/book/man-bypass-firewalls-ids.html
```

Here are the ones worth knowing in detail:

---

### 1. `-f` — Fragment Packets

```bash
nmap -f target_ip
```

**What it does:**
- Splits packets into **smaller pieces** before sending them
- Makes it **less likely** that firewalls or IDS systems will detect and analyze the full packet
- Many older firewalls/IDS inspect packets as whole units — fragmenting can confuse this inspection process

**Why it works:**  
Some security devices struggle to reassemble and properly inspect fragmented traffic in real-time, especially under load — giving fragmented scans a better chance of slipping through undetected.

---

### 2. `--mtu <number>` — Custom Packet Size

```bash
nmap --mtu 16 target_ip
```

**What it does:**
- An **alternative to `-f`**
- Gives you **more precise control** over the exact size of packets being sent
- The value represents the **Maximum Transmission Unit** size

**Important rule:**  
The number you specify **must be a multiple of 8** (e.g. 8, 16, 24, 32...). This isn't optional — Nmap requires it because of how packet fragmentation works at the protocol level.

**Why use this over `-f`:**  
`-f` uses a fixed fragmentation size, while `--mtu` lets you fine-tune exactly how small (or large) you want each fragment to be — useful when trying to match a specific evasion strategy or work around a particular firewall's inspection limits.

---

### 3. `--scan-delay <time>ms` — Add Delay Between Packets

```bash
nmap --scan-delay 500ms target_ip
```

**What it does:**
- Adds a **deliberate delay** between each packet Nmap sends
- Time is specified in milliseconds (`ms`), seconds (`s`), or other units

**Two major use cases:**

**Use Case 1 — Unstable Networks**  
If you're scanning over a flaky or unreliable connection, spacing out packets reduces the chance of packets getting lost or scans failing due to network congestion.

**Use Case 2 — Evading Time-Based Detection**  
Many firewalls and IDS systems are configured to flag **rapid bursts of traffic** as suspicious (a classic sign of port scanning). By slowing down your packet rate, you can fly under these time-based detection thresholds — making your scan look more like normal, gradual traffic instead of an obvious automated scan.

```
Fast scan:  ████████████  → looks like an attack → triggers IDS alert
Slow scan:  █ · · █ · · █ · · █  → looks like normal traffic → flies under radar
```

---

### 4. `--badsum` — Generate an Invalid Checksum

```bash
nmap --badsum target_ip
```

**What it does:**
- Deliberately generates an **invalid/incorrect checksum** for the packets being sent

**Why this is actually useful — the clever logic:**

A **real, properly implemented TCP/IP stack** will:
1. Check the packet's checksum
2. Notice it's invalid
3. **Automatically drop the packet** — no response at all

However, **firewalls and IDS systems sometimes respond automatically** to packets **without bothering to verify the checksum first.**

This creates a detection technique:

```
Send packet with --badsum
        ↓
No response at all → likely a real OS/TCP stack (correctly dropped it)
        ↓
You GET a response → likely a firewall/IDS sitting in front (didn't check checksum)
```

So `--badsum` isn't really about bypassing a firewall directly — it's a clever way to **determine whether a firewall or IDS is present** in the first place, based on how the target reacts to a packet that should be invalid.

---

## Quick Reference — Firewall Evasion Cheat Sheet

| Switch | Purpose | Trade-off |
|---|---|---|
| `-Pn` | Skip ping check, treat host as always alive | Slower scans on dead hosts |
| `-f` | Fragment packets into smaller pieces | May not work against modern stateful firewalls |
| `--mtu <n>` | Custom fragment size (multiple of 8) | Requires understanding of MTU values |
| `--scan-delay <t>ms` | Add delay between packets | Significantly slower overall scan time |
| `--badsum` | Send invalid checksum packets | Used for detection, not direct bypass |

---

## Combining Evasion Techniques

In real scenarios, these switches are often combined for maximum effect:

```bash
# Skip ping check + fragment packets + add delay
nmap -Pn -f --scan-delay 300ms target_ip

# Skip ping check + custom MTU size
nmap -Pn --mtu 16 target_ip

# Test if a firewall/IDS exists at all
nmap --badsum target_ip
```

---

## Full Decision Flow — When to Use What

```
Is the host showing as "down" but you suspect it's alive?
        → Use -Pn

Is your scan getting blocked/detected by a firewall?
        → Try -f or --mtu to fragment packets

Is the firewall flagging rapid scan traffic specifically?
        → Add --scan-delay to slow down and blend in

Want to confirm whether a firewall/IDS exists before anything else?
        → Test with --badsum first
```

---

## 🔐 Why This Matters in Hacking

- **`-Pn` is essential in real engagements:** corporate Windows machines almost always block ICMP by default — without `-Pn` you'd think half your target network is offline when it's actually fully active
- **Fragmentation against legacy security:** older IDS/firewall appliances that don't properly reassemble fragments can be completely blind to fragmented scan traffic
- **`--scan-delay` mimics human/normal traffic:** real attackers in actual engagements slow scans down deliberately over hours or days specifically to avoid triggering automated alerting systems — this flag simulates that principle
- **`--badsum` as a recon technique:** before attempting any other evasion, knowing whether a firewall/IDS is even present changes your entire approach — this flag answers that question cheaply
- **ARP fallback on local networks:** when doing internal network pentests, this means ICMP-blocking host firewalls won't stop you from identifying live hosts if you're already inside the LAN
- **Combining techniques = real-world tradecraft:** professional red team engagements rarely use a single evasion switch — chaining `-Pn`, `-f`, and `--scan-delay` together reflects genuine, careful tradecraft used to avoid detection during actual assessments
