# 🌐 OSI Model — Application, Presentation, Session Layers & Ports

> **Phase:** Networking | **Topic:** 06 | **Status:** ✅ Completed

---

## OSI Model — Quick Overview

The OSI model has 7 layers. Today we cover the top 3:

| Layer | Name | Simple Job |
|---|---|---|
| 7 | Application | Message made — what you see |
| 6 | Presentation | Encrypt / format the data |
| 5 | Session | Manage the connection |
| 4 | Transport | Break into segments, add ports |
| 3 | Network | Add IP addresses |
| 2 | Data Link | Add MAC addresses |
| 1 | Physical | Send as bits (0s and 1s) |

---

## Layer 7 — Application Layer

### What is it?

The Application Layer is the **first impression layer** — the one visible to you as a user.  
It converts your raw input into something the network understands using the right protocol.

> It doesn't decide which protocol to use — the protocol is already fixed based on the app you're using.

### Protocols at Layer 7

| Protocol | Used For |
|---|---|
| HTTP | Web browsing (unsecured) |
| HTTPS | Web browsing (secured) |
| SMTP | Sending emails |
| IMAP/POP3 | Receiving emails |
| FTP | File transfers |
| DNS | Domain name to IP lookup |
| SSH | Secure remote access |

### Real Example — What Happens When You Type google.com

Your browser converts your request into this at Layer 7:

```
GET / HTTP/1.1
Host: google.com
User-Agent: Chrome
```

This gets passed down to the next layer for further processing.

### Simple Rule

- Open a browser → automatically using **HTTP/HTTPS**
- Send an email → automatically using **SMTP**
- Transfer a file → automatically using **FTP**

---

## Layer 6 — Presentation Layer

### What is it?

The Presentation Layer deals with **how data is formatted, encrypted, and compressed.**  
Think of it as the translator — it makes sure data is in the right format before sending and after receiving.

### Three Main Jobs

**1. Encryption & Decryption**
- Before sending: converts plain text → encrypted data
- After receiving: converts encrypted data → plain text
- Example: **HTTPS** encrypts your data so nobody can read it in transit

**2. File Format Handling**
- Tells the system how to handle different file types
- When you receive a `.pdf` — presentation layer knows it's a PDF and handles it correctly
- Same for `.jpg`, `.mp4`, `.docx` etc

**3. Compression & Decompression**
- Compresses data before sending = smaller size = faster transfer
- Decompresses after receiving = original size restored
- Example: WhatsApp compresses images before sending — that's why quality drops slightly

### Simple Summary

```
Sending:   Plain text → Encrypt → Compress → send
Receiving: Receive → Decompress → Decrypt → Plain text
```

---

## Layer 5 — Session Layer

### What is it?

The Session Layer **establishes, manages, and terminates connections** between devices.  
Think of it as the connection manager.

### How it Works — Facebook Example

```
1. You open facebook.com
        ↓
2. You enter username + password → Login
        ↓
3. Session ESTABLISHED ✅
        ↓
4. A unique SESSION ID is created
        ↓
5. You browse Facebook freely
        ↓
6. You click Logout
        ↓
7. Session TERMINATED ❌
```

### What is a Session ID?

Every time you log in, the server creates a **unique Session ID** — a token that proves you're logged in.

```
Example Session ID: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Your browser stores this and sends it with every request — so the server knows it's you.

---

## Layer 4 — Transport Layer (Bonus — Ports Live Here!)

### What is it?

The Transport Layer breaks data into **segments** and adds **port numbers** so the receiving device knows which app to send data to.

### Two Protocols at Layer 4

| Protocol | Type | Reliable? | Speed | Used For |
|---|---|---|---|---|
| TCP | Connection-based | ✅ Yes — guarantees delivery | Slower | Web, email, file transfer |
| UDP | Connectionless | ❌ No — fire and forget | Faster | Video streaming, gaming, DNS |

### TCP — Transmission Control Protocol

TCP makes sure every packet arrives and in the right order.

**TCP 3-Way Handshake — How Connection is Established:**
```
Client → Server:  SYN        "Can we talk?"
Server → Client:  SYN-ACK    "Yes, ready!"
Client → Server:  ACK        "Great, let's go!"
        ↓
Connection established ✅
```

### UDP — User Datagram Protocol

UDP just sends data without caring if it arrives.

```
Client → Server: sends packets
No handshake, no confirmation
If a packet is lost — it's gone
```

Why use UDP? **Speed.** For YouTube video streaming, losing 1 packet is better than waiting for it — you'd rather have a tiny glitch than buffering.

---

## Ports — The Most Important Part 🔥

### What is a Port?

A port is like a **door number on a building.**  
Your device's IP address is the building — ports are the specific doors for each service.

```
IP Address = 192.168.1.5  (the building)
Port 80     = HTTP door
Port 443    = HTTPS door
Port 22     = SSH door
Port 21     = FTP door
```

### Why Do We Need Ports?

When you're watching YouTube AND using Facebook at the same time — your device is receiving data from both.

How does it know which data goes to which app?  
**Port numbers!**

```
YouTube data  → arrives on port 443 → goes to browser tab 1
Facebook data → arrives on port 443 → goes to browser tab 2
SSH session   → arrives on port 22  → goes to terminal
```

Each connection gets a unique combination of IP + Port.

### Well Known Ports — MEMORIZE THESE

| Port | Protocol | Used For |
|---|---|---|
| 20, 21 | FTP | File transfer |
| 22 | SSH | Secure remote access |
| 23 | Telnet | Remote access (unencrypted — dangerous!) |
| 25 | SMTP | Sending email |
| 53 | DNS | Domain name resolution |
| 80 | HTTP | Web browsing (unencrypted) |
| 110 | POP3 | Receiving email |
| 143 | IMAP | Receiving email |
| 443 | HTTPS | Web browsing (encrypted) |
| 445 | SMB | Windows file sharing |
| 3306 | MySQL | Database |
| 3389 | RDP | Windows Remote Desktop |
| 8080 | HTTP Alt | Alternative web server port |

### Port Ranges

| Range | Name | Description |
|---|---|---|
| 0–1023 | Well-known ports | Reserved for standard protocols |
| 1024–49151 | Registered ports | Used by applications |
| 49152–65535 | Dynamic/Private | Temporary connections |

### Check Open Ports on Linux

```bash
# See all open ports and listening services
netstat -tulnp

# See what's running on a specific port
ss -tulnp | grep :80

# Scan ports with Nmap
nmap -sV target_ip
```

---

## Full Picture — All 3 Layers Working Together

```
You type youtube.com in browser
        ↓
Layer 7 (Application)
→ Creates HTTP GET request
→ Uses HTTPS protocol
        ↓
Layer 6 (Presentation)
→ Encrypts the request with TLS
→ Compresses data
        ↓
Layer 5 (Session)
→ Establishes session with YouTube server
→ Creates Session ID
        ↓
Layer 4 (Transport)
→ Breaks into segments
→ Adds port number (443 for HTTPS)
→ Uses TCP for reliable delivery
        ↓
(continues down through Layers 3, 2, 1...)
        ↓
YouTube server receives → processes in reverse order → video plays ✅
```

---

## Quick Reference

| Layer | Name | Key Protocols | Job |
|---|---|---|---|
| 7 | Application | HTTP, HTTPS, FTP, DNS, SSH, SMTP | Creates the message |
| 6 | Presentation | TLS/SSL | Encrypt, format, compress |
| 5 | Session | NetBIOS, PPTP | Establish/end connections |
| 4 | Transport | TCP, UDP | Segment data, add port numbers |

---

## 🔐 Why This Matters in Hacking

- **Session hijacking:** steal someone's Session ID (Layer 5) → log in as them without needing password — very common web attack
- **Port scanning:** `nmap -sV target` scans all ports to find open services — first step in every pentest
- **Port 22 open:** SSH is running — try default credentials or brute force
- **Port 3389 open:** RDP is running — Windows machine, high value target
- **Port 445 open:** SMB running — check for EternalBlue (MS17-010) — the exploit used in WannaCry ransomware
- **HTTP vs HTTPS:** port 80 traffic can be intercepted and read — port 443 is encrypted
- **UDP attacks:** DNS amplification DDoS attacks abuse UDP port 53
- **TCP SYN flood:** send millions of SYN packets without completing handshake — crashes servers
- **Telnet (port 23):** completely unencrypted — if running, all traffic including passwords visible in Wireshark
