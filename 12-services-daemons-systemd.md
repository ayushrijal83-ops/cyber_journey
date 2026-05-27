# ⚙️ Services, Daemons & systemd

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is a Daemon?

In Linux, **daemons = processes/services** running in the background.  
Think of it like Windows Task Manager processes — but in Linux they are called daemons.

| Windows | Linux |
|---|---|
| Process | Daemon |
| Task Manager | ps / systemctl |
| Services | Daemons / Units |

> 💡 **Easy way to identify a daemon:** they always end with the letter `d`  
> `ssh` → `sshd` | `apache` → `apache2` | `cron` → `crond`

---

## systemd — The Master Daemon

`systemd` is the **first process that runs when Linux boots up.**  
It manages all other daemons on the system — starting, stopping, and monitoring them.

- systemd's PID (Process ID) is always **1**
- All other daemons are called **units** in systemd
- So: **daemons = units** in systemd language

### View the Full Process Tree

```bash
pstree
```

Shows all processes in a tree — systemd sits at the very top as PID 1.

---

## Viewing Processes / Daemons

### See ALL Running Processes

```bash
sudo ps -aux
```

Shows every process running on your system with:
- User who owns it
- PID (Process ID)
- CPU and memory usage
- Command that started it

### Find a Specific Daemon

```bash
ps -aux | grep sshd
```

Uses pipe + grep to filter — only shows the SSH daemon.  
Replace `sshd` with any daemon name you're looking for.

### View Process Tree

```bash
pstree
```

---

## systemctl — Daemon Controller

`systemctl` is the command used to control all daemons through systemd.

### Start a Daemon

```bash
sudo systemctl start sshd
```

### Stop a Daemon

```bash
sudo systemctl stop sshd
```

### Restart a Daemon

```bash
sudo systemctl restart sshd
```

Stops then starts the daemon — useful after config changes.

### Reload a Daemon

```bash
sudo systemctl reload sshd
```

Reloads config files without fully stopping the daemon — less disruptive than restart.

### Reload OR Restart (Smart Command)

```bash
sudo systemctl reload-or-restart sshd
```

Checks if the daemon supports reload — if yes it reloads, if no it restarts.  
Best command to use when you're not sure which to use.

### Check Status

```bash
sudo systemctl status sshd
```

Shows whether the daemon is active, inactive, or failed — plus recent log output.

### Check if Active

```bash
sudo systemctl is-active sshd
```

Returns simply `active` or `inactive`.

### Enable a Daemon (Auto-start on Boot)

```bash
sudo systemctl enable sshd
```

Daemon will automatically start every time the system boots.

### Disable a Daemon (Don't Auto-start)

```bash
sudo systemctl disable sshd
```

Daemon won't start on boot — but you can still start it manually.

---

## Listing Daemons / Units

### List ALL Units (Daemons)

```bash
sudo systemctl list-units
```

Shows every unit running on the system.

### List Only Services

```bash
sudo systemctl list-units -t service
```

`-t service` filters to show only service-type units — cleaner output.

### List All Installed Units (Including Inactive)

```bash
sudo systemctl list-units --all
```

---

## start vs enable — What's the Difference?

| Command | What it does |
|---|---|
| `systemctl start` | Starts daemon **right now** — doesn't survive reboot |
| `systemctl enable` | Makes daemon **auto-start on every boot** |
| `systemctl enable --now` | Does both at the same time |

```bash
# Start AND enable in one command
sudo systemctl enable --now sshd
```

---

## Full systemctl Reference

| Command | What it does |
|---|---|
| `systemctl start name` | Start a daemon |
| `systemctl stop name` | Stop a daemon |
| `systemctl restart name` | Stop then start |
| `systemctl reload name` | Reload config without stopping |
| `systemctl reload-or-restart name` | Smart reload or restart |
| `systemctl status name` | Show status + recent logs |
| `systemctl is-active name` | Check if active |
| `systemctl enable name` | Auto-start on boot |
| `systemctl disable name` | Don't auto-start on boot |
| `systemctl enable --now name` | Enable + start immediately |
| `systemctl list-units` | List all running units |
| `systemctl list-units -t service` | List only services |
| `systemctl list-units --all` | List all including inactive |
| `ps -aux` | Show all running processes |
| `ps -aux \| grep name` | Find specific daemon |
| `pstree` | View process tree |

---

## 🔐 Why This Matters in Hacking

- **Service enumeration:** `systemctl list-units -t service` shows every running service on a compromised machine — reveals attack surface
- **Starting services for attacks:** `systemctl start ssh` starts SSH on a target so you can connect remotely
- **Persistence:** attackers use `systemctl enable malware.service` to make malicious services auto-start on every reboot
- **Disabling defenses:** disabling security services like firewalls (`systemctl stop ufw`) is a common post-exploitation step
- **ps -aux in CTFs:** finding unusual processes running with elevated privileges is a common privilege escalation path
- **PID 1 significance:** in Docker containers, PID 1 is NOT systemd — this is important for container escape techniques
- **Daemon hunting:** `ps -aux | grep` is used constantly during post-exploitation to find running services that might be exploitable
