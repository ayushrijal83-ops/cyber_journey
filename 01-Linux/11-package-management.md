# 📦 Package Management — apt, dpkg, git, Python & pip

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is a Package?

In Linux, **packages = software/apps.**  
Just like Windows has `.exe` installers, Linux has package managers that handle everything automatically — downloading, installing, and removing software through the terminal.

---

## Package Managers Covered

| Tool | What it is |
|---|---|
| `dpkg` | Low level — installs `.deb` files manually |
| `apt` | High level — installs from internet automatically |
| `aptitude` | GUI version of apt |
| `git` | Downloads code from GitHub |
| `pip3` | Installs Python packages |

---

## dpkg — Basic Package Manager

`dpkg` is the low level package manager for Debian-based systems.  
It installs `.deb` files that you download manually.

> ⚠️ **Limitation:** dpkg does NOT automatically install dependencies — it will often fail because of missing required packages. That's why we prefer `apt`.

### Install a .deb File

```bash
dpkg -i packagename.deb
```

- `-i` = install
- You must already have the `.deb` file downloaded

### Remove a Package

```bash
dpkg -r packagename
```

### List All Installed Packages

```bash
dpkg -l
```

### Check if Specific Package is Installed

```bash
dpkg -l | grep packagename
```

---

## apt — The Main Package Manager

`apt` is the upgraded version of dpkg.  
**Two biggest advantages:**
- You don't need to download any file — just give the package name
- It automatically installs all required dependencies

### How apt Works

apt downloads packages from **OS repositories** (repos) — official servers that store trusted software.  
To see or edit which repos you're using:

```bash
sudo apt edit-sources
```

This opens the sources list where you can add or change repositories.

### Update Package List

```bash
sudo apt update
```

> Always run this before installing anything — it refreshes the list of available packages from the repos.

### Upgrade All Installed Packages

```bash
sudo apt upgrade
```

Updates all installed software to the latest versions.

### Install a Package

```bash
sudo apt install packageName
```

**Real examples:**
```bash
sudo apt install nmap
sudo apt install git
sudo apt install python3
sudo apt install netcat
```

### Show Package Info

```bash
sudo apt show packageName
```

Shows details about a package — version, size, description, dependencies.

### Search for a Package

```bash
sudo apt search packageName
```

Find a package by name or keyword.

### List All Installed Packages

```bash
apt list --installed
```

Shows everything currently installed on your system.

### Remove a Package

```bash
sudo apt remove packageName
```

> ⚠️ Removes the package but **keeps its config files and data.**

### Remove Package + All Data (100% Clean)

```bash
sudo apt purge packageName
```

Removes the package AND all its config files — complete removal.

### Clean Up Unused Packages

```bash
sudo apt autoremove
```

Removes packages that were installed as dependencies but are no longer needed.

### GUI Version of apt

```bash
sudo aptitude
```

Opens a terminal-based graphical interface for managing packages — good for browsing available software visually.

---

## apt remove vs apt purge

| Command | What it removes |
|---|---|
| `apt remove` | Package only — config files stay |
| `apt purge` | Package + all config files and data |

Use `purge` when you want a completely clean uninstall.

---

## git — Download Tools from GitHub

`git` is how you download hacking tools, exploits, and scripts from GitHub.

### Install git

```bash
sudo apt install git
```

### Clone (Download) a Repository

```bash
git clone https://github.com/username/repository.git
```

**Real hacking examples:**
```bash
# Download SecLists (wordlists for CTFs)
git clone https://github.com/danielmiessler/SecLists.git

# Download LinPEAS (privilege escalation tool)
git clone https://github.com/carlospolop/PEASS-ng.git
```

### Update a Downloaded Tool

```bash
cd tool-folder
git pull
```

### Basic git Workflow for Your GitHub

```bash
git add .
git commit -m "what you changed"
git push
```

### First Time git Setup

```bash
git config --global user.name "YourName"
git config --global user.email "your@email.com"
```

---

## Python & pip — Python Package Management

Python is pre-installed on Kali. pip is Python's package manager.

### Check Python Version

```bash
python3 --version
```

### Install pip

```bash
sudo apt install python3-pip
```

### Install a Python Package

```bash
pip3 install packageName
```

**Examples:**
```bash
pip3 install requests
pip3 install scapy
pip3 install pwntools
```

### Install All Dependencies from a File

```bash
pip3 install -r requirements.txt
```

Most tools on GitHub include a `requirements.txt` — this installs everything needed in one command.

### List Installed Python Packages

```bash
pip3 list
```

### Uninstall a Package

```bash
pip3 uninstall packageName
```

---

## Full Workflow — Installing Any Hacking Tool

This is the workflow you'll use constantly throughout your journey:

```bash
# 1. Update your system
sudo apt update

# 2. Clone the tool from GitHub
git clone https://github.com/tool/repo.git

# 3. Go into the folder
cd repo

# 4. Install Python dependencies
pip3 install -r requirements.txt

# 5. Run the tool
python3 tool.py
```

---

## Quick Reference Table

| Command | What it does |
|---|---|
| `sudo apt update` | Refresh package list from repos |
| `sudo apt upgrade` | Update all installed packages |
| `sudo apt install name` | Install a package |
| `sudo apt show name` | Show package details |
| `sudo apt search name` | Search for a package |
| `apt list --installed` | List all installed packages |
| `sudo apt remove name` | Remove package (keeps config) |
| `sudo apt purge name` | Remove package + all data |
| `sudo apt autoremove` | Remove unused dependencies |
| `sudo apt edit-sources` | Edit package repositories |
| `sudo aptitude` | GUI version of apt |
| `dpkg -i file.deb` | Install a .deb file |
| `dpkg -l` | List all installed packages |
| `git clone URL` | Download a GitHub repo |
| `git pull` | Get latest updates |
| `pip3 install name` | Install Python package |
| `pip3 install -r requirements.txt` | Install all dependencies |
| `pip3 list` | List Python packages |

---

## 🔐 Why This Matters in Hacking

- **Installing tools:** every tool you use — Nmap, Metasploit, Burp Suite — gets installed via apt. This is your daily workflow
- **git clone for exploits:** when you find a CVE with a public exploit on GitHub, `git clone` gets it onto your machine instantly
- **requirements.txt:** Python-based security tools need specific libraries — pip makes sure you can run anything
- **apt purge for cleanup:** after a pentest or CTF, purge tools you no longer need to keep your system clean
- **Repo management:** adding custom repos (like exploit-db) via `edit-sources` lets you install specialist security tools not in the default Kali repos
- **dpkg for offline installs:** on air-gapped machines (no internet), dpkg lets you install `.deb` packages you transferred manually
