# 🌐 IP Address – A Complete Beginner's Guide

> *From `ipconfig` to default gateway, subnet masks, and who really assigns your IP.*

---

## 📌 Table of Contents

- [What is an IP Address?](#what-is-an-ip-address)
- [How to Find Your Own IP](#how-to-find-your-own-ip)
- [Who Assigns IP Addresses?](#who-assigns-ip-addresses)
  - [On Your Home Network](#on-your-home-network)
  - [On the Internet (Public IPs)](#on-the-internet-public-ips)
- [Default Gateway – The Door to the Internet](#default-gateway--the-door-to-the-internet)
- [Subnet Mask – Splitting Network & Host](#subnet-mask--splitting-network--host)
- [Private IP Ranges (Not Just 192.168.x.x)](#private-ip-ranges-not-just-192168xx)
- [Special IP Addresses](#special-ip-addresses)
- [DHCP – Automatic IP Assignment](#dhcp--automatic-ip-assignment)
- [APIPA – When DHCP Fails](#apipa--when-dhcp-fails)
- [IPv4 vs IPv6](#ipv4-vs-ipv6)
- [Quick Reference Card](#quick-reference-card)

---

## 🔍 What is an IP Address?

**IP address** = Internet Protocol address.  
Every device connected to the internet (or any network) has its own unique IP address. It works like a **postal address** – it tells the network where to send data.

> Example: `192.168.56.5`

---

## 🖥️ How to Find Your Own IP

| OS      | Command                 |
|---------|-------------------------|
| Windows | `ipconfig`              |
| Linux   | `ip addr show` or `ip a`|
| macOS   | `ifconfig` or `ip a`    |

### 📸 Sample output (Windows)

---

## 👤 Who Assigns IP Addresses?

### On Your Home Network

Your **router** (often a Wi-Fi box from your ISP) automatically assigns IPs to all your devices – phone, laptop, smart TV, etc.  
The router runs a **DHCP server** (Dynamic Host Configuration Protocol).

- Common home IP range: `192.168.56.x`
- Subnet mask: `255.255.255.0`

### On the Internet (Public IPs)

Your router itself gets a **public IP address** from your **Internet Service Provider (ISP)**.  
Public IPs are globally unique and managed by **IANA** (Internet Assigned Numbers Authority) and regional registries like ARIN, RIPE, APNIC.

> 🏠 Home network → private IPs  
> 🌍 Internet → public IPs (assigned by ISP)

---

## 🚪 Default Gateway – The Door to the Internet

The **default gateway** is the device that connects your local network to the outside world (usually your router).

- When your computer wants to talk to a device **outside** your network (e.g., `8.8.8.8`), it sends the traffic to the **default gateway**.
- In `192.168.56.x/24` networks, the gateway is often `192.168.56.1` or `192.168.56.254`.

### How to find your default gateway

| OS      | Command                       |
|---------|-------------------------------|
| Windows | `ipconfig`                    |
| Linux   | `ip route show default`       |
| macOS   | `netstat -rn \| grep default` |

---

## 🧮 Subnet Mask – Splitting Network & Host

A subnet mask tells you which part of the IP is the **network** and which part is the **host**.

### Example: `255.255.255.0` (CIDR: `/24`)

| IP Address      | Network part | Host part |
|----------------|--------------|-----------|
| `192.168.56.5` | `192.168.56` | `.5`      |

- All devices with the same network part are in the **same local network**.
- The host part can be from `1` to `254` (for `/24`).
- **Network address**: `192.168.56.0` (can’t assign to a device)  
- **Broadcast address**: `192.168.56.255` (can’t assign to a device)

> Broadcast is used to send a message to **all devices** on the network.

---

## 🏘️ Private IP Ranges (Not Just 192.168.x.x)

Private IPs are **not routable on the internet**. They are free to use inside any home or business network.

| Range                     | Subnet Mask      | CIDR | # of Hosts  |
|---------------------------|------------------|------|-------------|
| `10.0.0.0` – `10.255.255.255` | `255.0.0.0`      | `/8` | 16,777,214  |
| `172.16.0.0` – `172.31.255.255` | `255.240.0.0` | `/12`| 1,048,574   |
| `192.168.0.0` – `192.168.255.255` | `255.255.0.0` | `/16`| 65,534      |

> Most home routers use `192.168.0.0/24` or `192.168.1.0/24`. Your example `192.168.56.5` is less common but perfectly fine.

---

## 🔁 Special IP Addresses

| Address          | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| `127.0.0.1`      | **localhost** – your own computer (loopback). Used for testing.         |
| `0.0.0.0`        | Default route – represents “any address”.                               |
| `255.255.255.255`| Limited broadcast (to current network).                                 |
| `169.254.x.x`    | **APIPA** – assigned when DHCP fails (see below).                       |

---

## 📡 DHCP – Automatic IP Assignment

Most home routers act as **DHCP servers**. They:

- Automatically assign an unused IP to each device.
- Give the device the **subnet mask** and **default gateway**.
- Set a **lease time** (after which the IP might change).

> Without DHCP, you would have to configure every device manually (static IP).

### Check DHCP info
- Windows: `ipconfig /all`
- Linux: `cat /var/lib/dhcp/dhclient.leases` or check router admin page.

---

## ⚠️ APIPA – When DHCP Fails

If your device tries to get an IP from a DHCP server but **none responds**, Windows (and some others) will auto-assign an **APIPA address**:

- Range: `169.254.0.1` – `169.254.255.254`
- Subnet mask: `255.255.0.0`

> 🔴 Seeing a `169.254.x.x` IP usually means **your device can’t reach the router** (e.g., cable unplugged, router down).

---

## 🔄 IPv4 vs IPv6

| Feature     | IPv4                         | IPv6                          |
|-------------|------------------------------|-------------------------------|
| Bits        | 32                           | 128                           |
| Format      | Dotted decimal (`.`), e.g., `192.168.56.5` | Hexadecimal (`:`), e.g., `fe80::1` |
| Addresses   | ~4.3 billion (exhausted)     | 340 undecillion (enough forever) |
| Common use  | Still dominant in home nets  | Growing, often both run together (dual stack) |

> You don’t need to master IPv6 immediately, but know it exists.

---

## 📋 Quick Reference Card

| Concept            | Example / Value                                      |
|--------------------|------------------------------------------------------|
| Your home IP       | `192.168.56.5`                                       |
| Subnet mask        | `255.255.255.0` (or `/24`)                           |
| Network address    | `192.168.56.0` (cannot use)                          |
| Broadcast address  | `192.168.56.255` (cannot use)                        |
| Usable host range  | `192.168.56.1` – `192.168.56.254`                    |
| Default gateway    | Usually `192.168.56.1`                               |
| Localhost          | `127.0.0.1`                                          |
| APIPA range        | `169.254.x.x`                                        |
| Find your IP (Win) | `ipconfig`                                           |
| Find your IP (Linux)| `ip a`                                              |

---

## 🧠 What’s Next?

- **CIDR & VLSM** – How to break networks into smaller pieces.
- **Subnetting practice** – Calculate network ID, broadcast, first/last host from any IP.
- **Static vs Dynamic IP** – When and why to use static.
- **NAT (Network Address Translation)** – How one public IP serves many private devices.

---

> ✅ You now understand: IP address definition, who assigns it (router + ISP), default gateway, subnet mask basics, private ranges, and special addresses.  
>   
> 🚀 Keep going – networking is a superpower!
