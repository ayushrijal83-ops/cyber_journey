# 🔐 File & Directory Permissions

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## Permission Types

Linux has 3 types of permissions:

| Symbol | Name | What it allows |
|---|---|---|
| `r` | Read | View the contents of a file |
| `w` | Write | Edit or delete a file |
| `x` | Execute | Run a file as a program/script |

---

## Reading Permissions — `ls -la`

When you run `ls -la` you see something like:

```
-rwxr-xr--  1 alice users  file.sh
```

Break it down like this:

```
- rwx r-x r--
│ │   │   │
│ │   │   └── Others: read only
│ │   └────── Group: read + execute
│ └────────── Owner: read + write + execute
└──────────── File type (- = file, d = directory)
```

---

## CHMOD — Changing Permissions

`chmod` is used to change the permissions of a file or directory.

### Method 1 — Symbolic

```bash
# Set permission for current user (owner)
chmod u=rwx file.sh

# Set permission for group and others
chmod go=rx file.sh

# Set permission for everyone (all)
chmod a=rwx file.sh
```

| Symbol | Refers to |
|---|---|
| `u` | Owner (current user) |
| `g` | Group |
| `o` | Others |
| `a` | All (u + g + o) |

### Method 2 — Binary (Octal Numbers)

Each permission has a number value:

| Permission | Value |
|---|---|
| read (r) | 4 |
| write (w) | 2 |
| execute (x) | 1 |

Add them up to get the permission number:

```
rwx = 4+2+1 = 7
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4
```

**Example:**
```bash
# owner=rwx, group=r-x, others=r--
chmod 754 file.sh

# Most common — owner=rwx, group=rx, others=rx
chmod 755 file.sh

# Owner only — no one else can read
chmod 700 secret.sh
```

---

## Quick Reference

```bash
chmod +x file.sh        # add execute for everyone
chmod -w file.txt       # remove write for everyone
chmod 777 file.sh       # full permissions for everyone (dangerous)
chmod 600 id_rsa        # SSH key — owner read/write only
```

---

## 🔐 Why This Matters in Hacking

- **SUID bit** (`chmod +s`) — if set on a binary owned by root, it runs as root even when executed by a normal user → **privilege escalation**
- **World-writable files** (`chmod 777`) — if a root-owned script is writable by everyone, you can inject code → **root access**
- **`/tmp` is world-writable by default** — attackers drop payloads here
- In CTFs, misconfigured permissions are one of the most common ways to escalate privileges
