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