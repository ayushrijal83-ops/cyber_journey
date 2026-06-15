# 🔍 Nmap — Complete Guide

> **Phase:** Networking
> **Topic:** 11 — Nmap
> **Status:** ✅ Completed
> **Sources:** TryHackMe Nmap, Further Nmap, Industry Best Practices

---

# What is Nmap?

**Nmap (Network Mapper)** is the most widely used network scanning and reconnaissance tool in cybersecurity.

It is:

* Free and open source
* Fast and highly customizable
* Capable of host discovery
* Able to identify open ports
* Detect service versions
* Detect operating systems
* Run vulnerability checks through NSE scripts

## Why Pentesters Use Nmap

Every attack begins with information gathering.

Nmap helps you:

* Discover live hosts
* Find open ports
* Identify running services
* Determine software versions
* Detect operating systems
* Discover potential vulnerabilities

---

# Ports — Quick Recap

Every TCP/IP-enabled device has **65,535 ports**.

| Range       | Type                    | Purpose                              |
| ----------- | ----------------------- | ------------------------------------ |
| 0–1023      | Well-Known Ports        | Standard services (HTTP, SSH, HTTPS) |
| 1024–49151  | Registered Ports        | Application-specific services        |
| 49152–65535 | Dynamic/Ephemeral Ports | Temporary client connections         |

### Common Examples

| Port | Service |
| ---- | ------- |
| 21   | FTP     |
| 22   | SSH     |
| 23   | Telnet  |
| 25   | SMTP    |
| 53   | DNS     |
| 80   | HTTP    |
| 443  | HTTPS   |
| 445  | SMB     |
| 3306 | MySQL   |
| 3389 | RDP     |

---

# TCP Flags — The Secret Sauce

Nmap creates different scan types by manipulating TCP flags.

| Flag | Name           | Purpose                             |
| ---- | -------------- | ----------------------------------- |
| SYN  | Synchronize    | Starts a connection                 |
| ACK  | Acknowledgment | Confirms received data              |
| RST  | Reset          | Immediately terminates a connection |
| FIN  | Finish         | Gracefully closes a connection      |
| PSH  | Push           | Delivers buffered data immediately  |
| URG  | Urgent         | Marks urgent data                   |

---

# Major Scan Types

## TCP Connect Scan (-sT)

Performs a full TCP three-way handshake.

```text
Client → SYN
Server → SYN-ACK
Client → ACK
```

### Advantages

* Reliable
* Works without root privileges

### Disadvantages

* Easy to detect
* Appears in application logs

```bash
nmap -sT target
```

---

## SYN Scan (-sS)

Also called a **Half-Open Scan**.

```text
Client → SYN
Server → SYN-ACK
Client → RST
```

Connection is never completed.

### Advantages

* Faster
* Stealthier
* Less logging

### Disadvantages

* Requires root/admin privileges

```bash
nmap -sS target
```

---

## UDP Scan (-sU)

Used to discover UDP services.

```bash
nmap -sU target
```

Common UDP services:

| Port  | Service |
| ----- | ------- |
| 53    | DNS     |
| 67/68 | DHCP    |
| 123   | NTP     |
| 161   | SNMP    |

### Drawback

UDP scanning is significantly slower than TCP scanning.

---

# Advanced Scan Types

| Scan        | Flag | Purpose                   |
| ----------- | ---- | ------------------------- |
| Null Scan   | -sN  | Sends no flags            |
| FIN Scan    | -sF  | Sends FIN only            |
| Xmas Scan   | -sX  | Sends FIN, PSH, URG       |
| Maimon Scan | -sM  | FIN + ACK                 |
| ACK Scan    | -sA  | Firewall mapping          |
| Window Scan | -sW  | ACK variation             |
| Idle Scan   | -sI  | Zombie-based stealth scan |
| Ping Scan   | -sn  | Host discovery only       |

> **Note:** Null, FIN, and Xmas scans are ineffective against Windows systems because Windows typically responds with RST regardless of port state.

---

# Port State Responses

| Scan Type     | Open Port      | Closed Port |
| ------------- | -------------- | ----------- |
| SYN (-sS)     | SYN-ACK → RST  | RST         |
| Connect (-sT) | Full Handshake | RST         |
| Null (-sN)    | No Response    | RST         |
| FIN (-sF)     | No Response    | RST         |
| Xmas (-sX)    | No Response    | RST         |
| ACK (-sA)     | RST            | RST         |

---

# Scan Type Flags

```bash
nmap -sS target    # SYN Scan
nmap -sT target    # TCP Connect Scan
nmap -sU target    # UDP Scan
nmap -sn target    # Host Discovery Only
```

---

# Port Selection

### Single Port

```bash
nmap -p 80 target
```

### Multiple Ports

```bash
nmap -p 22,80,443 target
```

### Port Range

```bash
nmap -p 1-1000 target
```

### All Ports

```bash
nmap -p- target
```

### Top Ports

```bash
nmap --top-ports 100 target
```

---

# Detection Flags

## Service Version Detection

```bash
nmap -sV target
```

Example Output:

```text
Apache httpd 2.4.49
OpenSSH 8.2
```

---

## Operating System Detection

```bash
nmap -O target
```

Attempts to determine:

* Linux
* Windows
* BSD
* Network devices

---

## Aggressive Scan

```bash
nmap -A target
```

Includes:

* OS Detection
* Version Detection
* NSE Scripts
* Traceroute

---

# Verbosity

### Verbose

```bash
nmap -v target
```

### Very Verbose

```bash
nmap -vv target
```

Useful for monitoring long scans.

---

# Timing Templates

| Flag | Name       | Speed     |
| ---- | ---------- | --------- |
| -T0  | Paranoid   | Slowest   |
| -T1  | Sneaky     | Very Slow |
| -T2  | Polite     | Slow      |
| -T3  | Normal     | Default   |
| -T4  | Aggressive | Fast      |
| -T5  | Insane     | Fastest   |

```bash
nmap -T4 target
```

> Higher speed generally increases the chance of missing results.

---

# Fine-Tuning Performance

```bash
--min-rate 1000
--max-retries 2
--host-timeout 15m
--scan-delay 1s
```

Example:

```bash
nmap -sS --min-rate 1000 target
```

---

# Saving Output

## Normal Output

```bash
nmap -oN output.txt target
```

## Grepable Output

```bash
nmap -oG output.txt target
```

## All Formats

```bash
nmap -oA scan_results target
```

Creates:

```text
scan_results.nmap
scan_results.gnmap
scan_results.xml
```

> Always save your scans to avoid rescanning targets.

---

# NSE — Nmap Scripting Engine

NSE uses Lua scripts to automate discovery and vulnerability checks.

---

## Default Scripts

```bash
nmap -sC target
```

---

## Vulnerability Scan

```bash
nmap --script=vuln target
```

---

## HTTP Title Enumeration

```bash
nmap --script=http-title target
```

---

## Banner Grabbing

```bash
nmap --script=banner target
```

---

# NSE Categories

| Category  | Purpose                    |
| --------- | -------------------------- |
| safe      | Safe information gathering |
| default   | Common default scripts     |
| auth      | Authentication testing     |
| brute     | Brute-force attacks        |
| discovery | Information gathering      |
| vuln      | Vulnerability checks       |
| intrusive | Potentially disruptive     |
| exploit   | Exploitation scripts       |
| dos       | Denial-of-Service testing  |

Examples:

```bash
nmap --script "safe or default" target
```

```bash
nmap --script "vuln and not intrusive" target
```

```bash
nmap --script "http-*" target
```

---

# Port States

| State           | Meaning                     |
| --------------- | --------------------------- |
| open            | Service accepts connections |
| closed          | No service listening        |
| filtered        | Firewall blocks access      |
| open|filtered   | State cannot be determined  |
| closed|filtered | State cannot be determined  |

---

# Firewall & IDS Evasion

| Technique            | Flag              |
| -------------------- | ----------------- |
| Decoys               | -D                |
| Fragmentation        | -f                |
| Custom MTU           | --mtu             |
| Source Port Spoofing | --source-port     |
| Random Host Order    | --randomize-hosts |
| MAC Spoofing         | --spoof-mac       |
| Idle Scan            | -sI               |

Examples:

```bash
nmap -D RND:5,ME target
```

```bash
nmap -f target
```

```bash
nmap --source-port 53 target
```

---

# Real-World Examples

## CTF Enumeration

```bash
nmap -sV -sC -p- target
```

## Full Aggressive Scan

```bash
nmap -A -p- target
```

## Stealth Scan

```bash
nmap -sS -sV -T2 target
```

## Vulnerability Scan

```bash
nmap --script=vuln target
```

## Network Discovery

```bash
nmap -sn 192.168.1.0/24
```

## Common UDP Services

```bash
nmap -sU -p 53,67,68,123,161 target
```

---

# Recommended Pentesting Workflow

## Step 1 — Discover Live Hosts

```bash
nmap -sn 192.168.1.0/24 -oA live_hosts
```

## Step 2 — Quick Scan

```bash
nmap --top-ports 1000 -sV -oA quick target
```

## Step 3 — Full TCP Scan

```bash
nmap -p- -T4 -oA full_tcp target
```

## Step 4 — Deep Enumeration

```bash
nmap -sV -sC -p 22,80,443 target -oA deep
```

## Step 5 — Vulnerability Checks

```bash
nmap --script=vuln -p 22,80,443 target -oA vuln
```

---

# Why Nmap Matters

### Reconnaissance

Every penetration test begins with Nmap.

### Version Detection

Knowing a service version allows targeted vulnerability research.

Example:

```text
Apache 2.4.49
```

Searching for known CVEs becomes possible.

### Operating System Detection

Attack strategies differ greatly between:

* Windows
* Linux
* BSD
* Network appliances

### Full Port Scans

```bash
nmap -p- target
```

Administrators frequently run services on non-standard ports.

### NSE Vulnerability Detection

```bash
nmap --script=vuln target
```

Can identify vulnerabilities such as:

* EternalBlue
* Heartbleed
* SMB flaws
* Weak configurations

### Output Management

```bash
nmap -oA results target
```

Professional engagements require maintaining evidence and scan records.

---

# Quick Cheat Sheet

```bash
# BASIC SCANS
nmap target
nmap -sS target
nmap -sT target

# PORTS
nmap -p 80 target
nmap -p 1-1000 target
nmap -p- target

# DETECTION
nmap -sV target
nmap -O target
nmap -A target

# NSE
nmap -sC target
nmap --script=vuln target
nmap --script=http-title target

# OUTPUT
nmap -oA results target
nmap -oN results.txt target

# TIMING
nmap -T4 target
nmap -T2 target

# EVASION
nmap -f target
nmap -D RND:10 target
nmap -sI zombie target

# UDP
nmap -sU target
nmap -sU -p 53 target
```

---

# Final Takeaway

Nmap is the foundation of network reconnaissance and penetration testing.

A practical workflow is:

```text
Host Discovery
      ↓
Quick Scan
      ↓
Full Port Scan
      ↓
Service Enumeration
      ↓
Vulnerability Analysis
      ↓
Exploitation
```

Mastering Nmap means mastering the first phase of almost every cybersecurity assessment.
