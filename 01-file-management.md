# 📁 File Management & Manipulation

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## ECHO Command — Writing to Files

The `echo` command can write text directly into a file.

```bash
echo "text you want to write" > filename.txt
```

- `>` redirects the output into the file
- If the file **doesn't exist**, it gets created automatically
- If the file **already exists**, it gets **overwritten**

> ⚠️ Use `>>` instead of `>` if you want to **append** without overwriting:
```bash
echo "new line" >> filename.txt
```

---

## CAT Command — Redirecting File Contents

You can redirect the contents of any file into a new file using `cat`:

```bash
cat /etc/network > redirect.txt
```

- Reads the contents of `/etc/network`
- Redirects everything into `redirect.txt`
- If `redirect.txt` doesn't exist, it creates it automatically

---

## Creating Directories

```bash
mkdir directory_name
```

---

## Deleting Files & Folders

```bash
# Delete a file
rm filename.txt

# Delete a folder (recursively — deletes everything inside too)
rm -R folder_name
```

> ⚠️ **Be careful with `rm -R`** — there is no recycle bin in Linux. It's gone permanently.

---

## Copying Files

```bash
cp file_to_copy destination_location
```

**Example:**
```bash
cp notes.txt /home/user/backup/notes.txt
```

---

## Moving / Renaming Files

```bash
mv file_name destination_or_new_name
```

**Example — move:**
```bash
mv notes.txt /tmp/notes.txt
```

**Example — rename:**
```bash
mv oldname.txt newname.txt
```

---

## Quick Reference Table

| Command | What it does |
|---|---|
| `echo "text" > file.txt` | Write text to a file |
| `echo "text" >> file.txt` | Append text to a file |
| `cat file > newfile.txt` | Copy file contents to new file |
| `mkdir folder` | Create a new directory |
| `rm file.txt` | Delete a file |
| `rm -R folder` | Delete a folder and everything in it |
| `cp file destination` | Copy a file |
| `mv file destination` | Move or rename a file |

---

## 🔐 Why This Matters in Hacking

- **Log manipulation** — attackers use `echo` and `>` to clear or overwrite log files
- **File redirection** — used constantly when saving Nmap scan results: `nmap -sV target > results.txt`
- **`rm -R`** — used in post-exploitation to delete tools and cover tracks
