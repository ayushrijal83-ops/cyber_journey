# 💾 Disk Usage — du & df Commands

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## Two Commands to Know

| Command | What it does |
|---|---|
| `du` | Shows disk usage of **files and directories** |
| `df` | Shows disk usage of **entire drives/partitions** |

Simple way to remember: **du = directory usage**, **df = disk filesystem**

---

## du Command — Directory Usage

### Basic Usage

```bash
du -s *
```

- `*` = current working directory (all files and folders inside)
- `-s` = summarize — shows one total per item instead of listing everything inside

### Human Readable + Grand Total

```bash
du -sch *
```

Breaking down the flags:

| Flag | Meaning |
|---|---|
| `-s` | Summarize each item |
| `-c` | Print grand total at the bottom |
| `-h` | Human readable format (KB, MB, GB instead of raw bytes) |

**Example output:**
```
4.0K    Desktop
120M    Downloads
2.1G    Videos
500M    Documents
2.7G    total
```

### Combine du with grep

```bash
# Find directories/files that are 1GB in size
du -s * | grep "1G"

# Find anything over 500MB
du -sh * | grep "M"
```

This is piping in action — `du` produces the data, `grep` filters it.

### More Useful du Examples

```bash
# Check size of a specific folder
du -sh /var/log

# Check sizes of everything in /home
du -sh /home/*

# Find the top 10 largest directories
du -sh /* 2>/dev/null | sort -rh | head -10
```

---

## df Command — Disk/Drive Usage

`df` shows you information about your **entire drives and partitions** — how much total space, how much used, how much free.

### Basic Usage

```bash
df
```

### Human Readable Format

```bash
df -h
```

**Example output:**
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   18G   30G  38% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
```

### Useful df Examples

```bash
# Show all filesystems including virtual ones
df -ha

# Show only specific filesystem type
df -t ext4

# Check space on a specific directory
df -h /home
```

---

## man Command — Read the Manual

For ANY command you want to learn more about:

```bash
man du
man df
man grep
man find
```

This opens the full manual page. Press `q` to quit.

> 💡 **Pro tip:** When you encounter a new command or flag you don't understand, always try `man command` first before Googling.

---

## du vs df — When to Use Which

| Situation | Use |
|---|---|
| "My disk is full, what's taking up space?" | `du -sch *` |
| "How much total space do I have left?" | `df -h` |
| "Which folder is the biggest?" | `du -sh /* \| sort -rh` |
| "How many drives are mounted?" | `df -h` |

---

## Quick Reference Table

| Command | What it does |
|---|---|
| `du -s *` | Size of each item in current directory |
| `du -sch *` | Size + grand total + human readable |
| `du -sh /path` | Size of a specific folder |
| `du -s * \| grep "1G"` | Find items that are 1GB |
| `df -h` | All drives with human readable sizes |
| `df -ha` | All filesystems including virtual |
| `man du` | Full manual for du command |

---

## 🔐 Why This Matters in Hacking

- **Post-exploitation recon:** `df -h` quickly tells you how much storage a compromised machine has and what drives are mounted — useful for deciding where to store tools or exfiltrate data
- **Finding large files:** `du -sch *` helps locate large log files or database dumps that might contain sensitive information
- **Log analysis:** `/var/log` can get very large — `du -sh /var/log/*` helps identify which logs are growing suspiciously fast
- **CTF challenges:** some challenges hide files in unusual locations — checking disk usage can reveal unexpected large files
