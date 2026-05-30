# ⚡ Linux Terminal Hacks — Hack Faster!

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## Why Terminal Hacks Matter

Speed in the terminal = speed in hacking.  
These tricks save time, reduce mistakes, and make you look like a pro. 😄

---

## ⌨️ Keyboard Shortcuts — Use These Every Day

| Shortcut | What it does |
|---|---|
| `Ctrl + C` | Kill/stop the current running process |
| `Ctrl + Z` | Suspend current process (send to background) |
| `Ctrl + L` | Clear the terminal screen (same as `clear`) |
| `Ctrl + A` | Jump to beginning of line |
| `Ctrl + E` | Jump to end of line |
| `Ctrl + U` | Delete everything before cursor |
| `Ctrl + K` | Delete everything after cursor |
| `Ctrl + W` | Delete the word before cursor |
| `Ctrl + R` | Reverse search through command history |
| `Ctrl + Shift + C` | Copy in terminal |
| `Ctrl + Shift + V` | Paste in terminal |
| `Tab` | Autocomplete command or filename |
| `Tab Tab` | Show all possible completions |
| `↑ ↓` | Navigate through command history |

---

## 🔁 Command History Tricks

### View Full History
```bash
history
```

### Search History (Most Useful Trick)
Press `Ctrl + R` then start typing — it finds matching past commands instantly.

```bash
# Example: press Ctrl+R then type "nmap"
# It finds your last nmap command automatically
```

### Run Last Command Again
```bash
!!
```

### Run Last Command with sudo (Game Changer)
```bash
sudo !!
```

Forgot to type sudo? Just run `sudo !!` — reruns the previous command with sudo. Saves so much time!

### Run Command from History by Number
```bash
!42    # runs command number 42 from history
```

### Clear History
```bash
history -c
cat /dev/null > ~/.bash_history
```

---

## 🚀 Navigation Tricks

### Jump to Home Directory
```bash
cd ~
cd      # just cd alone also works
```

### Go Back to Previous Directory
```bash
cd -
```

Instantly switches back to wherever you just were — great when jumping between folders.

### Go Up Multiple Directories
```bash
cd ../..      # up 2 levels
cd ../../..   # up 3 levels
```

---

## ✂️ Aliases — Create Your Own Shortcuts

Aliases let you create short custom commands for long ones.

```bash
# Add to ~/.bashrc for permanent aliases
alias update='sudo apt update && sudo apt upgrade'
alias ll='ls -la'
alias cls='clear'
alias myip='curl ifconfig.me'
alias ports='netstat -tulnp'
alias scan='nmap -sV'
```

### Apply Changes Immediately
```bash
source ~/.bashrc
```

Now typing `update` runs the full apt update + upgrade automatically!

---

## 📋 Copy Output Directly to Clipboard

```bash
# Install xclip first
sudo apt install xclip

# Copy command output to clipboard
cat file.txt | xclip -selection clipboard

# Copy IP address directly
ifconfig | grep inet | xclip -selection clipboard
```

---

## 🔀 Running Multiple Commands

```bash
# Run command2 only if command1 succeeds
command1 && command2

# Run command2 only if command1 fails
command1 || command2

# Run both regardless
command1 ; command2

# Example — update then upgrade
sudo apt update && sudo apt upgrade

# Example — scan and save results
nmap -sV target && echo "Scan Complete"
```

---

## 📁 Quick File Tricks

### Create Multiple Files at Once
```bash
touch file1.txt file2.txt file3.txt
```

### Create Nested Directories at Once
```bash
mkdir -p folder1/folder2/folder3
```

### View File Without Scrolling Issues
```bash
less filename.txt    # press q to quit
```

### View Last 20 Lines of a File
```bash
tail -20 filename.txt
```

### Watch a File Update in Real Time
```bash
tail -f /var/log/apache2/access.log
```

---

## 🖥️ Terminal Multiplexer — tmux

`tmux` lets you have multiple terminal windows in one — essential for hacking.

```bash
# Install tmux
sudo apt install tmux

# Start tmux
tmux

# Key shortcuts inside tmux:
# Ctrl+B then C    → create new window
# Ctrl+B then N    → next window
# Ctrl+B then P    → previous window
# Ctrl+B then %    → split vertically
# Ctrl+B then "    → split horizontally
# Ctrl+B then D    → detach session
# Ctrl+B then ?    → help/all shortcuts

# Reattach to session
tmux attach
```

---

## 🔍 Miscellaneous Power Tricks

### Repeat a Command Every 2 Seconds
```bash
watch -n 2 command
# Example: watch -n 2 netstat -tulnp
```

### Run Command in Background
```bash
command &
```

### Time How Long a Command Takes
```bash
time nmap -sV target
```

### Output to File AND See it on Screen
```bash
nmap -sV target | tee results.txt
```

### Find and Replace in a File
```bash
sed -i 's/old_text/new_text/g' filename.txt
```

### Download a File Quickly
```bash
wget https://example.com/file.zip
curl -O https://example.com/file.zip
```

---

## Quick Reference — The Most Used Ones

| Trick | Command |
|---|---|
| Forgot sudo? | `sudo !!` |
| Search history | `Ctrl + R` |
| Clear screen | `Ctrl + L` |
| Go back to last dir | `cd -` |
| Run two commands | `cmd1 && cmd2` |
| Background process | `command &` |
| Watch live updates | `tail -f file` |
| Save + see output | `command \| tee file.txt` |
| Custom shortcut | `alias short='long command'` |

---

## 🔐 Why This Matters in Hacking

- **`sudo !!`** — you'll forget sudo constantly, this saves time every single session
- **`Ctrl + R`** — finding that long nmap command you ran 20 minutes ago instantly
- **`tail -f`** — watching logs update live during an attack or CTF challenge
- **`tee`** — saves scan output to file while still seeing it on screen — essential for documentation
- **`tmux`** — run multiple tools simultaneously in one terminal — nmap in one pane, gobuster in another, netcat listener in a third
- **`&&` chaining** — automate attack sequences: scan → enumerate → exploit
- **Aliases** — `alias scan='nmap -sV -sC'` means you type `scan target` instead of the full command every time
- **`history -c`** — clearing command history is part of covering tracks after a pentest
