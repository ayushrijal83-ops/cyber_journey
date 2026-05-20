# 🔎 The Find Command

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is Find?

`find` is one of the most powerful commands in Linux.  
It searches the **entire file system** for files or directories based on filters you set.  
Unlike `locate`, it searches in **real time** — so results are always up to date.

---

## Basic Syntax

```bash
find [where to search] [what to look for]
```

---

## Finding by Name

```bash
# Find a file by exact name
find / -name "filename.txt"

# Find case-insensitively
find / -iname "filename.txt"

# Find all .txt files
find / -name "*.txt"
```

---

## Finding by Type

```bash
# Find only files
find / -type f -name "*.sh"

# Find only directories
find / -type d -name "config"
```

| Type flag | Meaning |
|---|---|
| `-type f` | Files only |
| `-type d` | Directories only |
| `-type l` | Symbolic links only |

---

## Finding by Size

```bash
# Files bigger than 1MB
find / -size +1M

# Files smaller than 100KB
find / -size -100k

# Files exactly 1033 bytes (Bandit uses this!)
find / -size 1033c
```

| Size suffix | Meaning |
|---|---|
| `c` | bytes |
| `k` | kilobytes |
| `M` | megabytes |
| `G` | gigabytes |

---

## Finding by Permissions

```bash
# Find files with SUID bit set (important in hacking!)
find / -perm -4000

# Find world-writable files
find / -perm -o+w

# Find files with exact permission 777
find / -perm 777
```

---

## Finding by Owner

```bash
# Files owned by root
find / -user root

# Files owned by a specific group
find / -group shadow
```

---

## Suppressing Errors

When searching from `/` you'll get many "Permission denied" errors. Suppress them:

```bash
find / -name "secret.txt" 2>/dev/null
```

`2>/dev/null` sends all error messages to the trash — clean output only.

---

## Combining Filters

```bash
# Find files owned by root, with SUID, that are executable
find / -user root -perm -4000 -type f 2>/dev/null

# Find readable files not owned by root in /etc
find /etc -readable -not -user root 2>/dev/null
```

---

## Execute a Command on Found Files

```bash
# Print full details of every found file
find / -name "*.txt" -exec ls -la {} \;

# Read every found file
find / -name "passwords*" -exec cat {} \;
```

---

## Quick Reference Table

| Command | What it finds |
|---|---|
| `find / -name "file.txt"` | File by exact name |
| `find / -name "*.log"` | All log files |
| `find / -type f -size +1M` | Files bigger than 1MB |
| `find / -perm -4000` | SUID files (privesc targets) |
| `find / -user root -writable` | Root-owned but writable |
| `find / -name "*.txt" 2>/dev/null` | Suppress errors |

---

## 🔐 Why This Matters in Hacking

- **Privilege escalation:** `find / -perm -4000 2>/dev/null` finds SUID binaries — one of the most common privesc techniques
- **Finding sensitive files:** `find / -name "*.conf" 2>/dev/null` finds config files that may contain credentials
- **Bandit challenge:** multiple levels require `find` with specific size/permission/owner filters to locate the password file
- **Post exploitation:** after landing on a machine, `find` is the first tool used to map out interesting files
