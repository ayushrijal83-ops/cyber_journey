# <span style="font-size: 16px">📜 Nmap Scripting Engine (NSE) — Complete Guide</span>

> **<span style="font-size: 16px">Phase:</span>**<span style="font-size: 16px"> Networking | </span>**<span style="font-size: 16px">Topic:</span>**<span style="font-size: 16px"> 13 | </span>**<span style="font-size: 16px">Status:</span>**<span style="font-size: 16px"> ✅ Completed </span>**<span style="font-size: 16px">Source:</span>**<span style="font-size: 16px"> TryHackMe Further Nmap</span>

---

## <span style="font-size: 16px">What is NSE?</span>

<span style="font-size: 16px">The </span>**<span style="font-size: 16px">Nmap Scripting Engine (NSE)</span>**<span style="font-size: 16px"> is one of the most powerful additions to Nmap — it extends Nmap's functionality far beyond simple port scanning.</span>

- <span style="font-size: 16px">Scripts are written in the </span>**<span style="font-size: 16px">Lua programming language</span>**
- <span style="font-size: 16px">Can do everything from </span>**<span style="font-size: 16px">vulnerability scanning</span>**<span style="font-size: 16px"> to </span>**<span style="font-size: 16px">automating exploits</span>**
- <span style="font-size: 16px">Particularly useful for </span>**<span style="font-size: 16px">reconnaissance</span>**
- <span style="font-size: 16px">The script library is huge — worth bearing in mind how extensive it is</span>

---

## <span style="font-size: 16px">NSE Script Categories</span>

<table>
<tbody><tr><th colspan="1" rowspan="1"><p><span style="font-size: 16px">Category</span></p></th><th colspan="1" rowspan="1"><p><span style="font-size: 16px">Purpose</span></p></th><th colspan="1" rowspan="1"><p><span style="font-size: 16px">Safe for Target?</span></p></th></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">safe</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Won't affect the target</span></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">✅ Yes</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">intrusive</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Likely to affect the target</span></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">❌ No</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">vuln</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Scan for vulnerabilities</span></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">⚠️ Depends</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">exploit</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Attempt to exploit a vulnerability</span></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">❌ No</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">auth</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Bypass authentication (e.g. anonymous FTP login)</span></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">⚠️ Depends</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">brute</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Brute force credentials for running services</span></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">❌ No</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">discovery</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Query running services for more network info (e.g. SNMP)</span></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">✅ Mostly</span></p></td></tr></tbody>
</table>

> <span style="font-size: 16px">A more exhaustive list exists at: </span>`nmap.org/book/nse-usage.html`

---

## <span style="font-size: 16px">How to Use NSE Scripts</span>

### <span style="font-size: 16px">Run All Scripts From a Category</span>

```bash
nmap --script=vuln target_ip
nmap --script=safe target_ip
nmap --script=discovery target_ip
```

> <span style="font-size: 16px">Note: only scripts which target an </span>**<span style="font-size: 16px">active service</span>**<span style="font-size: 16px"> on the host will actually run. If port 21 (FTP) isn't open, FTP-related scripts simply won't trigger.</span>

### <span style="font-size: 16px">Run a Specific Script</span>

```bash
nmap --script=http-fileupload-exploiter target_ip
```

### <span style="font-size: 16px">Run Multiple Specific Scripts at Once</span>

<span style="font-size: 16px">Separate script names with a </span>**<span style="font-size: 16px">comma</span>**<span style="font-size: 16px">:</span>

```bash
nmap --script=smb-enum-users,smb-enum-shares target_ip
```

---

## <span style="font-size: 16px">Scripts That Need Arguments</span>

<span style="font-size: 16px">Some scripts require extra information to function — like credentials for an authenticated exploit. These are passed using </span>`--script-args`<span style="font-size: 16px">.</span>

### <span style="font-size: 16px">Syntax Rules</span>

- <span style="font-size: 16px">Arguments are separated by </span>**<span style="font-size: 16px">commas</span>**
- <span style="font-size: 16px">Each argument is connected to its script using a </span>**<span style="font-size: 16px">period</span>**<span style="font-size: 16px">:</span>

  ```
  <script-name>.<argument>
  
  ```

### <span style="font-size: 16px">Real Example — http-put Script</span>

<span style="font-size: 16px">The </span>`http-put`<span style="font-size: 16px"> script uploads a file using the HTTP PUT method. It needs:</span>

1. <span style="font-size: 16px">The URL to upload the file to</span>
2. <span style="font-size: 16px">The file's location on disk</span>

```bash
nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'
```

<span style="font-size: 16px">Breaking this down:</span>

```
--script http-put                              ← which script to run
--script-args                                   ← passing arguments
  http-put.url='/dav/shell.php'                ← argument 1: where to upload
  http-put.file='./shell.php'                  ← argument 2: local file path
```

---

## <span style="font-size: 16px">Getting Help for Scripts</span>

<span style="font-size: 16px">Every NSE script has a built-in help menu:</span>

```bash
nmap --script-help <script-name>
```

<span style="font-size: 16px">Example:</span>

```bash
nmap --script-help http-put
```

> <span style="font-size: 16px">This local help is less detailed than the official documentation but still useful when working offline or without internet access.</span>

---

## <span style="font-size: 16px">Finding Scripts — Two Methods</span>

### <span style="font-size: 16px">Method 1 — Official Nmap Website</span>

<span style="font-size: 16px">The full list of all official scripts with documentation and example use cases:</span>

```
nmap.org/nsedoc/
```

### <span style="font-size: 16px">Method 2 — Local Storage on Your Machine</span>

<span style="font-size: 16px">On Linux, all NSE scripts are stored at:</span>

```
/usr/share/nmap/scripts
```

<span style="font-size: 16px">This is the </span>**<span style="font-size: 16px">default location</span>**<span style="font-size: 16px"> Nmap looks in when you specify a script by name.</span>

---

## <span style="font-size: 16px">Searching For Installed Scripts</span>

### <span style="font-size: 16px">Method A — Using script.db</span>

<span style="font-size: 16px">Despite the </span>`.db`<span style="font-size: 16px"> extension, this is </span>**<span style="font-size: 16px">not actually a database</span>**<span style="font-size: 16px"> — it's a formatted text file containing filenames and categories for every available script.</span>

```bash
# View the file location
/usr/share/nmap/scripts/script.db
```

**<span style="font-size: 16px">Search for scripts by keyword (grep):</span>**

```bash
grep "ftp" /usr/share/nmap/scripts/script.db
```

<span style="font-size: 16px">This finds all scripts related to FTP.</span>

**<span style="font-size: 16px">Search for scripts by category:</span>**

```bash
grep "safe" /usr/share/nmap/scripts/script.db
```

<span style="font-size: 16px">This finds all scripts tagged as "safe."</span>

### <span style="font-size: 16px">Method B — Using ls Command</span>

<span style="font-size: 16px">You can also search directly using </span>`ls`<span style="font-size: 16px"> with wildcards:</span>

```bash
ls -l /usr/share/nmap/scripts/*ftp*
```

> <span style="font-size: 16px">Note the asterisks (</span>`*`<span style="font-size: 16px">) on </span>**<span style="font-size: 16px">both sides</span>**<span style="font-size: 16px"> of the search term — this finds any filename containing "ftp" anywhere in the name.</span>

---

## <span style="font-size: 16px">Installing New Scripts</span>

### <span style="font-size: 16px">Method 1 — Standard Update (Easiest)</span>

<span style="font-size: 16px">If a script is missing, the simplest fix is updating Nmap itself:</span>

```bash
sudo apt update && sudo apt install nmap
```

### <span style="font-size: 16px">Method 2 — Manual Installation</span>

<span style="font-size: 16px">You can manually download a specific script directly from Nmap's repository:</span>

```bash
sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse
```

### <span style="font-size: 16px">Critical Final Step — Update the Script Database</span>

<span style="font-size: 16px">After manually adding ANY script (downloaded or self-written), you </span>**<span style="font-size: 16px">must</span>**<span style="font-size: 16px"> run:</span>

```bash
nmap --script-updatedb
```

<span style="font-size: 16px">This updates </span>`script.db`<span style="font-size: 16px"> so Nmap actually recognizes the new script exists.</span>

> <span style="font-size: 16px">⚠️ Skipping this step means Nmap won't find your newly added script even though the file is physically present in the scripts folder.</span>

---

## <span style="font-size: 16px">Writing Your Own Scripts</span>

<span style="font-size: 16px">NSE scripts are written in </span>**<span style="font-size: 16px">Lua</span>**<span style="font-size: 16px"> — described as "a more than manageable task with some basic knowledge of Lua."</span>

```
Basic Lua knowledge → Write custom .nse script → Place in /usr/share/nmap/scripts → Run --script-updatedb → Ready to use
```

<span style="font-size: 16px">This means you can build </span>**<span style="font-size: 16px">custom reconnaissance or exploitation scripts</span>**<span style="font-size: 16px"> tailored to specific situations you encounter repeatedly.</span>

---

## <span style="font-size: 16px">Full Workflow Example — Real World Usage</span>

```bash
# Step 1: Find what FTP-related scripts are available
grep "ftp" /usr/share/nmap/scripts/script.db

# Step 2: Read what a specific script does
nmap --script-help ftp-anon

# Step 3: Run it against your target
nmap -p 21 --script=ftp-anon target_ip

# Step 4: If it needs arguments, check nsedoc and pass them
nmap -p 21 --script=ftp-brute --script-args userdb=users.txt,passdb=pass.txt target_ip
```

---

## <span style="font-size: 16px">Quick Reference — Commands Cheat Sheet</span>

<table>
<tbody><tr><th colspan="1" rowspan="1"><p><span style="font-size: 16px">Command</span></p></th><th colspan="1" rowspan="1"><p><span style="font-size: 16px">What it does</span></p></th></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">nmap --script=vuln target</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Run all vulnerability scripts</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">nmap --script=safe target</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Run all safe scripts</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">nmap --script=script-name target</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Run one specific script</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">nmap --script=script1,script2 target</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Run multiple specific scripts</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">nmap --script-args arg=value target</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Pass arguments to a script</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">nmap --script-help script-name</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Show built-in help for a script</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">grep "keyword" /usr/share/nmap/scripts/script.db</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Search scripts by keyword</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">ls -l /usr/share/nmap/scripts/*keyword*</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Search scripts by filename</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">sudo apt update &amp;&amp; sudo apt install nmap</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Update Nmap + refresh script library</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">sudo wget -O /usr/share/nmap/scripts/name.nse URL</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Manually download a script</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">nmap --script-updatedb</code></p></td><td colspan="1" rowspan="1"><p><span style="font-size: 16px">Refresh script database after adding new scripts</span></p></td></tr></tbody>
</table>

---

## <span style="font-size: 16px">Quick Reference — Category Cheat Sheet</span>

```
safe        → Information gathering, won't touch the target
intrusive   → Might affect target — use with caution
vuln        → Checks for known vulnerabilities
exploit     → Actually attempts to exploit found vulnerabilities
auth        → Tests for authentication bypasses (anonymous logins etc)
brute       → Brute forces usernames/passwords
discovery   → Gathers extra info from running services (SNMP, etc)
```

---

## <span style="font-size: 16px">🔐 Why This Matters in Hacking</span>

- `--script=vuln`<span style="font-size: 16px"> is gold: automatically checks for known CVEs across every detected service — finds things like EternalBlue, Heartbleed automatically without manual research</span>
- `--script=auth`<span style="font-size: 16px"> for quick wins: checking for anonymous FTP/SMB access is one of the fastest ways to get initial access in CTFs — often the very first thing to try</span>
- `--script=brute`<span style="font-size: 16px"> for credential attacks: automates username/password attacks against services like FTP, SSH, and HTTP without needing separate tools</span>
- **<span style="font-size: 16px">Custom scripts = custom recon:</span>**<span style="font-size: 16px"> writing your own NSE script in Lua means you can automate repetitive recon tasks specific to your engagements</span>
- **<span style="font-size: 16px">script.db searching:</span>**<span style="font-size: 16px"> when you don't know the exact script name, grep-ing script.db by service name (ftp, smb, http) quickly surfaces all relevant options</span>
- **<span style="font-size: 16px">discovery scripts for network mapping:</span>**<span style="font-size: 16px"> scripts like SNMP enumeration can reveal entire network topology, usernames, and configuration details</span>
- **<span style="font-size: 16px">Real world example — http-put:</span>**<span style="font-size: 16px"> the http-put script with arguments is literally how you'd upload a web shell to a vulnerable WebDAV server — a real exploitation technique, not just theory</span>
- **<span style="font-size: 16px">Local scripts directory:</span>**<span style="font-size: 16px"> knowing </span>`/usr/share/nmap/scripts`<span style="font-size: 16px"> exists means during a CTF you can quickly browse what's available without needing internet access to nmap.org</span>