# 🎯 OverTheWire Bandit Walkthrough (Levels 2 → 13)
## ⚡ Short + Clear Linux Command Explanations

---

# 📁 Level 2 → Level 3

## 🎯 Goal
Read a file named:
--spaces in this filename--

## ✅ Solution
```bash
cat "./--spaces in this filename--"
```

## 🔍 Explanation

### `cat`
Displays file content.

### Why quotes?
The filename contains spaces, so Linux treats it as multiple arguments unless wrapped in " ".

### Why `./`?
Because file starts with `--`, Linux may think it's a command option. `./` forces it to be treated as a file.

---

# 📁 Level 3 → Level 4

## 🎯 Goal
Find hidden file inside inhere.

## ✅ Solution
```bash
cd inhere
ls -a
cat .hidden
```

## 🔍 Explanation

### `cd`
Changes directory.

### `ls -a`
Shows all files including hidden ones starting with .

### Hidden files
Linux hides config-like files using . prefix.

---

# 📁 Level 4 → Level 5

## 🎯 Goal
Find human-readable file among many.

## ✅ Solution
```bash
file ./*
cat ./-file07
```

## 🔍 Explanation

### `file`
Identifies file type (text, binary, etc.)

### Why use it?
We don’t know which file is readable, so we detect type first.

---

# 📁 Level 5 → Level 6

## 🎯 Goal
Find file with:
- size 1033 bytes
- readable
- not executable

## ✅ Solution
```bash
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2
```

## 🔍 Explanation

### `find`
Searches files based on conditions.

| Option | Meaning |
|------|--------|
| -type f | Only files |
| -size 1033c | 1033 bytes |
| ! -executable | Not executable |

---

# 📁 Level 6 → Level 7

## 🎯 Goal
Find file owned by bandit7/bandit6, size 33 bytes.

## ✅ Solution
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

## 🔍 Explanation

### find /
Search whole system.

### 2>/dev/null
Hides permission errors.

---

# 📁 Level 7 → Level 8

## 🎯 Goal
Find word millionth in file.

## ✅ Solution
```bash
grep millionth data.txt
```

## 🔍 Explanation

### grep
Searches text inside files.

---

# 📁 Level 8 → Level 9

## 🎯 Goal
Find line that appears only once.

## ✅ Solution
```bash
sort data.txt | uniq -u
```

## 🔍 Explanation

### sort
Groups duplicates.

### uniq -u
Shows only unique lines.

---

# 📁 Level 9 → Level 10

## 🎯 Goal
Extract readable text from binary.

## ✅ Solution
```bash
strings data.txt | grep ===
```

## 🔍 Explanation

### strings
Extract readable text from binary data.

---

# 📁 Level 10 → Level 11

## 🎯 Goal
Decode Base64.

## ✅ Solution
```bash
base64 -d data.txt
```

---

# 📁 Level 11 → Level 12

## 🎯 Goal
Decode ROT13.

## ✅ Solution
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

---

# 📁 Level 12 → Level 13

## 🎯 Goal
Decode hexdump + multiple compressions.

## Step 1
```bash
mktemp -d
cd /tmp/tmp.xxx
```

## Step 2
```bash
xxd -r data.txt > file1
```

## Step 3
Check type and decompress repeatedly:
- gzip → gunzip
- bzip2 → bunzip2
- tar → tar xf

## Final
```bash
cat file
```

---

# 🏁 Summary

You learned:
- file handling
- searching
- encoding/decoding
- compression tools
- Linux pipelines
