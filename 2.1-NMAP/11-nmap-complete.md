# 🔍 Nmap — Complete Guide

> **Phase:** Networking | **Topic:** 11 | **Status:** ✅ Completed
> **Source:** TryHackMe — Nmap + Further Nmap rooms

---

## What is Nmap?

Nmap (Network Mapper) is the **most used port scanning tool** in cybersecurity. It's open source, free, and packed with features including its own scripting engine.

**Why we use it:**
- Every attack starts with information gathering
- Find open ports on a target
- Detect what services are running
- Detect the operating system
- Find vulnerabilities using scripts

---

## Ports — Quick Recap

Every computer has **65,535 ports** available.

- **Ports 0–1023** = Well-known ports (HTTP=80, HTTPS=443, SSH=22)
- **Ports 1024–49151** = Registered ports (applications)
- **Ports 49152–65535** = Dynamic ports (assigned automatically by your OS)

When you open multiple browser tabs — your OS automatically assigns different dynamic port numbers for each connection. That's how one device can talk to multiple websites simultaneously.

---

## Scan Types

### 3 Main Scan Types

| Scan | Flag | How it works |
|---|---|---|
| TCP Connect | `-sT` | Completes full 3-way handshake — noisy but reliable |
| SYN (Half-open) | `-sS` | Sends SYN, doesn't complete handshake — stealthier |
| UDP | `-sU` | Scans UDP ports — slower but important |

### Less Common Scan Types

| Scan | Flag | Purpose |
|---|---|---|
| TCP Null | `-sN` | Sends packet with no flags — evades some firewalls |
| TCP FIN | `-sF` | Sends FIN flag only — evades some firewalls |
| TCP Xmas | `-sX` | Sends FIN, PSH, URG flags — evades some firewalls |
| ICMP/Ping | `-sn` | Discovers live hosts — no port scan |

---

## Key Flags — The Most Important Ones

### Scan Type Flags

```bash
nmap -sS IP        # SYN scan (default when root — stealthiest)
nmap -sT IP        # TCP Connect scan (default without root)
nmap -sU IP        # UDP scan
nmap -sn IP        # Ping scan — just find live hosts, no ports
```

### Detection Flags

```bash
nmap -O IP         # OS detection — what operating system is the target running?
nmap -sV IP        # Service version detection — what version of each service?
nmap -A IP         # Aggressive mode — OS + version + traceroute + scripts
```

### Port Flags

```bash
nmap -p 80 IP           # Scan specific port (port 80 only)
nmap -p 80,443,22 IP    # Scan multiple specific ports
nmap -p 20-100 IP       # Scan a range of ports
nmap -p- IP             # Scan ALL 65,535 ports
```

### Verbosity Flags

```bash
nmap -v IP         # Verbose — more output
nmap -vv IP        # Very verbose — even more output
```

Think of verbosity like a juice factory — the higher the level, the more juice (output) you get. 😄

### Timing Flags

```bash
nmap -T0 IP        # Paranoid — very slow, very stealthy
nmap -T1 IP        # Sneaky
nmap -T2 IP        # Polite
nmap -T3 IP        # Normal (default)
nmap -T4 IP        # Aggressive — faster
nmap -T5 IP        # Insane — fastest but may miss things
```

> ⚠️ Higher speed = higher inaccuracy. Use T5 at your own risk — it can give wrong results.

### Output Flags

```bash
nmap -oN output.txt IP     # Normal format — human readable
nmap -oG output.txt IP     # Grepable format — easy to grep/filter
nmap -oA output IP         # All formats at once (saves .nmap, .gnmap, .xml)
```

> 💡 Always save your scan output! You only need to run the scan once — saves time and reduces detection risk.

### Script Flags (NSE)

```bash
nmap --script IP              # Run a specific script
nmap --script=vuln IP         # Run all vulnerability scripts
nmap --script=http-title IP   # Get HTTP page titles
nmap --script=banner IP       # Grab service banners
```

---

## Combining Flags — Real World Examples

```bash
# Most common CTF scan
nmap -sV -sC -p- target_ip

# Aggressive full scan
nmap -A -p- target_ip

# Stealthy SYN scan with version detection
nmap -sS -sV -T2 target_ip

# Quick scan of top 1000 ports with OS detection
nmap -O -sV target_ip

# Full aggressive scan saved to all formats
nmap -A -p- -oA full_scan target_ip

# Vulnerability scan
nmap --script=vuln target_ip

# Scan whole network for live hosts
nmap -sn 192.168.1.0/24
```

---

## Port States

Nmap reports ports in these states:

| State | Meaning |
|---|---|
| **Open** | Service is actively accepting connections |
| **Closed** | Port accessible but no service listening |
| **Filtered** | Firewall blocking — Nmap can't tell if open or closed |
| **Open\|Filtered** | Can't determine — usually UDP scans |
| **Closed\|Filtered** | Can't determine state |

---

## NSE — Nmap Scripting Engine

NSE scripts are Lua scripts that extend Nmap's functionality.

```bash
# Categories of scripts:
--script=safe       # Won't affect the target
--script=intrusive  # May affect the target
--script=vuln       # Check for vulnerabilities
--script=exploit    # Attempt to exploit vulnerabilities
--script=auth       # Check for authentication bypasses
--script=brute      # Brute force credentials
--script=discovery  # Gather more information
```

---

## Quick Reference — Most Used in CTFs

```bash
# Step 1 — Quick initial scan
nmap -sV target_ip

# Step 2 — Full port scan
nmap -p- target_ip

# Step 3 — Deep scan on discovered ports
nmap -sV -sC -p 22,80,443 target_ip

# Step 4 — Vuln scan
nmap --script=vuln target_ip
```

---

## Important Port Numbers to Know

| Port | Service | Why It Matters |
|---|---|---|
| 21 | FTP | File transfer — often misconfigured |
| 22 | SSH | Remote access — try default creds |
| 23 | Telnet | Unencrypted — sniff credentials |
| 25 | SMTP | Email — user enumeration |
| 53 | DNS | Zone transfer attacks |
| 80 | HTTP | Web app attacks |
| 139/445 | SMB | EternalBlue, pass-the-hash |
| 443 | HTTPS | Web app attacks |
| 3306 | MySQL | Database attacks |
| 3389 | RDP | Windows remote desktop |

---

## 🔐 Why This Matters in Hacking

- **First step in every pentest:** Nmap is always the first tool run on a target — reconnaissance before any exploitation
- **Version detection (-sV):** knowing Apache 2.4.49 is running = you can search CVEs for that exact version
- **OS detection (-O):** Windows vs Linux changes your entire attack approach
- **-sS SYN scan:** doesn't complete the handshake = doesn't appear in application logs — stealthier than -sT
- **-p- full port scan:** admins often run services on non-standard ports thinking nobody will find them — `-p-` finds them all
- **--script=vuln:** automates vulnerability checking — finds EternalBlue, Heartbleed, and other known vulns automatically
- **Always save output (-oA):** in real pentests you can't rescan — it causes noise and may alert the blue team
- **-T timing:** in real engagements use T1 or T2 — slow = stealthy. CTFs use T4-T5 — speed matters more
