# 👤 File & Directory Ownership

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is Ownership?

Every file in Linux has two owners:
- **User** — the individual account that owns the file
- **Group** — the group that owns the file

You can see both when you run `ls -la`:

```
-rwxr-xr--  1 alice developers  file.sh
                 │     │
                 │     └── Group owner: developers
                 └──────── User owner: alice
```

---

## CHOWN — Change User Ownership

```bash
chown new_user filename
```

**Example — change owner to root:**
```bash
chown root test.py
```

**Change both user and group at once:**
```bash
chown root:root test.py
#      │    │
#      │    └── new group
#      └──────── new user
```

**Change ownership recursively (entire folder):**
```bash
chown -R root /var/www/html
```

---

## CHGRP — Change Group Ownership

```bash
chgrp new_group filename
```

**Example:**
```bash
chgrp root test.py
```

---

## Useful Commands

```bash
# See which groups a user belongs to
groups username

# Example
groups root

# See your own groups
groups

# See current user
whoami

# See user ID and group info
id
```

---

## Quick Reference Table

| Command | What it does |
|---|---|
| `chown user file` | Change file's user owner |
| `chown user:group file` | Change both user and group |
| `chown -R user folder` | Change ownership recursively |
| `chgrp group file` | Change file's group owner |
| `groups username` | See what groups a user is in |
| `id` | Show current user + group IDs |

---

## 🔐 Why This Matters in Hacking

- If a script **owned by root** is **writable by your user** → you can edit it to add malicious commands → when root runs it, you get root access
- **Privilege escalation** often involves finding files with weak ownership + permission combinations
- `chown` requires **root privileges** — if you can run it without sudo, that's a serious misconfiguration
- Always check file ownership when you land on a machine: `ls -la /etc/cron*` and `ls -la /var/www/`
