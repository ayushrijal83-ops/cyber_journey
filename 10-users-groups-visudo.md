# 👥 Users, Groups & Permissions with visudo

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## Why This Matters

Every Linux system has multiple users and groups. As a hacker or sysadmin you need to know:
- How to create, modify, and delete users
- How to manage groups
- How sudo permissions work
- Where passwords are actually stored

---

## Adding Users — Two Commands

| Command | Behavior |
|---|---|
| `adduser` | Interactive — asks for password & details automatically |
| `useradd` | Silent — creates user but you must set password manually |

### adduser (recommended for beginners)

```bash
sudo adduser newusername
```

After running this it asks for password, full name, and other info automatically.

### useradd (manual setup required)

```bash
useradd newusername
```

User is created but has no password yet — you must set it manually after.

---

## Setting a Password

```bash
sudo passwd username
```

Use this after creating a user with `useradd`, or any time you want to change a password.

---

## Where Users are Stored

```bash
cat /etc/passwd
```

This file contains all users on the system with details like:
- Username
- User ID (UID)
- Group ID (GID)
- Home directory
- Default shell

**Example line:**
```
ayush:x:1001:1001::/home/ayush:/bin/bash
        │
        └── x means password is stored in /etc/shadow
```

---

## Where Passwords are Stored — /etc/shadow

```bash
sudo cat /etc/shadow
```

The `x` you see in `/etc/passwd` means the actual password is stored in `/etc/shadow`.  
Passwords here are **hashed** — not readable as plain text.  
You need sudo permission to read this file.

---

## Modifying Users — usermod

`usermod` is used to change existing user settings.

### Change default shell

```bash
sudo usermod username --shell /bin/bash
```

### Rename a user

```bash
sudo usermod -l newname oldname
```

Example — rename `hulk` to `ironman`:
```bash
sudo usermod -l ironman hulk
```

`-l` = new login name. Note: `ironman` is the new name, `hulk` is the existing one.

### Give a user a home directory

```bash
sudo usermod username -m
```

### Add user to a group

```bash
sudo usermod -aG groupname username
```

- `-G` = specify group
- `-a` = append (don't remove from other groups)

---

## Switching Users — su

`su` = switch user

```bash
# Switch with sudo
sudo su - username

# Switch directly
su - username
```

The `-` (hyphen) is important — it loads the user's full environment (shell config, variables, etc).  
Always put a space before and after the hyphen.

---

## Deleting Users

```bash
sudo userdel username
```

To also delete their home directory:
```bash
sudo userdel -r username
```

---

## The sudoers File & visudo

The sudoers file controls **which users have sudo (root) power.**

### Open with visudo (recommended way)

```bash
sudo visudo
```

Always use `visudo` — it checks for syntax errors before saving. Editing directly can break sudo for everyone.

### What you'll find inside

Two important sections:
- **root user line** — gives root full sudo access
- **sudo group** — any user in the sudo group gets sudo access

```
root    ALL=(ALL:ALL) ALL
%sudo   ALL=(ALL:ALL) ALL
```

To give a user sudo power, add them to the sudo group:
```bash
sudo usermod -aG sudo username
```

---

## Group Management

### Create a group

```bash
sudo groupadd groupname
```

### View all groups

```bash
cat /etc/group
```

### Add user to a group

```bash
sudo usermod -aG groupname username
```

### Remove user from a group

```bash
sudo gpasswd -d username groupname
```

`-d` = delete/remove the user from that group

### See what groups a user belongs to

```bash
groups username
```

---

## Quick Reference Table

| Command | What it does |
|---|---|
| `sudo adduser name` | Add user interactively |
| `useradd name` | Add user silently |
| `sudo passwd name` | Set/change password |
| `cat /etc/passwd` | View all users |
| `sudo cat /etc/shadow` | View hashed passwords |
| `sudo usermod name --shell /bin/bash` | Change user's shell |
| `sudo usermod -l newname oldname` | Rename a user |
| `sudo usermod -aG group user` | Add user to group |
| `su - username` | Switch to another user |
| `sudo userdel -r name` | Delete user + home dir |
| `sudo visudo` | Edit sudoers file safely |
| `sudo groupadd name` | Create a group |
| `cat /etc/group` | View all groups |
| `sudo gpasswd -d user group` | Remove user from group |

---

## 🔐 Why This Matters in Hacking

- **`/etc/shadow` cracking:** this file contains hashed passwords — attackers who get root access dump this file and crack hashes offline using hashcat or john the ripper
- **Privilege escalation via sudo:** `sudo -l` shows what commands a user can run as root — misconfigurations here are one of the most common privesc vectors in CTFs
- **visudo misconfig:** if sudoers is misconfigured (e.g. `NOPASSWD` on a dangerous command), a low-privilege user can get root instantly
- **Adding backdoor users:** after compromising a system, attackers often create a new user with sudo access for persistence
- **`su` abuse:** if you find credentials for another user, `su` lets you switch into their account and inherit their permissions
- **Group membership:** being in the `docker` or `disk` group can give a user root-level access even without sudo — always check `groups username` during enumeration
