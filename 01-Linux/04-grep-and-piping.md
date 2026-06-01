# 🔍 Grep & Piping

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is Grep?

`grep` is used to **search for specific text** inside files or command output.  
It is **case sensitive** by default — so `Ayush` and `ayush` are treated as different things.

---

## Method 1 — Grep Only

```bash
grep "searchterm" ./path/to/file
```

**Example:**
```bash
grep "root" /etc/passwd
```

### Bypass Case Sensitivity with `-i`

```bash
grep -i "searchterm" ./path/to/file
```

Now it matches regardless of uppercase or lowercase.

---

## Method 2 — Grep with Pipe `|`

The pipe `|` takes the output of one command and passes it directly into another command.  
Think of it like a funnel — left side produces data, right side processes it.

```bash
cat ./Documents/test.txt | grep "ayush"
```

What's happening here step by step:
1. `cat` reads the file and outputs its contents
2. `|` passes that output to `grep`
3. `grep` filters and shows only lines containing "ayush"

---

## Real World Examples

```bash
# Search for a specific package in your installed list
apt list | grep neofetch

# Search for a user in the password file
cat /etc/passwd | grep "root"

# Find a specific process running
ps aux | grep "apache"

# Search Nmap results for open ports
cat scan_results.txt | grep "open"
```

---

## Useful Grep Flags

| Flag | What it does |
|---|---|
| `-i` | Case insensitive search |
| `-r` | Search recursively through folders |
| `-n` | Show line numbers in results |
| `-v` | Show lines that do NOT match |
| `-c` | Count how many lines matched |

**Examples:**
```bash
# Search recursively through entire /etc folder
grep -r "password" /etc/

# Show line numbers
grep -n "root" /etc/passwd

# Show everything EXCEPT root
grep -v "root" /etc/passwd

# Count matches
grep -c "error" /var/log/syslog
```

---

## Pipe Chaining — Multiple Pipes

You can chain multiple pipes together:

```bash
cat /etc/passwd | grep "home" | grep -v "root"
```

This reads the file → filters lines with "home" → then removes any that also contain "root".

---

## `>` vs `|` — What's the Difference?

| Symbol | What it does |
|---|---|
| `>` | Redirects output to a **file** |
| `\|` | Redirects output to another **command** |

```bash
# Save grep results to a file
grep "root" /etc/passwd > results.txt

# Pass grep results to another command
grep "root" /etc/passwd | cut -d: -f1
```

---

## 🔐 Why This Matters in Hacking

- **Finding passwords in files:** `grep -r "password" /var/www/`
- **Filtering Nmap output:** `nmap -sV target | grep "open"`
- **Log analysis:** `cat /var/log/auth.log | grep "Failed"`
- **CTFs:** grep is used in almost every single challenge to filter large amounts of data
- Bandit levels heavily rely on grep + piping to find hidden passwords
