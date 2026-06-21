<span style="font-size: 16px"># 🐍 Python Basics – Complete Reference Guide</span>

<span style="font-size: 16px">&gt; </span>**<span style="font-size: 16px">Purpose:</span>**<span style="font-size: 16px"> A comprehensive reference for all Python fundamentals.  </span>

<span style="font-size: 16px">&gt; </span>**<span style="font-size: 16px">Use this:</span>**<span style="font-size: 16px"> As a quick lookup while building your port scanner and recon tools.</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">## 📦 Data Types & Variables</span>

<span style="font-size: 16px">### Variables</span>

<span style="font-size: 16px">Variables store data. No declaration needed – Python infers the type.</span>

<span style="font-size: 16px">\`\`\`python</span>

```
# Variable assignment

name = "Alice"           # String

age = 25                 # Integer

height = 5.8             # Float

is_student = True        # Boolean
```

---

### <span style="font-size: 16px">📝 Strings</span>

<span style="font-size: 16px">Text data enclosed in quotes (single </span>`'`<span style="font-size: 16px">, double </span>`"`<span style="font-size: 16px">, or triple </span>`'''`<span style="font-size: 16px"> for multi-line).</span>

```
# String examples

greeting = "Hello, World!"

single_quoted = 'Python is fun'

multi_line = """This is a

multi-line string"""

# String methods

text = "  Python  "

print(text.strip())          # "Python" - removes whitespace

print(text.upper())          # "  PYTHON  "

print(text.lower())          # "  python  "

print(text.replace("P", "J")) # "  Jython  "

# String indexing & slicing

word = "Cybersecurity"

print(word[0])          # 'C' - first character

print(word[-1])         # 'y' - last character

print(word[0:5])        # "Cyber" - first 5 characters

print(word[5:])         # "security" - from index 5 to end

# String concatenation & formatting

first = "Cyber"

last = "Security"

full = first + last      # "CyberSecurity"

age = 25

message = f"I am {age} years old"  # f-string (Python 3.6+)

message2 = "I am {} years old".format(age)  # format method

🔢 Numbers (Integers & Floats)

# Integers

age = 25

count = -10

large = 1_000_000  # Underscore for readability

# Floats (decimal numbers)

pi = 3.14159

price = 19.99

# Basic operations

sum = 10 + 5         # 15

diff = 10 - 5        # 5

product = 10 * 5     # 50

division = 10 / 3    # 3.3333333333333335

floor_div = 10 // 3  # 3 (integer division, rounds down)

modulo = 10 % 3      # 1 (remainder)

power = 2 ** 3       # 8 (2 to the power of 3)

# Type conversion

num_str = "123"

num_int = int(num_str)   # Converts to integer: 123

num_float = float(num_str) # Converts to float: 123.0

str_num = str(123)        # Converts to string: "123"
```

---

### <span style="font-size: 16px">✅ Booleans (</span>`True`<span style="font-size: 16px"> / </span>`False`<span style="font-size: 16px">)</span>

```
is_authenticated = True

is_admin = False

# Boolean operators

x = True

y = False

print(x and y)   # False

print(x or y)    # True

print(not x)     # False

# Comparisons (return Booleans)

print(10 > 5)    # True

print(10 == 10)  # True

print(10 != 5)   # True

print(10 <= 5)   # False

# Truthy / Falsy values

print(bool(0))      # False

print(bool(1))      # True

print(bool(""))     # False (empty string)

print(bool("abc"))  # True

print(bool([]))     # False (empty list)

print(bool([1,2]))  # True

```