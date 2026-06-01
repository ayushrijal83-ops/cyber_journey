# 🖥️ Enumerating Distribution & Kernel Information

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is Enumeration?

Enumeration means **gathering information about a system**.  
In hacking, the first thing you do after landing on a machine is enumerate — find out:
- What OS and version is running?
- What kernel version?
- What users exist?
- What's the hostname?

This information tells you **which exploits might work** against the system.

---

## OS & Distribution Information

```bash
# See full OS release info
cat /etc/os-release

# Shorter version
cat /etc/issue

# Another way
lsb_release -a
```

**Example output:**
```
NAME="Kali GNU/Linux"
VERSION="2024.1"
ID=kali
```

---

## Kernel Information

The kernel version is critical — older kernels have known exploits.

```bash
# Full kernel info
uname -a

# Kernel version only
uname -r

# System architecture (32-bit or 64-bit)
uname -m
```

**Example output of `uname -a`:**
```
Linux kali 6.6.9-amd64 #1 SMP Debian 6.6.9-1kali1 x86_64 GNU/Linux
         │              │                              │
         │              └── kernel build info          └── architecture
         └── kernel version
```

---

## Hostname

```bash
hostname
```

---

## CPU Information

```bash
cat /proc/cpuinfo
```

---

## Memory Information

```bash
# RAM usage
free -h

# Detailed memory info
cat /proc/meminfo
```

---

## All Users on the System

```bash
# List all users
cat /etc/passwd

# Just the usernames
cat /etc/passwd | cut -d: -f1

# Currently logged in users
who

# Your current user
whoami

# Your user ID and groups
id
```

---

## Environment Variables

```bash
# Show all environment variables
env

# Show PATH variable
echo $PATH
```

---

## Network Information

```bash
# Your IP address
ip a
ifconfig

# Active connections
netstat -an
ss -tulnp

# Routing table
route
ip route
```

---

## Running Processes

```bash
# All running processes
ps aux

# Interactive process viewer
top
htop
```

---

## Installed Software

```bash
# List all installed packages (Debian/Kali)
dpkg -l

# Find if specific tool is installed
which nmap
which python3
```

---

## Quick Enumeration Checklist

When you first land on any Linux machine, run these in order:

```bash
whoami                    # who am I?
id                        # my privileges
uname -a                  # kernel version
cat /etc/os-release       # OS info
hostname                  # machine name
cat /etc/passwd           # all users
ip a                      # network info
ps aux                    # running processes
env                       # environment variables
```

---

## 🔐 Why This Matters in Hacking

- **Kernel exploits:** knowing the kernel version lets you search for known CVEs — e.g. dirty cow (CVE-2016-5195) worked on kernels below 4.8.3
- **User enumeration:** finding other users on the system helps target privilege escalation
- **Network enumeration:** `ip a` shows you what other networks the machine is connected to — useful for pivoting
- In CTFs and real pentests, enumeration is **always the first step** after initial access — never skip it
