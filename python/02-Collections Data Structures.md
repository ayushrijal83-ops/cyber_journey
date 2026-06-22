## <span style="font-size: 16px">📚 Collections (Data Structures)</span>

### <span style="font-size: 16px">📋 Lists – Ordered, Mutable Collection</span>

```
# Creating lists

fruits = ["apple", "banana", "cherry"]

numbers = [1, 2, 3, 4, 5]

mixed = [1, "hello", 3.14, True]

empty = []

# Accessing elements

print(fruits[0])     # "apple" - first element

print(fruits[-1])    # "cherry" - last element

print(fruits[0:2])   # ["apple", "banana"] - slicing

# Adding elements

fruits.append("orange")   # ["apple", "banana", "cherry", "orange"]

fruits.insert(1, "grape") # ["apple", "grape", "banana", "cherry", "orange"]

fruits.extend(["mango", "kiwi"]) # ["apple", "grape", "banana", "cherry", "orange", "mango", "kiwi"]

# Removing elements

fruits.remove("banana")   # Removes first "banana"

last = fruits.pop()       # Removes and returns last element ("kiwi")

first = fruits.pop(0)     # Removes and returns element at index 0 ("apple")

del fruits[1]             # Deletes element at index 1

fruits.clear()            # Empties the list

# Iterating through lists

for fruit in fruits:

    print(fruit)

# List comprehension (generate list quickly)

squares = [x**2 for x in range(10)]  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Useful list methods

numbers = [3, 1, 4, 1, 5, 9]

numbers.sort()           # Sorts in place: [1, 1, 3, 4, 5, 9]

numbers.reverse()        # Reverses list: [9, 5, 4, 3, 1, 1]

count = numbers.count(1) # Counts occurrences of 1: 2

index = numbers.index(4) # Finds index of 4: 2

length = len(numbers)    # Length of list: 6
```

---

### <span style="font-size: 16px">🔑 Dictionaries – Key-Value Pairs</span>

```
# Creating dictionaries

person = {

    "name": "Alice",

    "age": 30,

    "city": "New York",

    "skills": ["Python", "Linux", "Networking"]

}

# Accessing values

print(person["name"])        # "Alice"

print(person.get("age"))     # 30

print(person.get("country", "USA"))  # "USA" (default if key not found)

# Adding/updating key-value pairs

person["email"] = "alice@email.com"   # Adds new key

person["age"] = 31                    # Updates existing key

# Removing key-value pairs

del person["city"]           # Removes key "city"

email = person.pop("email")  # Removes and returns value "alice@email.com"

last_item = person.popitem() # Removes and returns last key-value pair

# Iterating through dictionaries

for key, value in person.items():

    print(f"{key}: {value}")

for key in person.keys():

    print(key)

for value in person.values():

    print(value)

# Checking if key exists

if "name" in person:

    print("Name exists")

# Dictionary comprehension

squares = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

---

### <span style="font-size: 16px">🔄 Tuples – Ordered, Immutable Collection</span>

```
# Creating tuples (cannot be modified after creation)

colors = ("red", "green", "blue")

single_tuple = (1,)  # Must include comma for single-element tuple

# Accessing elements (same as lists)

print(colors[0])    # "red"

print(colors[-1])   # "blue"

# Iterating through tuples

for color in colors:

    print(color)

# Tuple unpacking

r, g, b = colors   # r="red", g="green", b="blue"

# When to use tuples:

# - When data should not change (e.g., coordinates, fixed settings)

# - As keys in dictionaries (lists cannot be keys)
```

---

### <span style="font-size: 16px">🎯 Sets – Unordered, Unique Collection</span>

```
# Creating sets

unique_numbers = {1, 2, 3, 4, 5}

mixed_set = {1, "hello", 3.14}

# Adding elements

unique_numbers.add(6)      # {1, 2, 3, 4, 5, 6}

unique_numbers.add(1)      # No change (already exists)

# Removing elements

unique_numbers.remove(6)   # Removes 6 (raises error if not found)

unique_numbers.discard(6)  # Removes 6 (no error if not found)

unique_numbers.pop()       # Removes and returns arbitrary element

unique_numbers.clear()     # Empties set

# Set operations

A = {1, 2, 3, 4}

B = {3, 4, 5, 6}

print(A | B)   # Union: {1, 2, 3, 4, 5, 6}

print(A & B)   # Intersection: {3, 4}

print(A - B)   # Difference: {1, 2}

print(A ^ B)   # Symmetric difference: {1, 2, 5, 6}

# Use sets to remove duplicates from a list

numbers = [1, 2, 2, 3, 3, 4, 5, 5]

unique = list(set(numbers))   # [1, 2, 3, 4, 5]
```

---

## <span style="font-size: 16px">⚙️ Control Flow</span>

### <span style="font-size: 16px">🔀 If / Elif / Else</span>

```
# Basic if statement

age = 20

if age >= 18:

    print("Adult")

# If-else

if age >= 18:

    print("Adult")

else:

    print("Minor")

# If-elif-else

score = 85

if score >= 90:

    grade = "A"

elif score >= 80:

    grade = "B"

elif score >= 70:

    grade = "C"

else:

    grade = "F"

# Multiple conditions

if age >= 18 and age < 65:

    print("Adult of working age")

if age < 18 or age > 65:

    print("Not in working age")

if not is_suspended:

    print("Account active")

# Ternary operator (single-line if-else)

status = "Adult" if age >= 18 else "Minor"
```

---

### <span style="font-size: 16px">🔄 Loops</span>

#### <span style="font-size: 16px">For Loop</span>

```
# Iterating through a list

fruits = ["apple", "banana", "cherry"]

for fruit in fruits:

    print(fruit)

# Iterating through a range

for i in range(5):        # 0, 1, 2, 3, 4

    print(i)

for i in range(2, 8):     # 2, 3, 4, 5, 6, 7

    print(i)

for i in range(1, 10, 2): # 1, 3, 5, 7, 9 (step=2)

    print(i)

# Iterating through dictionary

person = {"name": "Alice", "age": 30}

for key, value in person.items():

    print(f"{key}: {value}")

# Enumerate (get index and value)

for index, fruit in enumerate(fruits):

    print(f"{index}: {fruit}")   # 0: apple, 1: banana, 2: cherry
```

---

#### <span style="font-size: 16px">While Loop</span>

```
# Countdown

count = 5

while count > 0:

    print(count)

    count -= 1   # Decrement by 1

# Infinite loop (use carefully, Ctrl+C to stop)

# while True:

#     print("Infinite")

# Break and Continue

for i in range(10):

    if i == 5:

        break      # Exit loop when i == 5

    print(i)       # Prints 0, 1, 2, 3, 4

for i in range(10):

    if i % 2 == 0:

        continue   # Skip even numbers

    print(i)       # Prints 1, 3, 5, 7, 9
```

---