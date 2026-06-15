# 🔍 Nmap — Complete Guide (Original + Detailed)

> **Phase:** Networking | **Topic:** 11 | **Status:** ✅ Completed  
> **Sources:** TryHackMe – Nmap & Further Nmap rooms + industry best practices

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

## TCP Flags – The Secret Sauce

Nmap manipulates TCP header flags to create different scan types. The 6 standard flags:

| Flag | Name | Function |
|------|------|----------|
| **SYN** | Synchronize | Initiates a connection |
| **ACK** | Acknowledgment | Confirms receipt of data |
| **RST** | Reset | Abruptly terminates a connection |
| **FIN** | Finish | Gracefully ends a connection |
| **PSH** | Push | Forces data delivery |
| **URG** | Urgent | Marks data as high priority |

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
| TCP Maimon | `-sM` | FIN+ACK — works on some BSD systems |
| ACK scan | `-sA` | Maps firewall rules |
| Window scan | `-sW` | Same as ACK on some systems |
| Idle (zombie) scan | `-sI zombieIP` | Ultimate stealth – no direct contact |
| ICMP/Ping | `-sn` | Discovers live hosts — no port scan |


### How Different Scans Behave on Open/Closed Ports

| Scan Type | **Open Port** | **Closed Port** |
|-----------|---------------|-----------------|
| SYN (-sS) | SYN‑ACK → RST | RST |
| Connect (-sT) | Completes handshake | RST after SYN |
| Null/FIN/Xmas | No response | RST |
| ACK (-sA) | RST | RST (but firewall may drop) |

> ✅ Null, FIN, Xmas scans fail on Windows (always send RST). Use SYN scans for Windows targets.

---

## Key Flags — The Most Important Ones

### Scan Type Flags

```bash
nmap -sS IP        # SYN scan (default when root — stealthiest)
nmap -sT IP        # TCP Connect scan (default without root)
nmap -sU IP        # UDP scan
nmap -sn IP        # Ping scan — just find live hosts, no ports
Port Flags
bash
nmap -p 80 IP           # Scan specific port (port 80 only)
nmap -p 80,443,22 IP    # Multiple specific ports
nmap -p 20-100 IP       # Scan a range of ports
nmap -p- IP             # Scan ALL 65,535 ports
nmap --top-ports 100 IP # Most common 100 ports
Detection Flags
bash
nmap -O IP         # OS detection — what operating system is the target running?
nmap -sV IP        # Service version detection — what version of each service?
nmap -A IP         # Aggressive mode — OS + version + traceroute + scripts
Verbosity Flags
bash
nmap -v IP         # Verbose — more output
nmap -vv IP        # Very verbose — even more output
Timing Flags
bash
nmap -T0 IP        # Paranoid — very slow, very stealthy
nmap -T1 IP        # Sneaky
nmap -T2 IP        # Polite
nmap -T3 IP        # Normal (default)
nmap -T4 IP        # Aggressive — faster
nmap -T5 IP        # Insane — fastest but may miss things
⚠️ Higher speed = higher inaccuracy. Use T5 at your own risk.

Fine‑tuning without templates:

bash
--min-rate 1000           # Send at least 1000 packets/sec
--max-retries 2           # Retry only twice
--host-timeout 15m        # Abort after 15 minutes
--scan-delay 1s           # Wait 1 second between probes
Output Flags
bash
nmap -oN output.txt IP     # Normal format — human readable
nmap -oG output.txt IP     # Grepable format — easy to grep/filter
nmap -oA output IP         # All formats at once (saves .nmap, .gnmap, .xml)
💡 Always save your scan output! You only need to run the scan once — saves time and reduces detection risk.

Script Flags (NSE)
bash
nmap --script IP              # Run a specific script
nmap --script=vuln IP         # Run all vulnerability scripts
nmap --script=http-title IP   # Get HTTP page titles
nmap --script=banner IP       # Grab service banners
NSE — Nmap Scripting Engine (Deep Dive)
NSE scripts are Lua scripts organized into categories:

Category	Safety	Example scripts
safe	✅ Won't crash	http-title, ssh-hostkey
intrusive	⚠️ May affect service	http-slowloris
vuln	🟡 Checks vulns	smb-vuln-ms17-010
exploit	🔴 Actually exploits	http-shellshock
auth	🔑 Auth bypass	ftp-anon
brute	🔓 Brute‑force	ssh-brute
discovery	🌐 Info gathering	smb-os-discovery
dos	⚠️ May cause downtime	teardrop
bash
nmap --script "safe or default" 10.10.10.1
nmap --script "vuln and not intrusive" 10.10.10.1
nmap --script "http-*" 10.10.10.1
Port States
State	Meaning
open	Service is actively accepting connections
closed	Port accessible but no service listening
filtered	Firewall blocking — Nmap can't tell if open or closed
open|filtered	Can't determine — usually UDP scans
closed|filtered	Can't determine state
Firewall & IDS Evasion
Technique	Flag	Explanation
Decoys	-D RND:5,ME	Hides your real IP
Fragmentation	-f	Splits packets into tiny fragments
MTU	--mtu 16	Manual fragment size
Source port spoof	--source-port 53	Pretend to be DNS
Randomize hosts	--randomize-hosts	Scan in random order
MAC spoof	--spoof-mac 0	Random MAC address
Idle (zombie) scan	-sI zombie:port	No direct contact – ultimate stealth
Combining Flags — Real World Examples
bash
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

# UDP heavy scan
nmap -sU -p 53,123,161,67,68 target_ip

# Decoy scan
nmap -D RND:10,10.10.10.1 10.10.10.2
Recommended Workflow
bash
# Step 1 — Discover live hosts
nmap -sn 192.168.1.0/24 -oA live_hosts

# Step 2 — Quick initial scan
nmap --top-ports 1000 -sV -oA quick target_ip

# Step 3 — Full port scan
nmap -p- -T4 -oA full_tcp target_ip

# Step 4 — Deep scan on discovered ports
nmap -sV -sC -p 22,80,443 target_ip -oA deep

# Step 5 — Vulnerability scan
nmap --script=vuln -p 22,80,443 target_ip -oA vuln
Important Port Numbers to Know
Port	Service	Why It Matters
21	FTP	Anonymous login, bounce attack
22	SSH	Brute‑force, default creds
23	Telnet	Cleartext credentials
25	SMTP	User enumeration, open relay
53	DNS	Zone transfer attacks
80	HTTP	Web app attacks
139/445	SMB	EternalBlue, pass‑the‑hash
443	HTTPS	Web app + TLS attacks
3306	MySQL	Default creds, SQL injection
3389	RDP	BlueKeep, brute‑force
5432	PostgreSQL	Default creds, RCE
27017	MongoDB	No‑auth default
🔐 Why This Matters in Hacking
First step in every pentest: Nmap is always the first tool run on a target — reconnaissance before any exploitation

Version detection (-sV): knowing Apache 2.4.49 is running = you can search CVEs for that exact version

OS detection (-O): Windows vs Linux changes your entire attack approach

-sS SYN scan: doesn't complete the handshake = doesn't appear in application logs — stealthier than -sT

-p- full port scan: admins often run services on non-standard ports thinking nobody will find them — -p- finds them all

--script=vuln: automates vulnerability checking — finds EternalBlue, Heartbleed, and other known vulns automatically

Always save output (-oA): in real pentests you can't rescan — it causes noise and may alert the blue team

-T timing: in real engagements use T1 or T2 — slow = stealthy. CTFs use T4-T5 — speed matters more

Quick Cheat Sheet (Printable)
bash
# BASICS
nmap target               # Default scan (TCP 1000 ports)
nmap -sS target           # SYN stealth (root)
nmap -sT target           # TCP connect (no root)

# PORT SELECTION
nmap -p 80 target
nmap -p- target
nmap -p 1-1000 target

# DETECTION
nmap -sV target           # Versions
nmap -O target            # OS
nmap -A target            # Aggressive

# SCRIPTING
nmap -sC target           # Default scripts
nmap --script=vuln target
nmap --script http-title target

# OUTPUT
nmap -oA filename target  # All formats
nmap -oN filename target  # Normal

# TIMING
nmap -T4 target           # Faster (CTF)
nmap -T2 target           # Stealthier (prod)

# EVASION
nmap -f target            # Fragment packets
nmap -D RND:10 target     # Decoys
nmap -sI zombie target    # Idle scan

# UDP
nmap -sU target
nmap -sU -p 53 target
Happy scanning! 🚀
