# 📦 File Compression & Archiving with tar

> **Phase:** Linux Basics | **Status:** ✅ Completed

---

## What is tar?

`tar` is the main tool in Linux for **compressing and archiving** files and folders through the command line.  
Two formats covered:

| Format | Description |
|---|---|
| `.tar` | Archive only — bundles files together but doesn't compress |
| `.tar.gz` | Archive + compressed — smaller file size |

---

## tar Flags — Know These by Heart

| Flag | Meaning |
|---|---|
| `-c` | Create — compress/archive the file |
| `-x` | Extract — unzip the file |
| `-v` | Verbose — show files being processed in detail |
| `-f` | File — tells tar we are dealing with a file |
| `-z` | gzip — use .gz compression format |

---

## .tar Format

### Compress (zip)

```bash
tar -cf test.tar test/
```

Breaking it down:
- `tar` → the tool
- `-c` → create/compress
- `-f` → dealing with a file
- `test.tar` → name of the output archive
- `test/` → the folder we want to compress

### Extract (unzip)

```bash
tar -xvf test.tar
```

Breaking it down:
- `-x` → extract
- `-v` → verbose (shows each file as it extracts)
- `-f` → dealing with a file
- `test.tar` → the archive to extract

---

## .tar.gz Format

### Compress (zip)

```bash
tar -czf test.tar.gz folder_name/
```

Breaking it down:
- `-c` → create
- `-z` → use gzip compression (this is what makes it .gz)
- `-f` → dealing with a file
- `test.tar.gz` → output archive name
- `folder_name/` → folder to compress

### Extract (unzip)

```bash
tar -xzvf test.tar.gz
```

Breaking it down:
- `-x` → extract
- `-z` → it's a gzip file
- `-v` → verbose output
- `-f` → dealing with a file

---

## Side by Side Comparison

| Action | .tar | .tar.gz |
|---|---|---|
| Compress | `tar -cf file.tar folder/` | `tar -czf file.tar.gz folder/` |
| Extract | `tar -xvf file.tar` | `tar -xzvf file.tar.gz` |

The only difference is the `-z` flag and the `.gz` extension.

---

## Other Useful tar Commands

```bash
# List contents of an archive without extracting
tar -tf file.tar
tar -tzf file.tar.gz

# Extract to a specific folder
tar -xzvf file.tar.gz -C /destination/folder/

# Compress multiple files
tar -czf archive.tar.gz file1.txt file2.txt file3.txt
```

---

## Quick Reference Table

| Command | What it does |
|---|---|
| `tar -cf out.tar folder/` | Create .tar archive |
| `tar -xvf file.tar` | Extract .tar archive |
| `tar -czf out.tar.gz folder/` | Create .tar.gz archive |
| `tar -xzvf file.tar.gz` | Extract .tar.gz archive |
| `tar -tf file.tar` | List contents without extracting |
| `tar -xzvf file.tar.gz -C /path/` | Extract to specific location |

---

## 🔐 Why This Matters in Hacking

- **Exfiltration:** attackers compress stolen data into `.tar.gz` before transferring it out — smaller size = faster transfer, less suspicious
- **Tool deployment:** offensive tools are often delivered as `.tar.gz` archives to target machines
- **CTF challenges:** downloaded challenge files are almost always `.tar` or `.tar.gz` — you need to extract them before working with them
- **Log archiving:** Linux systems automatically compress old logs into `.tar.gz` — knowing how to read them is essential for log analysis and blue team work
- **Backup scripts:** tar is used in almost every Linux backup script — understanding it helps identify what data is being backed up (and potentially stolen)
