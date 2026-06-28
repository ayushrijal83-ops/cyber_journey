# <span style="font-size: 16px">🛰️ Python Nmap Scanner - Complete Code Explanation</span>

> <span style="font-size: 16px">A beginner-friendly explanation of a simple Python port scanner that uses </span>**<span style="font-size: 16px">Nmap</span>**<span style="font-size: 16px"> through Python's </span>`subprocess`<span style="font-size: 16px"> module.</span>

---

# <span style="font-size: 16px">📖 Introduction</span>

<span style="font-size: 16px">This project demonstrates how Python can interact with external programs installed on a Linux system.</span>

<span style="font-size: 16px">Instead of implementing a port scanner from scratch, this script acts as a </span>**<span style="font-size: 16px">wrapper</span>**<span style="font-size: 16px"> around the powerful </span>**<span style="font-size: 16px">Nmap</span>**<span style="font-size: 16px"> command-line tool. The user enters a target IP address or website, optionally specifies a port or port range, and Python executes the appropriate Nmap command.</span>

<span style="font-size: 16px">Although the project is simple, it introduces several important Python concepts that are commonly used in cybersecurity automation.</span>

---

# <span style="font-size: 16px">📂 Complete Code</span>

```python
#!/usr/bin/env python3

import subprocess
import shlex


def main():
    target = input("Enter IP address or website URL to scan: ").strip()
    if not target:
        print("No target specified.")
        return

    specific = input("Scan specific port? (y/n): ").strip().lower()
    if specific in ("y", "yes"):
        port = input("Enter port number or range (for example 80 or 1-1024): ").strip()
        if not port:
            print("No port specified.")
            return
        cmd = ["nmap", "-p", port, target]
    else:
        cmd = ["nmap", target]

    print("Running:", " ".join(shlex.quote(arg) for arg in cmd))

    try:
        result = subprocess.run(cmd, capture_output=True, text=True)
        print(result.stdout)
        if result.stderr:
            print(result.stderr)
    except FileNotFoundError:
        print("nmap is not installed or not found in PATH.")
    except Exception as err:
        print("Error executing nmap:", err)


if __name__ == "__main__":
    main()
```

---

# <span style="font-size: 16px">📌 Step 1 — The Shebang</span>

```python
#!/usr/bin/env python3
```

<span style="font-size: 16px">This line is called the </span>**<span style="font-size: 16px">Shebang</span>**<span style="font-size: 16px">.</span>

<span style="font-size: 16px">It tells Linux which interpreter should execute the file.</span>

<span style="font-size: 16px">When you run</span>

```bash
./scanner.py
```

<span style="font-size: 16px">Linux automatically executes</span>

```bash
python3 scanner.py
```

<span style="font-size: 16px">without requiring you to type </span>`python3`<span style="font-size: 16px"> manually.</span>

---

# <span style="font-size: 16px">📌 Step 2 — Importing Modules</span>

```python
import subprocess
import shlex
```

<span style="font-size: 16px">Two built-in Python modules are imported.</span>

## <span style="font-size: 16px">subprocess</span>

<span style="font-size: 16px">This module allows Python to execute external programs.</span>

<span style="font-size: 16px">Example:</span>

```python
subprocess.run(["ls"])
```

<span style="font-size: 16px">Python asks Linux to execute the </span>`ls`<span style="font-size: 16px"> command.</span>

<span style="font-size: 16px">Similarly,</span>

```python
subprocess.run(["nmap"])
```

<span style="font-size: 16px">runs the Nmap program.</span>

---

## <span style="font-size: 16px">shlex</span>

`shlex`<span style="font-size: 16px"> helps safely handle shell commands.</span>

<span style="font-size: 16px">This project uses</span>

```python
shlex.quote()
```

<span style="font-size: 16px">to safely display commands.</span>

<span style="font-size: 16px">Example:</span>

```
My Folder
```

<span style="font-size: 16px">becomes</span>

```
'My Folder'
```

<span style="font-size: 16px">which prevents incorrect splitting of arguments.</span>

---

# <span style="font-size: 16px">📌 Step 3 — Creating the Main Function</span>

```python
def main():
```

<span style="font-size: 16px">A function groups related code together.</span>

<span style="font-size: 16px">Nothing inside this function runs until</span>

```python
main()
```

<span style="font-size: 16px">is called.</span>

<span style="font-size: 16px">Functions improve readability and allow code to be reused.</span>

---

# <span style="font-size: 16px">📌 Step 4 — Getting User Input</span>

```python
target = input(...).strip()
```

`input()`<span style="font-size: 16px"> waits for the user to type something.</span>

<span style="font-size: 16px">Example</span>

```
Enter IP address:

192.168.1.1
```

<span style="font-size: 16px">The value is stored inside the variable</span>

```python
target
```

---

# <span style="font-size: 16px">📌 Step 5 — Why </span>`.strip()`<span style="font-size: 16px">?</span>

`.strip()`<span style="font-size: 16px"> removes whitespace from both ends of a string.</span>

<span style="font-size: 16px">Example</span>

<span style="font-size: 16px">Before:</span>

```
"     google.com     "
```

<span style="font-size: 16px">After</span>

```python
.strip()
```

```
"google.com"
```

<span style="font-size: 16px">This prevents accidental spaces from causing errors.</span>

---

# <span style="font-size: 16px">📌 Step 6 — Checking Empty Input</span>

```python
if not target:
```

<span style="font-size: 16px">This checks whether the user entered anything.</span>

<span style="font-size: 16px">If the user simply presses </span>**<span style="font-size: 16px">Enter</span>**

```
target = ""
```

<span style="font-size: 16px">Python treats an empty string as </span>**<span style="font-size: 16px">False</span>**<span style="font-size: 16px">.</span>

<span style="font-size: 16px">Therefore,</span>

```python
if not target:
```

<span style="font-size: 16px">becomes</span>

```python
if True:
```

<span style="font-size: 16px">The program prints</span>

```
No target specified.
```

<span style="font-size: 16px">and exits.</span>

---

# <span style="font-size: 16px">📌 Step 7 — Asking Whether to Scan a Specific Port</span>

```python
specific = input(...).strip().lower()
```

<span style="font-size: 16px">The user is asked</span>

```
Scan specific port? (y/n)
```

<span style="font-size: 16px">The </span>`.lower()`<span style="font-size: 16px"> method converts everything to lowercase.</span>

<span style="font-size: 16px">Examples</span>

```
YES
Yes
yEs
Y
```

<span style="font-size: 16px">all become</span>

```
yes
```

<span style="font-size: 16px">This makes user input easier to handle.</span>

---

# <span style="font-size: 16px">📌 Step 8 — Checking the User's Choice</span>

```python
if specific in ("y", "yes"):
```

<span style="font-size: 16px">Python checks whether the user's answer matches either</span>

```
y
```

<span style="font-size: 16px">or</span>

```
yes
```

<span style="font-size: 16px">If either matches, the program asks for a port number.</span>

---

# <span style="font-size: 16px">📌 Step 9 — Reading the Port</span>

```python
port = input(...).strip()
```

<span style="font-size: 16px">Examples of valid input</span>

```
80
```

```
443
```

```
1-1024
```

<span style="font-size: 16px">The value is stored as a string because Nmap accepts ports as text.</span>

---

# <span style="font-size: 16px">📌 Step 10 — Building the Command</span>

<span style="font-size: 16px">If the user chooses a specific port</span>

```python
cmd = ["nmap", "-p", port, target]
```

<span style="font-size: 16px">Suppose</span>

```
port = 80

target = google.com
```

<span style="font-size: 16px">The list becomes</span>

```python
[
    "nmap",
    "-p",
    "80",
    "google.com"
]
```

<span style="font-size: 16px">When executed, Python runs</span>

```bash
nmap -p 80 google.com
```

---

<span style="font-size: 16px">If the user chooses a normal scan</span>

```python
cmd = ["nmap", target]
```

<span style="font-size: 16px">Python executes</span>

```bash
nmap google.com
```

---

# <span style="font-size: 16px">📌 Why Use a List Instead of a String?</span>

<span style="font-size: 16px">Instead of writing</span>

```python
command = "nmap -p 80 google.com"
```

<span style="font-size: 16px">the program creates</span>

```python
[
    "nmap",
    "-p",
    "80",
    "google.com"
]
```

<span style="font-size: 16px">This is much safer.</span>

<span style="font-size: 16px">Each item is treated as one separate argument.</span>

<span style="font-size: 16px">It also helps protect against command injection attacks and avoids problems with spaces or special characters.</span>

---

# <span style="font-size: 16px">📌 Step 11 — Displaying the Command</span>

```python
print("Running:", " ".join(shlex.quote(arg) for arg in cmd))
```

<span style="font-size: 16px">This line creates a readable version of the command.</span>

<span style="font-size: 16px">Example</span>

```
[
"nmap",
"-p",
"80",
"google.com"
]
```

<span style="font-size: 16px">becomes</span>

```
nmap -p 80 google.com
```

<span style="font-size: 16px">This is only printed for the user.</span>

<span style="font-size: 16px">The actual command executed is still the Python list.</span>

---

# <span style="font-size: 16px">📌 Step 12 — Executing Nmap</span>

```python
result = subprocess.run(
    cmd,
    capture_output=True,
    text=True
)
```

<span style="font-size: 16px">This is where Python actually launches the Nmap program.</span>

---

## <span style="font-size: 16px">capture_output=True</span>

<span style="font-size: 16px">Instead of letting Nmap print directly to the terminal, Python captures everything.</span>

<span style="font-size: 16px">The output is stored inside</span>

```python
result
```

---

## <span style="font-size: 16px">text=True</span>

<span style="font-size: 16px">Without this option, Python returns raw bytes.</span>

<span style="font-size: 16px">Example</span>

```
b'Starting Nmap...'
```

<span style="font-size: 16px">With</span>

```python
text=True
```

<span style="font-size: 16px">Python automatically converts it into a normal string</span>

```
Starting Nmap...
```

<span style="font-size: 16px">making it much easier to work with.</span>

---

# <span style="font-size: 16px">📌 Step 13 — Printing the Scan Results</span>

```python
print(result.stdout)
```

`stdout`<span style="font-size: 16px"> means</span>

**<span style="font-size: 16px">Standard Output</span>**

<span style="font-size: 16px">Everything Nmap normally prints is stored here.</span>

<span style="font-size: 16px">Example</span>

```
PORT

80/tcp open

443/tcp open
```

---

# <span style="font-size: 16px">📌 Step 14 — Printing Errors</span>

```python
if result.stderr:
```

`stderr`<span style="font-size: 16px"> means</span>

**<span style="font-size: 16px">Standard Error</span>**

<span style="font-size: 16px">If Nmap reports an error</span>

```
Failed to resolve hostname.
```

<span style="font-size: 16px">it will be displayed here.</span>

---

# <span style="font-size: 16px">📌 Step 15 — Exception Handling</span>

```python
try:
```

<span style="font-size: 16px">Python attempts to execute the code.</span>

<span style="font-size: 16px">If something unexpected happens, execution jumps to an appropriate </span>`except`<span style="font-size: 16px"> block.</span>

---

## <span style="font-size: 16px">FileNotFoundError</span>

```python
except FileNotFoundError:
```

<span style="font-size: 16px">This occurs when Nmap is not installed.</span>

<span style="font-size: 16px">Instead of crashing, the program displays</span>

```
nmap is not installed or not found in PATH.
```

---

## <span style="font-size: 16px">Generic Exceptions</span>

```python
except Exception as err:
```

<span style="font-size: 16px">This catches other unexpected runtime errors and prints the error message.</span>

---

# <span style="font-size: 16px">📌 Step 16 — Program Entry Point</span>

```python
if __name__ == "__main__":
    main()
```

<span style="font-size: 16px">This is the standard Python entry point.</span>

<span style="font-size: 16px">When the file is run directly</span>

```bash
python scanner.py
```

<span style="font-size: 16px">the </span>`main()`<span style="font-size: 16px"> function executes.</span>

<span style="font-size: 16px">If another Python program imports this file</span>

```python
import scanner
```

<span style="font-size: 16px">the code inside </span>`main()`<span style="font-size: 16px"> does </span>**<span style="font-size: 16px">not</span>**<span style="font-size: 16px"> execute automatically.</span>

<span style="font-size: 16px">This makes the file reusable.</span>

---

# <span style="font-size: 16px">🔄 Program Flow</span>

```
Start
   │
   ▼
Ask for target
   │
   ▼
Empty?
 ├── Yes → Exit
 └── No
        │
        ▼
Ask if specific port
        │
        ▼
Yes?
├── Yes
│      │
│      ▼
│ Ask for port
│      │
│ Build:
│ nmap -p PORT TARGET
│
└── No
       │
       ▼
 Build:
 nmap TARGET
       │
       ▼
Display command
       │
       ▼
Run Nmap
       │
       ▼
Capture Output
       │
       ▼
Print Results
       │
       ▼
Finish
```

---

# <span style="font-size: 16px">🧠 Python Concepts Learned</span>

- <span style="font-size: 16px">Shebang (</span>`#!/usr/bin/env python3`<span style="font-size: 16px">)</span>

- <span style="font-size: 16px">Importing modules</span>

- <span style="font-size: 16px">Functions</span>

- <span style="font-size: 16px">Variables</span>

- <span style="font-size: 16px">User input</span>

- `.strip()`

- `.lower()`

- <span style="font-size: 16px">Lists</span>

- <span style="font-size: 16px">Conditional statements</span>

- <span style="font-size: 16px">Membership operator (</span>`in`<span style="font-size: 16px">)</span>

- `return`

- `subprocess.run()`

- `capture_output`

- `stdout`

- `stderr`

- <span style="font-size: 16px">Exception handling</span>

- `try`<span style="font-size: 16px"> / </span>`except`

- `if __name__ == "__main__"`

---

# <span style="font-size: 16px">🎯 What I Learned</span>

<span style="font-size: 16px">This project helped me understand how Python can interact with operating system tools such as </span>**<span style="font-size: 16px">Nmap</span>**<span style="font-size: 16px">. While the script itself is small, it introduced several important programming concepts including user input handling, command construction, safe argument passing, subprocess execution, and error handling. These skills form the foundation for building more advanced cybersecurity automation tools in the future.</span>

---

<span style="font-size: 16px">⭐ If you found this project helpful, feel free to star the repository and explore the code yourself.</span>
