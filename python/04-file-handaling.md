<span style="font-size: 16px"># 📂 File Handling in Python</span>

<span style="font-size: 16px">A comprehensive guide to reading, writing, and manipulating files using Python.</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## 📖 Table of Contents</span>

<span style="font-size: 16px">1. \[Introduction\](#introduction)</span>

<span style="font-size: 16px">2. \[Opening a File\](#opening-a-file)</span>

<span style="font-size: 16px">3. \[Reading from a File\](#reading-from-a-file)</span>

<span style="font-size: 16px">4. \[Writing to a File\](#writing-to-a-file)</span>

<span style="font-size: 16px">5. \[Appending to a File\](#appending-to-a-file)</span>

<span style="font-size: 16px">6. \[Reading and Writing Simultaneously (\`r+\` Mode)\](#reading-and-writing-simultaneously-r-mode)</span>

<span style="font-size: 16px">7. \[File Pointer Management\](#file-pointer-management)</span>

<span style="font-size: 16px">8. \[Using Context Managers (\`with\` Statement)\](#using-context-managers-with-statement)</span>

<span style="font-size: 16px">9. \[Error Handling\](#error-handling)</span>

<span style="font-size: 16px">10. \[Working with Binary Files\](#working-with-binary-files)</span>

<span style="font-size: 16px">11. \[Best Practices\](#best-practices)</span>

<span style="font-size: 16px">12. \[Conclusion\](#conclusion)</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## Introduction</span>

<span style="font-size: 16px">File handling is an essential skill in Python. It allows you to:</span>

<span style="font-size: 16px">- Read data from existing files (e.g., </span>`.txt`<span style="font-size: 16px">, </span>`.csv`<span style="font-size: 16px">, </span>`.json`<span style="font-size: 16px">, </span>`.png`<span style="font-size: 16px">, </span>`.jpg`<span style="font-size: 16px">).</span>

<span style="font-size: 16px">- Write new data into files.</span>

<span style="font-size: 16px">- Modify or append content to files.</span>

<span style="font-size: 16px">Python provides built-in functions and methods to perform these operations efficiently and safely.</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## Opening a File</span>

<span style="font-size: 16px">The </span>`open()`<span style="font-size: 16px"> function is the gateway to file operations. Its basic syntax is:</span>

<span style="font-size: 16px">\`\`\`python</span>

<span style="font-size: 16px">file_object = open(file_path, mode)</span>

### <span style="font-size: 16px">Common Modes</span>

<table>
<tbody><tr><th colspan="1" rowspan="1"><p><span style="font-size: 16px">Mode</span></p></th><th colspan="1" rowspan="1"><p><span style="font-size: 16px">Description</span></p></th></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">'r'</code></p></td><td colspan="1" rowspan="1"><p><strong><span style="font-size: 16px">Read</span></strong><span style="font-size: 16px"> (default). Opens the file for reading. Fails if file does not exist.</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">'w'</code></p></td><td colspan="1" rowspan="1"><p><strong><span style="font-size: 16px">Write</span></strong><span style="font-size: 16px">. Opens the file for writing. Creates the file if it doesn’t exist, </span><strong><span style="font-size: 16px">overwrites</span></strong><span style="font-size: 16px"> existing content.</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">'a'</code></p></td><td colspan="1" rowspan="1"><p><strong><span style="font-size: 16px">Append</span></strong><span style="font-size: 16px">. Opens the file for writing at the end. Creates the file if it doesn’t exist.</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">'r+'</code></p></td><td colspan="1" rowspan="1"><p><strong><span style="font-size: 16px">Read and Write</span></strong><span style="font-size: 16px">. Opens the file for both reading and writing. The file must exist.</span></p></td></tr><tr><td colspan="1" rowspan="1"><p><code class="hljs" spellcheck="false">'b'</code></p></td><td colspan="1" rowspan="1"><p><strong><span style="font-size: 16px">Binary mode</span></strong><span style="font-size: 16px">. Used with other modes (e.g., </span><code class="hljs" spellcheck="false">'rb'</code><span style="font-size: 16px">, </span><code class="hljs" spellcheck="false">'wb'</code><span style="font-size: 16px">) for non‑text files.</span></p></td></tr></tbody>
</table>

---

## <span style="font-size: 16px">Reading from a File</span>

<span style="font-size: 16px">Once a file is opened in read mode (</span>`'r'`<span style="font-size: 16px">), you can read its content using:</span>

### <span style="font-size: 16px">1. </span>`read()`<span style="font-size: 16px"> – Read the entire content</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "r")
content = file.read()
print(content)
file.close()
```

### <span style="font-size: 16px">2. </span>`readline()`<span style="font-size: 16px"> – Read one line at a time</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "r")
line = file.readline()
while line:
    print(line, end='')
    line = file.readline()
file.close()
```

### <span style="font-size: 16px">3. </span>`readlines()`<span style="font-size: 16px"> – Read all lines into a list</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "r")
lines = file.readlines()
for line in lines:
    print(line, end='')
file.close()
```

> <span style="font-size: 16px">⚠️ </span>**<span style="font-size: 16px">Always close the file</span>**<span style="font-size: 16px"> after reading to free system resources. Using </span>`close()`<span style="font-size: 16px"> is good practice, but we’ll see a better way later.</span>

---

## <span style="font-size: 16px">Writing to a File</span>

<span style="font-size: 16px">To write content, open the file in write mode (</span>`'w'`<span style="font-size: 16px">). If the file does not exist, Python creates it. If it exists, </span>**<span style="font-size: 16px">all previous content is erased</span>**<span style="font-size: 16px">.</span>

### `write()`<span style="font-size: 16px"> – Write a string</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "w")
file.write("Hello, hackers!\n")
file.write("This is a new line.")
file.close()
```

### `writelines()`<span style="font-size: 16px"> – Write a list of strings</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
lines = ["First line\n", "Second line\n", "Third line\n"]
file = open("example.txt", "w")
file.writelines(lines)
file.close()
```

> <span style="font-size: 16px">💡 </span>**<span style="font-size: 16px">Important</span>**<span style="font-size: 16px">: Write mode does </span>**<span style="font-size: 16px">not</span>**<span style="font-size: 16px"> add newline characters automatically; you must include </span>`\n`<span style="font-size: 16px"> where needed.</span>

---

## <span style="font-size: 16px">Appending to a File</span>

<span style="font-size: 16px">Append mode (</span>`'a'`<span style="font-size: 16px">) adds new content at the end of the file without erasing existing data.</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "a")
file.write("This line is appended.\n")
file.close()
```

<span style="font-size: 16px">If the file doesn’t exist, it will be created.</span>

---

## <span style="font-size: 16px">Reading and Writing Simultaneously (</span>`r+`<span style="font-size: 16px"> Mode)</span>

<span style="font-size: 16px">The </span>`'r+'`<span style="font-size: 16px"> mode allows both reading and writing </span>**<span style="font-size: 16px">without truncating</span>**<span style="font-size: 16px"> the file. However, the file must already exist.</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "r+")
content = file.read()        # Read existing content
print(content)
file.write("\nNew content appended via r+")  # Write at the current pointer position
file.close()
```

### <span style="font-size: 16px">Important Points:</span>

- <span style="font-size: 16px">The initial file pointer is at the beginning.</span>

- <span style="font-size: 16px">Writing starts at the current pointer position (by default, position 0).</span>

- <span style="font-size: 16px">To avoid overwriting existing data, you may need to move the pointer (see next section).</span>

---

## <span style="font-size: 16px">File Pointer Management</span>

<span style="font-size: 16px">The file pointer indicates where the next read or write will occur. Use:</span>

- `tell()`<span style="font-size: 16px"> – Returns the current position (in bytes).</span>

- `seek(offset, whence)`<span style="font-size: 16px"> – Moves the pointer.</span>

  - `offset`<span style="font-size: 16px">: number of bytes to move.</span>

  - `whence`<span style="font-size: 16px">: reference point (0 = start, 1 = current, 2 = end).</span>

### <span style="font-size: 16px">Example: Moving to the end before writing</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "r+")
file.seek(0, 2)               # Move to the end of the file
file.write("Appended at the end using r+")
file.close()
```

### <span style="font-size: 16px">Example: Reading after writing</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
file = open("example.txt", "r+")
file.write("Overwrite start")   # Writes from position 0
file.seek(0)                    # Go back to beginning
print(file.read())              # Read the entire content
file.close()
```

---

## <span style="font-size: 16px">Using Context Managers (</span>`with`<span style="font-size: 16px"> Statement)</span>

<span style="font-size: 16px">The </span>`with`<span style="font-size: 16px"> statement automatically closes the file when the block is exited, even if an error occurs. This is the </span>**<span style="font-size: 16px">recommended</span>**<span style="font-size: 16px"> way to handle files.</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
# Reading
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
# File is automatically closed here

# Writing
with open("example.txt", "w") as file:
    file.write("Automatically closed after this block")
```

<span style="font-size: 16px">Benefits:</span>

- <span style="font-size: 16px">No need to remember to call </span>`close()`<span style="font-size: 16px">.</span>

- <span style="font-size: 16px">Cleaner and more readable code.</span>

- <span style="font-size: 16px">Prevents resource leaks.</span>

---

## <span style="font-size: 16px">Error Handling</span>

<span style="font-size: 16px">Always anticipate that file operations may fail (e.g., file not found, permission issues). Use </span>`try-except`<span style="font-size: 16px"> blocks to handle exceptions gracefully.</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
try:
    with open("missing.txt", "r") as file:
        data = file.read()
except FileNotFoundError:
    print("Error: The file does not exist.")
except PermissionError:
    print("Error: You don't have permission to access this file.")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```

---

## <span style="font-size: 16px">Working with Binary Files</span>

<span style="font-size: 16px">For non‑text files (images, audio, etc.), open the file in </span>**<span style="font-size: 16px">binary mode</span>**<span style="font-size: 16px"> by adding </span>`'b'`<span style="font-size: 16px"> to the mode.</span>

<span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

```
# Copy an image file
with open("image.jpg", "rb") as src:
    data = src.read()

with open("copy_image.jpg", "wb") as dest:
    dest.write(data)
```

<span style="font-size: 16px">Common binary modes: </span>`'rb'`<span style="font-size: 16px">, </span>`'wb'`<span style="font-size: 16px">, </span>`'ab'`<span style="font-size: 16px">, </span>`'rb+'`<span style="font-size: 16px">.</span>

---

## <span style="font-size: 16px">Best Practices</span>

1. **<span style="font-size: 16px">Always use</span>** `with`<span style="font-size: 16px"> statements for automatic resource management.</span>

2. **<span style="font-size: 16px">Specify the encoding</span>**<span style="font-size: 16px"> when dealing with text files (e.g., </span>`encoding='utf-8'`<span style="font-size: 16px">) to avoid platform‑specific issues.</span>

   <span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

   ```
   with open("file.txt", "r", encoding="utf-8") as f:
       ...
   ```

3. **<span style="font-size: 16px">Use</span>** `os.path`<span style="font-size: 16px"> or </span>`pathlib`<span style="font-size: 16px"> for robust path handling.</span>

4. **<span style="font-size: 16px">Check if the file exists</span>**<span style="font-size: 16px"> before reading (optional, but avoids exceptions).</span>

   <span style="font-family: Menlo, Monaco, Consolas, Cascadia Mono, Ubuntu Mono, DejaVu Sans Mono, Liberation Mono, JetBrains Mono, Fira Code, Cousine, Roboto Mono, Courier New, Courier, sans-serif, system-ui; color: rgb(15, 17, 21); font-size: 16px">python</span>

   ```
   import os
   if os.path.exists("file.txt"):
       with open("file.txt", "r") as f:
           ...
   ```

5. **<span style="font-size: 16px">Close files explicitly</span>**<span style="font-size: 16px"> if not using </span>`with`<span style="font-size: 16px"> (though </span>`with`<span style="font-size: 16px"> is preferred).</span>

6. **<span style="font-size: 16px">Handle exceptions</span>**<span style="font-size: 16px"> to make your program robust and user‑friendly.</span>

---

## <span style="font-size: 16px">Conclusion</span>

<span style="font-size: 16px">Python provides a simple yet powerful set of tools for file handling. By mastering the various modes (</span>`r`<span style="font-size: 16px">, </span>`w`<span style="font-size: 16px">, </span>`a`<span style="font-size: 16px">, </span>`r+`<span style="font-size: 16px">, and binary variants) and combining them with context managers and error handling, you can build applications that efficiently manage data persistence.</span>

<span style="font-size: 16px">Remember:</span>

- <span style="font-size: 16px">📖 </span>**<span style="font-size: 16px">Read</span>**<span style="font-size: 16px"> to consume data.</span>

- <span style="font-size: 16px">✏️ </span>**<span style="font-size: 16px">Write</span>**<span style="font-size: 16px"> to create or overwrite.</span>

- <span style="font-size: 16px">➕ </span>**<span style="font-size: 16px">Append</span>**<span style="font-size: 16px"> to add without losing content.</span>

- <span style="font-size: 16px">🔀 </span>`r+`<span style="font-size: 16px"> for dual operations.</span>

- <span style="font-size: 16px">🛡️ </span>**<span style="font-size: 16px">Always close</span>**<span style="font-size: 16px"> your files (or use </span>`with`<span style="font-size: 16px">).</span>

<span style="font-size: 16px">Happy coding! 🐍</span>

---

*<span style="font-size: 16px">This guide was created to help Python learners master file handling. Feel free to share and contribute!</span>*
