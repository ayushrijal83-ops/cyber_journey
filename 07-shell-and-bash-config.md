# 🐚 Shell & Bash Configuration

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is a Shell?

A shell is the **interface between you and the Linux system** — it's what interprets the commands you type.  
Linux has multiple shells available. Common ones:

| Shell | Description |
|---|---|
| `bash` | Default on most Linux systems — Bourne Again Shell |
| `sh` | Original Unix shell — minimal and basic |
| `fish` | Modern shell with auto-suggestions and colors |
| `zsh` | Popular with hackers — highly customizable |

---

## See All Available Shells

```bash
cat /etc/shells
```

This prints all shells installed on your system. `/etc` is where Linux stores all system configuration files.

---

## Check Which Shell You're Currently Using

```bash
echo $SHELL
```

`$SHELL` is an **environment variable** — it stores the path of your current shell.  
Example output: `/usr/bin/bash`

---

## Switch Shell Temporarily

Just type the shell name — this only lasts for the current session:

```bash
bash
fish
sh
```

When you close the terminal it goes back to your default.

---

## Switch Shell Permanently (chsh)

`chsh` stands for **change shell** — it changes your login shell permanently.

```bash
# First find where the shell is located
cat /etc/shells

# Then change to it
chsh -s /bin/bash
```

The `-s` flag specifies which shell to set for your user.  
You need to **log out and back in** for the change to take effect.

---

## View Bash Configuration Files

```bash
ls -alps | grep .bash
```

What this does:
- `ls -alps` → lists all files including hidden ones with details
- `| grep .bash` → filters only files with `.bash` in the name

You'll see files like:

| File | Purpose |
|---|---|
| `.bashrc` | Runs every time you open a new terminal |
| `.bash_profile` | Runs when you log in |
| `.bash_history` | Stores your command history |
| `.bash_logout` | Runs when you log out |

---

## Bash History

Every command you type is saved in `.bash_history`. You can use this to review past commands:

```bash
# View your command history
cat ~/.bash_history

# Or just use the history command
history

# Search through history
history | grep nmap
```

---

## /dev/null — The Black Hole

`/dev/null` is a special file in Linux — **anything redirected here is permanently deleted.**  
It's like a trash can that empties itself instantly.

```bash
# Clear your bash history completely
cat /dev/null > ~/.bash_history

# Suppress error messages in any command
command 2>/dev/null
```

**What `cat /dev/null > ~/.bash_history` does step by step:**
1. `cat /dev/null` → reads nothing (the file is always empty)
2. `>` → redirects that nothing into `.bash_history`
3. Result → `.bash_history` is now completely empty

---

## Customize Your Bash (Aliases)

You can add shortcuts to `.bashrc` to make your workflow faster:

```bash
# Open .bashrc
nano ~/.bashrc

# Add aliases at the bottom
alias ll='ls -la'
alias cls='clear'
alias myip='curl ifconfig.me'

# Save and apply changes
source ~/.bashrc
```

Now typing `ll` does `ls -la` automatically.

---

## Quick Reference

| Command | What it does |
|---|---|
| `cat /etc/shells` | List all installed shells |
| `echo $SHELL` | Show current shell |
| `chsh -s /bin/bash` | Permanently change shell |
| `ls -alps \| grep .bash` | Show all bash config files |
| `cat ~/.bash_history` | View command history |
| `history \| grep cmd` | Search command history |
| `cat /dev/null > ~/.bash_history` | Clear bash history |
| `source ~/.bashrc` | Reload bash config |

---

## 🔐 Why This Matters in Hacking

- **Clearing tracks:** `cat /dev/null > ~/.bash_history` is used by attackers after compromising a system to erase evidence of what commands they ran
- **History mining:** when you first land on a machine, `cat ~/.bash_history` can reveal passwords, SSH commands, and sensitive operations the user ran before
- **Aliases in `.bashrc`:** malware sometimes hides in `.bashrc` as aliases — e.g. aliasing `ls` to also run a malicious script
- **`/dev/null`** is used constantly in CTFs and scripts to suppress noisy error output: `find / -perm -4000 2>/dev/null`
