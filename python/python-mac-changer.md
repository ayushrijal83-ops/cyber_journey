<span style="font-size: 16px"># 🕵️ Python MAC Address Changer</span>

<span style="font-size: 16px">A Python script to automatically change your network interface's MAC address, enhancing your privacy and anonymity on local networks.</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## 📖 Table of Contents</span>

<span style="font-size: 16px">1. \[Introduction\](#introduction)</span>

<span style="font-size: 16px">2. \[Understanding MAC Addresses\](#understanding-mac-addresses)</span>

<span style="font-size: 16px">3. \[Why Change Your MAC Address?\](#why-change-your-mac-address)</span>

<span style="font-size: 16px">4. \[The Python Script\](#the-python-script)</span>

<span style="font-size: 16px">5. \[Code Explanation\](#code-explanation)</span>

<span style="font-size: 16px">6. \[How to Run the Script\](#how-to-run-the-script)</span>

<span style="font-size: 16px">7. \[Dependencies & Installation\](#dependencies--installation)</span>

<span style="font-size: 16px">8. \[Potential Improvements\](#potential-improvements)</span>

<span style="font-size: 16px">9. \[Ethical Considerations\](#ethical-considerations)</span>

<span style="font-size: 16px">10. \[Conclusion\](#conclusion)</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## Introduction</span>

<span style="font-size: 16px">In the world of networking and cybersecurity, your MAC (Media Access Control) address is a unique identifier assigned to your network interface. It operates at Layer 2 of the OSI model and can be used to track your device on local networks. While the </span>**<span style="font-size: 16px">physical</span>**<span style="font-size: 16px"> MAC address is burned into the hardware and cannot be changed permanently, we can </span>**<span style="font-size: 16px">spoof</span>**<span style="font-size: 16px"> it – that is, change the visible MAC address that the OS reports to the network. This script automates the spoofing process using Python, making it easy to rotate your MAC address periodically.</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## Understanding MAC Addresses</span>

<span style="font-size: 16px">- </span>**<span style="font-size: 16px">MAC Address</span>**<span style="font-size: 16px">: A 48‑bit hexadecimal number, typically written as </span>`XX:XX:XX:XX:XX:XX`<span style="font-size: 16px">.</span>

<span style="font-size: 16px">- It is assigned by the manufacturer and is unique to each network interface card (NIC).</span>

<span style="font-size: 16px">- It is used for communication within a local network segment (e.g., Ethernet, Wi‑Fi).</span>

<span style="font-size: 16px">- </span>**<span style="font-size: 16px">Permanent vs. Spoofed</span>**<span style="font-size: 16px">: The hardware MAC is fixed, but most operating systems allow you to override it with a software‑defined value.</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## Why Change Your MAC Address?</span>

<span style="font-size: 16px">- </span>**<span style="font-size: 16px">Privacy</span>**<span style="font-size: 16px">: Prevent tracking by network administrators, advertisers, or malicious actors.</span>

<span style="font-size: 16px">- </span>**<span style="font-size: 16px">Anonymity</span>**<span style="font-size: 16px">: Avoid being identified on public Wi‑Fi hotspots.</span>

<span style="font-size: 16px">- </span>**<span style="font-size: 16px">Bypass MAC filtering</span>**<span style="font-size: 16px">: Some networks restrict access based on MAC addresses; changing yours may allow access (though this is not always ethical).</span>

<span style="font-size: 16px">- </span>**<span style="font-size: 16px">Testing</span>**<span style="font-size: 16px">: Useful for penetration testing and network troubleshooting.</span>

<span style="font-size: 16px">&gt; ⚠️ </span>**<span style="font-size: 16px">Important</span>**<span style="font-size: 16px">: Changing your MAC address can cause network disruptions (e.g., loss of connection) and may be illegal or against terms of service in some jurisdictions. Always use responsibly.</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## The Python Script</span>

<span style="font-size: 16px">The full script is shown below. It uses </span>`macchanger`<span style="font-size: 16px"> (a Linux tool) to change the MAC address of the </span>`eth0`<span style="font-size: 16px"> interface in an infinite loop, waiting 3 seconds between changes.</span>

<span style="font-size: 16px">\`\`\`python</span>

```python
import os

import random as rn

import subprocess as sb

import time

# Check if the script is run with root privileges

if os.geteuid() != 0:

    print("This script must be run as root. Use sudo to start it.")

    raise SystemExit(1)

while True:

    # Generate a random MAC address

    mac = ":".join("%02x" % rn.randint(0, 255) for _ in range(6))

    # Execute the macchanger command

    sb.run(["macchanger", "-m", mac, "eth0"])

    print(f"MAC address changed to {mac}")

    time.sleep(3)
```

## <span style="font-size: 16px">Code Explanation</span>

<span style="font-size: 16px">Let’s break down what each part does.</span>

### <span style="font-size: 16px">1. Importing Modules</span>

- `os`<span style="font-size: 16px"> – Used to check the effective user ID (</span>`os.geteuid()`<span style="font-size: 16px">) to ensure the script runs with root privileges (required to change network settings).</span>

- `random`<span style="font-size: 16px"> – Generates random bytes to form a new MAC address.</span>

- `subprocess`<span style="font-size: 16px"> – Allows Python to execute system commands (here, calling </span>`macchanger`<span style="font-size: 16px">).</span>

- `time`<span style="font-size: 16px"> – Provides </span>`sleep()`<span style="font-size: 16px"> to pause execution between changes.</span>

### <span style="font-size: 16px">2. Root Privilege Check</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
if os.geteuid() != 0:
    print("This script must be run as root. Use sudo to start it.")
    raise SystemExit(1)
```

- `geteuid()`<span style="font-size: 16px"> returns the effective user ID. Root has UID 0. If not root, the script exits with an error message.</span>

### <span style="font-size: 16px">3. Infinite Loop</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
while True:
    ...
```

- <span style="font-size: 16px">The script will run forever until manually stopped (e.g., with </span>`Ctrl+C`<span style="font-size: 16px">). Each iteration generates a new MAC and applies it.</span>

### <span style="font-size: 16px">4. Generating a Random MAC</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
mac = ":".join("%02x" % rn.randint(0, 255) for _ in range(6))
```

- <span style="font-size: 16px">Creates a list of 6 random integers between 0 and 255, formats each as a two‑digit hexadecimal string, and joins them with colons.</span>

- <span style="font-size: 16px">This produces a valid MAC address like </span>`a1:b2:c3:d4:e5:f6`<span style="font-size: 16px">.</span>

### <span style="font-size: 16px">5. Running </span>`macchanger`

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
sb.run(["macchanger", "-m", mac, "eth0"])
```

- `subprocess.run()`<span style="font-size: 16px"> executes the command in the terminal.</span>

- `macchanger -m NEW_MAC INTERFACE`<span style="font-size: 16px"> sets the MAC address of the given interface (here </span>`eth0`<span style="font-size: 16px">).</span>

- **<span style="font-size: 16px">Note</span>**<span style="font-size: 16px">: The original code had a space between </span>`-`<span style="font-size: 16px"> and </span>`m`<span style="font-size: 16px"> (</span>`"- m"`<span style="font-size: 16px">). This is a syntax error; it should be </span>`"-m"`<span style="font-size: 16px"> (no space). The corrected version is shown above.</span>

### <span style="font-size: 16px">6. Confirmation and Sleep</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
print(f"MAC address changed to {mac}")
time.sleep(3)
```

- <span style="font-size: 16px">Prints the new MAC for user feedback.</span>

- <span style="font-size: 16px">Pauses for 3 seconds before generating the next random MAC.</span>

---

## <span style="font-size: 16px">How to Run the Script</span>

1. **<span style="font-size: 16px">Save</span>**<span style="font-size: 16px"> the script as </span>`mac_changer.py`<span style="font-size: 16px">.</span>

2. **<span style="font-size: 16px">Make it executable</span>**<span style="font-size: 16px"> (optional):</span>

   <span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">bash</span>

   ```
   chmod +x mac_changer.py
   ```

3. **<span style="font-size: 16px">Run with sudo</span>**<span style="font-size: 16px">:</span>

   <span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">bash</span>

   ```
   sudo python3 mac_changer.py
   ```

   <span style="font-size: 16px">or</span>

   <span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">bash</span>

   ```
   sudo ./mac_changer.py
   ```

4. **<span style="font-size: 16px">Stop</span>**<span style="font-size: 16px"> the script by pressing </span>`Ctrl+C`<span style="font-size: 16px">.</span>

> **<span style="font-size: 16px">Warning</span>**<span style="font-size: 16px">: This script changes your MAC every 3 seconds. Your network connection may drop and reconnect frequently. Use it for demonstration or testing only.</span>

---

## <span style="font-size: 16px">Dependencies & Installation</span>

- **<span style="font-size: 16px">Python 3</span>**<span style="font-size: 16px"> – The script is written for Python 3.</span>

- `macchanger`<span style="font-size: 16px"> – A Linux utility that changes MAC addresses. Install it via:</span>

  <span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">bash</span>

  ```
  sudo apt install macchanger   # Debian/Ubuntu
  sudo dnf install macchanger   # Fedora
  sudo pacman -S macchanger     # Arch
  ```

<span style="font-size: 16px">The script assumes the interface is named </span>`eth0`<span style="font-size: 16px">. If you use Wi‑Fi (e.g., </span>`wlan0`<span style="font-size: 16px">), modify the script accordingly.</span>

---

## <span style="font-size: 16px">Potential Improvements</span>

<span style="font-size: 16px">The current script works but can be enhanced:</span>

1. **<span style="font-size: 16px">Interface Selection</span>**<span style="font-size: 16px"> – Accept the interface name as a command‑line argument or detect it automatically.</span>

2. **<span style="font-size: 16px">Vendor‑OUI Prefix</span>**<span style="font-size: 16px"> – Generate MACs that start with a known vendor prefix to avoid suspicion (e.g., first three bytes from a real manufacturer).</span>

3. **<span style="font-size: 16px">Error Handling</span>**<span style="font-size: 16px"> – Check if </span>`macchanger`<span style="font-size: 16px"> is installed; verify that the change succeeded.</span>

4. **<span style="font-size: 16px">Random Interval</span>**<span style="font-size: 16px"> – Instead of a fixed 3‑second sleep, randomize the interval.</span>

5. **<span style="font-size: 16px">Restore Original MAC on Exit</span>**<span style="font-size: 16px"> – Save the original MAC and restore it when the script exits (using </span>`atexit`<span style="font-size: 16px">).</span>

6. **<span style="font-size: 16px">Logging</span>**<span style="font-size: 16px"> – Write changes to a log file for auditing.</span>

<span style="font-size: 16px">Here’s a more robust version (conceptual):</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
import os, random, subprocess, time, sys, atexit

# ... function to get original MAC, restore it, etc.
```

---

## <span style="font-size: 16px">Ethical Considerations</span>

- **<span style="font-size: 16px">Authorization</span>**<span style="font-size: 16px">: Only change MAC addresses on networks you own or have explicit permission to test.</span>

- **<span style="font-size: 16px">Legal</span>**<span style="font-size: 16px">: In some countries, MAC spoofing may be prohibited or considered a violation of computer misuse laws.</span>

- **<span style="font-size: 16px">Network Policies</span>**<span style="font-size: 16px">: Many public Wi‑Fi providers monitor MAC addresses for authentication; spoofing may violate their terms of service.</span>

- **<span style="font-size: 16px">Use Responsibly</span>**<span style="font-size: 16px">: This script is for educational purposes and ethical hacking. Do not use it for malicious activities.</span>

---

## <span style="font-size: 16px">Conclusion</span>

<span style="font-size: 16px">This Python MAC changer demonstrates how easy it is to automate network‑level privacy enhancements. By combining the </span>`macchanger`<span style="font-size: 16px"> tool with Python’s subprocess and random modules, you can rotate your MAC address periodically, making it more difficult to track your device.</span>

<span style="font-size: 16px">Remember, while this script changes the </span>**<span style="font-size: 16px">visible</span>**<span style="font-size: 16px"> MAC address, your hardware’s permanent MAC remains unchanged. Use this knowledge to strengthen your understanding of network security and to protect your privacy, but always stay within legal and ethical boundaries.</span>