## <span style="font-size: 16px">🛠️ Functions</span>

### <span style="font-size: 16px">Defining and Calling Functions</span>

```
# Basic function

def greet():

    print("Hello, World!")

greet()  # Calls function

# Function with parameters

def greet_person(name):

    print(f"Hello, {name}!")

greet_person("Alice")

# Function with return value

def add(a, b):

    return a + b

result = add(5, 3)   # result = 8

# Default parameters

def greet_with_title(name, title="Mr."):

    print(f"Hello, {title} {name}")

greet_with_title("Smith")          # Hello, Mr. Smith

greet_with_title("Smith", "Dr.")   # Hello, Dr. Smith

# Multiple return values (returns as tuple)

def get_min_max(numbers):

    return min(numbers), max(numbers)

min_val, max_val = get_min_max([1, 5, 3, 9, 2])

# *args (variable number of arguments)

def sum_numbers(*args):

    return sum(args)

print(sum_numbers(1, 2, 3))       # 6

print(sum_numbers(1, 2, 3, 4, 5)) # 15

# **kwargs (variable number of keyword arguments)

def print_info(**kwargs):

    for key, value in kwargs.items():

        print(f"{key}: {value}")

print_info(name="Alice", age=30, city="NYC")

# name: Alice

# age: 30

# city: NYC

# Lambda functions (anonymous functions)

square = lambda x: x ** 2

print(square(5))   # 25

# Using lambda with built-in functions

numbers = [1, 2, 3, 4, 5]

squared = list(map(lambda x: x ** 2, numbers))

evens = list(filter(lambda x: x % 2 == 0, numbers))
```

---

## <span style="font-size: 16px">🚨 Error Handling (Try / Except)</span>

```
# Basic try/except

try:

    result = 10 / 0

except ZeroDivisionError:

    print("Cannot divide by zero!")

# Multiple exceptions

try:

    num = int(input("Enter a number: "))

    result = 10 / num

except ValueError:

    print("Please enter a valid number!")

except ZeroDivisionError:

    print("Cannot divide by zero!")

except Exception as e:

    print(f"An error occurred: {e}")

# Try/except/else/finally

try:

    result = 10 / 2

except ZeroDivisionError:

    print("Cannot divide by zero!")

else:

    print(f"Result: {result}")   # Runs if no exception

finally:

    print("Always runs")         # Runs regardless of exception

# Raising exceptions

def check_age(age):

    if age < 0:

        raise ValueError("Age cannot be negative")

    return age
```

---