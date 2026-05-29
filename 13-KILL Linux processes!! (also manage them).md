# Linux Process Management Notes

## What is a Process?

A **process** is simply a running program on Linux.  
Every application you open — Firefox, VS Code, terminal, music player — runs as a process.

Linux assigns every process a unique number called a:

- **PID (Process ID)**

This PID is used to manage, monitor, or terminate processes.

---

# The `ps` Command

The `ps` command stands for:

```bash
ps
```

It is used to display currently running processes.

---

## Basic Usage

```bash
ps
```

This command shows only the processes running in your current terminal session.

Example output:

```bash
PID TTY          TIME CMD
1452 pts/0    00:00:00 bash
1731 pts/0    00:00:00 ps
```

---

# Show All Running Processes

To display more detailed information about processes:

```bash
ps aux
```

### What does `aux` mean?

- `a` → show processes from all users
- `u` → display detailed user information
- `x` → include background processes

This is one of the most commonly used Linux process commands.

---

# Show Processes of a Specific User

```bash
ps -u username
```

Example:

```bash
ps -u yami
```

This displays all processes running under the user `yami`.

---

# Finding a Specific Process

Sometimes you only want one process, not the entire list.

Example: Find Firefox process.

```bash
ps -u yami | grep firefox
```

### Breakdown

- `ps -u yami` → shows all processes of user `yami`
- `|` → sends output to another command
- `grep firefox` → filters only lines containing "firefox"

---

# Faster Method: `pgrep`

Linux already provides a shortcut command for searching processes.

```bash
pgrep firefox
```

This directly returns the PID of Firefox.

Example output:

```bash
4721
```

Much cleaner and faster than combining `ps` and `grep`.

---

# Killing Processes

To terminate a process:

```bash
kill PID
```

Example:

```bash
kill 4721
```

This sends a termination signal to the process.

---

# Force Kill a Process

Some applications ignore normal kill requests.

In that case use:

```bash
kill -9 PID
```

Example:

```bash
kill -9 4721
```

### Warning

`kill -9` forcefully stops the process immediately.  
Use it only when normal `kill` does not work.

---

# Monitor Running Processes

## Using `top`

```bash
top
```

`top` displays real-time system activity including:

- CPU usage
- RAM usage
- Running processes
- System load

It works similarly to Windows Task Manager.

---

## Using `htop`

```bash
htop
```

`htop` is an improved interactive version of `top`.

Features:

- Better UI
- Colorful display
- Keyboard navigation
- Easier process management

---

# Installing `htop`

### Debian / Ubuntu / Kali

```bash
sudo apt install htop
```

### Arch Linux

```bash
sudo pacman -S htop
```

### Fedora

```bash
sudo dnf install htop
```

---

# Foreground vs Background Processes

## Foreground Process

A process running directly in the terminal.

Example:

```bash
ping google.com
```

The terminal stays busy until the command stops.

---

## Background Process

A process running without blocking the terminal.

Run a command in background using:

```bash
command &
```

Example:

```bash
firefox &
```

---

# Managing Background Jobs

## Show Running Background Jobs

```bash
jobs
```

---

## Bring Background Job to Foreground

```bash
fg
```

---

## Send Foreground Job to Background

First suspend it:

```bash
CTRL + Z
```

Then continue it in background:

```bash
bg
```

---

# Useful Process Management Commands

| Command | Purpose |
|---|---|
| `ps` | Show current terminal processes |
| `ps aux` | Show all running processes |
| `pgrep` | Find PID of a process |
| `kill PID` | Terminate process |
| `kill -9 PID` | Force kill process |
| `top` | Real-time process monitoring |
| `htop` | Interactive process monitor |
| `jobs` | Show background jobs |
| `fg` | Bring job to foreground |
| `bg` | Continue suspended job in background |

---

# Final Notes

Learning Linux process management is important because:

- Every Linux system runs through processes
- Servers depend heavily on process control
- Cybersecurity and system administration require process monitoring
- Understanding PIDs helps in troubleshooting and automation

Mastering these commands makes Linux administration much easier.
