# 🔧 Functions in Python - Complete Guide (Zero to Hero)

> A function is a **reusable block of code** that performs a specific task.

---

## 🔹 What is a Function?

A function is a block of code that:
- Has a **name**
- Takes **input** (optional)
- Does **something**
- Returns **output** (optional)

### 🧠 Real-World Analogy

> 👉 Think of a function like a **juice machine**:
> - You put in **fruits** (input/arguments)
> - The machine **processes** them (function body)
> - You get **juice** (return value)
>
> You can use the same machine again and again with different fruits.

---

## 🔹 Why Do We Need Functions?

### Without Functions (Bad ❌):

```python
# Calculate area of rectangle — repeated code
length1 = 10
width1 = 5
area1 = length1 * width1
print(f"Area: {area1}")

length2 = 20
width2 = 8
area2 = length2 * width2
print(f"Area: {area2}")

length3 = 15
width3 = 6
area3 = length3 * width3
print(f"Area: {area3}")
```

### With Functions (Good ✅):

```python
def calculate_area(length, width):
    return length * width

print(f"Area: {calculate_area(10, 5)}")
print(f"Area: {calculate_area(20, 8)}")
print(f"Area: {calculate_area(15, 6)}")
```

### Benefits:
- **Reusability** — write once, use many times
- **Readability** — code is organized and clean
- **Maintainability** — fix in one place, fixed everywhere
- **Modularity** — break big problems into small pieces

---

## 🔹 Creating a Function

### Syntax:

```python
def function_name(parameters):
    # function body
    return value
```

- `def` — keyword to define a function
- `function_name` — name of the function (follows variable naming rules)
- `parameters` — inputs (optional)
- `return` — output (optional)

### 🔸 Simplest Function (No Parameters, No Return)

```python
def greet():
    print("Hello, World!")

# Calling the function
greet()
```

Output:
```
Hello, World!
```

### 🔸 Function with Parameters

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Giridhar")
greet("Python")
```

Output:
```
Hello, Giridhar!
Hello, Python!
```

### 🔸 Function with Return Value

```python
def add(a, b):
    result = a + b
    return result

total = add(10, 20)
print(total)   # 30
```

### 🔸 Function with Multiple Parameters

```python
def introduce(name, age, city):
    print(f"I am {name}, {age} years old, from {city}")

introduce("Giridhar", 25, "Hyderabad")
```

---

## 🔹 Parameters vs Arguments

| Term | Meaning | Where? |
|------|---------|--------|
| **Parameter** | Variable in function definition | In `def` line |
| **Argument** | Actual value passed when calling | In function call |

```python
def greet(name):      # name is a PARAMETER
    print(f"Hello, {name}")

greet("Giridhar")     # "Giridhar" is an ARGUMENT
```

---

## 🔹 Types of Arguments (VERY IMPORTANT 🔥)

### 🔸 1. Positional Arguments

Arguments matched by **position** (order matters).

```python
def subtract(a, b):
    return a - b

print(subtract(10, 3))   # 7   (a=10, b=3)
print(subtract(3, 10))   # -7  (a=3, b=10)  ← order matters!
```

### 🔸 2. Keyword Arguments

Arguments matched by **name** (order doesn't matter).

```python
def introduce(name, age, city):
    print(f"{name}, {age}, {city}")

# Using keyword arguments — order doesn't matter
introduce(age=25, city="Hyderabad", name="Giridhar")
```

Output:
```
Giridhar, 25, Hyderabad
```

### 🔸 3. Mixing Positional and Keyword

```python
def introduce(name, age, city):
    print(f"{name}, {age}, {city}")

# Positional first, then keyword
introduce("Giridhar", city="Hyderabad", age=25)   # ✅ Works

# ❌ Positional AFTER keyword — Error!
introduce(name="Giridhar", 25, "Hyderabad")   # SyntaxError
```

✔ **Rule:** Positional arguments must come **before** keyword arguments.

### 🔸 4. Default Parameters

Parameters with **default values**. If no argument is passed, the default is used.

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Giridhar")              # Hello, Giridhar!
greet("Giridhar", "Welcome")   # Welcome, Giridhar!
```

⚠️ **Rule:** Default parameters must come **after** non-default parameters.

```python
# ✅ Correct
def func(a, b, c=10):
    pass

# ❌ Wrong
def func(a, b=10, c):   # SyntaxError
    pass
```

### ⚠️ TRAP: Mutable Default Arguments (INTERVIEW FAVORITE 🔥)

```python
# ❌ DANGEROUS — the list is shared across all calls!
def add_item(item, my_list=[]):
    my_list.append(item)
    return my_list

print(add_item("apple"))    # ['apple']
print(add_item("banana"))   # ['apple', 'banana']  ← BUG!
```

🧠 Why? The default list `[]` is created **once** when the function is defined, not each time it's called. All calls share the **same list object**.

```python
# ✅ CORRECT — use None as default
def add_item(item, my_list=None):
    if my_list is None:
        my_list = []
    my_list.append(item)
    return my_list

print(add_item("apple"))    # ['apple']
print(add_item("banana"))   # ['banana']  ✅ Fresh list each time
```

### 🔸 5. *args — Variable Number of Positional Arguments

When you don't know how many arguments will be passed.

```python
def add_all(*args):
    print(type(args))   # <class 'tuple'>
    total = 0
    for num in args:
        total = total + num
    return total

print(add_all(1, 2, 3))         # 6
print(add_all(10, 20, 30, 40))  # 100
print(add_all(5))               # 5
```

✔ `*args` collects all extra positional arguments into a **tuple**.

#### Pythonic shortcut:

```python
def add_all(*args):
    return sum(args)
```

### 🔸 6. **kwargs — Variable Number of Keyword Arguments

```python
def print_info(**kwargs):
    print(type(kwargs))   # <class 'dict'>
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Giridhar", age=25, city="Hyderabad")
```

Output:
```
<class 'dict'>
name: Giridhar
age: 25
city: Hyderabad
```

✔ `**kwargs` collects all extra keyword arguments into a **dictionary**.

### 🔸 7. Combining All Argument Types

```python
def func(a, b, *args, **kwargs):
    print(f"a = {a}")
    print(f"b = {b}")
    print(f"args = {args}")
    print(f"kwargs = {kwargs}")

func(1, 2, 3, 4, 5, name="Python", version=3)
```

Output:
```
a = 1
b = 2
args = (3, 4, 5)
kwargs = {'name': 'Python', 'version': 3}
```

✔ **Order must be:** `positional → *args → keyword → **kwargs`

---

## 🔹 Argument Unpacking (Passing Lists/Dicts as Arguments)

You've seen how `*args` and `**kwargs` **receive** variable arguments. Now let's see how to **pass** a list or dict into a function using `*` and `**`.

### 🔸 Unpacking a List with `*`

```python
def add(a, b, c):
    return a + b + c

numbers = [10, 20, 30]

# ❌ Wrong — passing the whole list as one argument
# add(numbers)   # TypeError: missing 2 required positional arguments

# ✅ Correct — unpack the list into 3 separate arguments
print(add(*numbers))   # 60
```

🧠 `*numbers` is the same as writing `add(10, 20, 30)`.

### 🔸 Unpacking a Dictionary with `**`

```python
def introduce(name, age, city):
    print(f"I am {name}, {age} years old, from {city}")

info = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

# ❌ Wrong
# introduce(info)   # TypeError

# ✅ Correct — unpack dict into keyword arguments
introduce(**info)   # I am Giridhar, 25 years old, from Hyderabad
```

🧠 `**info` is the same as writing `introduce(name="Giridhar", age=25, city="Hyderabad")`.

### 🔸 Unpacking in Function Calls — Practical Example

```python
def greet(first, last):
    print(f"Hello, {first} {last}!")

name_parts = ("Giridhar", "Reddy")
greet(*name_parts)   # Hello, Giridhar Reddy!

name_dict = {"first": "Giridhar", "last": "Reddy"}
greet(**name_dict)   # Hello, Giridhar Reddy!
```

✔ `*` unpacks **sequences** (list, tuple) into positional arguments.
✔ `**` unpacks **dictionaries** into keyword arguments.

---

## 🔹 Return Statement (VERY IMPORTANT 🔥)

### 🔸 Returning a Value

```python
def square(n):
    return n * n

result = square(5)
print(result)   # 25
```

### 🔸 Return Stops the Function

```python
def check(n):
    if n > 0:
        return "Positive"
    print("This line never runs if n > 0")
    return "Not positive"

print(check(5))   # Positive
```

✔ Once `return` is hit, the function **exits immediately**.

### 🔸 Returning Multiple Values

```python
def get_min_max(numbers):
    return min(numbers), max(numbers)

minimum, maximum = get_min_max([3, 1, 4, 1, 5, 9])
print(f"Min: {minimum}, Max: {maximum}")   # Min: 1, Max: 9
```

🧠 Python actually returns a **tuple**, and we **unpack** it.

```python
result = get_min_max([3, 1, 4, 1, 5, 9])
print(result)        # (1, 9)
print(type(result))  # <class 'tuple'>
```

### 🔸 Function Without Return

If a function has no `return` statement, it returns `None`.

```python
def greet(name):
    print(f"Hello, {name}")

result = greet("Giridhar")
print(result)   # None
```

### 🔸 Return vs Print (COMMON CONFUSION ⚠️)

```python
# print — displays to screen, returns None
def add_print(a, b):
    print(a + b)

# return — gives back a value you can use
def add_return(a, b):
    return a + b

result1 = add_print(3, 4)    # prints 7
print(result1)                # None  ← can't use the value!

result2 = add_return(3, 4)   # doesn't print anything
print(result2)                # 7     ← value is usable!
print(result2 * 2)            # 14    ← can do math with it!
```

✔ Use `return` when you need to **use the result** later. Use `print` only for **displaying**.

---

## 🔹 Scope of Variables (VERY IMPORTANT 🔥)

### 🔸 Local Scope — Inside a Function

```python
def my_func():
    x = 10   # local variable
    print(x)

my_func()     # 10
print(x)      # ❌ NameError: name 'x' is not defined
```

✔ `x` exists **only inside** the function. It's destroyed when the function ends.

### 🔸 Global Scope — Outside All Functions

```python
x = 10   # global variable

def my_func():
    print(x)   # can READ global variable

my_func()     # 10
print(x)      # 10
```

### 🔸 Local vs Global — Same Name

```python
x = 10   # global

def my_func():
    x = 20   # local (different variable!)
    print(f"Inside: {x}")

my_func()           # Inside: 20
print(f"Outside: {x}")  # Outside: 10
```

✔ The local `x` **shadows** the global `x` inside the function. They are **different variables**.

### 🔸 The `global` Keyword

To **modify** a global variable inside a function:

```python
x = 10

def my_func():
    global x
    x = 20

my_func()
print(x)   # 20  ← global x was changed
```

⚠️ **Avoid using `global`** — it makes code harder to debug. Pass values as arguments and return results instead.

### 🔸 The `nonlocal` Keyword

For **nested functions** — to modify a variable from the enclosing function:

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x = 20

    inner()
    print(x)   # 20

outer()
```

### 🔸 LEGB Rule (Scope Resolution Order)

When Python looks for a variable, it searches in this order:

```
L — Local (inside current function)
E — Enclosing (inside enclosing/outer function)
G — Global (module level)
B — Built-in (Python's built-in names)
```

```python
x = "global"

def outer():
    x = "enclosing"

    def inner():
        x = "local"
        print(x)   # local

    inner()

outer()
```

---

## 🔹 Docstrings (Documentation Strings)

A string at the **beginning** of a function that describes what it does.

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.

    Parameters:
        length (float): The length of the rectangle
        width (float): The width of the rectangle

    Returns:
        float: The area of the rectangle
    """
    return length * width
```

### 🔸 Accessing Docstrings

```python
print(calculate_area.__doc__)

# Or using help()
help(calculate_area)
```

✔ Docstrings are important for **code documentation** and **team collaboration**.

---

## 🔹 Lambda Functions (Anonymous Functions)

A **one-line** function without a name.

### Syntax:

```python
lambda parameters: expression
```

### 🔸 Basic Lambda

```python
# Normal function
def square(n):
    return n * n

# Same thing as lambda
square = lambda n: n * n

print(square(5))   # 25
```

### 🔸 Lambda with Multiple Parameters

```python
add = lambda a, b: a + b
print(add(3, 4))   # 7

full_name = lambda first, last: f"{first} {last}"
print(full_name("Giridhar", "Reddy"))   # Giridhar Reddy
```

### 🔸 Lambda with Conditional

```python
check = lambda n: "Even" if n % 2 == 0 else "Odd"

print(check(4))   # Even
print(check(7))   # Odd
```

### 🔸 When to Use Lambda?

✔ Use lambda for **short, simple** functions — especially as arguments to other functions.

❌ Don't use lambda for **complex logic** — use a regular function instead.

---

## 🔹 Higher-Order Functions (IMPORTANT 🔥)

A function that **takes another function as an argument** or **returns a function**.

### 🔸 map() — Apply Function to Every Item

```python
numbers = [1, 2, 3, 4, 5]

# Without map (manual way)
squared = []
for num in numbers:
    squared.append(num * num)
print(squared)   # [1, 4, 9, 16, 25]

# With map
squared = list(map(lambda n: n * n, numbers))
print(squared)   # [1, 4, 9, 16, 25]
```

#### map() with a Named Function

```python
def double(n):
    return n * 2

numbers = [1, 2, 3, 4, 5]
result = list(map(double, numbers))
print(result)   # [2, 4, 6, 8, 10]
```

### 🔸 filter() — Keep Items That Match a Condition

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Without filter (manual way)
evens = []
for num in numbers:
    if num % 2 == 0:
        evens.append(num)
print(evens)   # [2, 4, 6, 8, 10]

# With filter
evens = list(filter(lambda n: n % 2 == 0, numbers))
print(evens)   # [2, 4, 6, 8, 10]
```

### 🔸 reduce() — Reduce All Items to a Single Value

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Without reduce (manual way)
total = 0
for num in numbers:
    total = total + num
print(total)   # 15

# With reduce
total = reduce(lambda a, b: a + b, numbers)
print(total)   # 15
```

🧠 How reduce works step by step:
```
Step 1: a=1, b=2 → 3
Step 2: a=3, b=3 → 6
Step 3: a=6, b=4 → 10
Step 4: a=10, b=5 → 15
```

#### Pythonic shortcut:

```python
print(sum(numbers))   # 15
```

✔ For simple sum, use `sum()`. Use `reduce()` for more complex accumulations.

### 🔸 sorted() with key Function

```python
names = ["Charlie", "Alice", "Bob"]

# Sort alphabetically (default)
print(sorted(names))   # ['Alice', 'Bob', 'Charlie']

# Sort by length
print(sorted(names, key=lambda name: len(name)))
# ['Bob', 'Alice', 'Charlie']

# Sort by last character
print(sorted(names, key=lambda name: name[-1]))
# ['Charlie', 'Alice', 'Bob']
```

---

## 🔹 Recursion (Function Calling Itself)

A function that **calls itself** to solve a problem by breaking it into smaller sub-problems.

### 🔸 Basic Example: Countdown

```python
def countdown(n):
    if n <= 0:
        print("Done!")
        return
    print(n)
    countdown(n - 1)

countdown(5)
```

Output:
```
5
4
3
2
1
Done!
```

### 🔸 Factorial Using Recursion

```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))   # 120
```

🧠 How it works:
```
factorial(5) = 5 * factorial(4)
             = 5 * 4 * factorial(3)
             = 5 * 4 * 3 * factorial(2)
             = 5 * 4 * 3 * 2 * factorial(1)
             = 5 * 4 * 3 * 2 * 1
             = 120
```

### 🔸 Fibonacci Using Recursion

```python
def fibonacci(n):
    if n <= 0:
        return 0
    if n == 1:
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)

for i in range(10):
    print(fibonacci(i), end=" ")
```

Output:
```
0 1 1 2 3 5 8 13 21 34
```

### 🔸 Base Case (CRITICAL ⚠️)

Every recursive function **must** have a **base case** — a condition that stops the recursion.

```python
# ❌ No base case — infinite recursion!
def bad_recursion(n):
    return bad_recursion(n - 1)   # RecursionError!

# ✅ Has base case
def good_recursion(n):
    if n <= 0:       # base case
        return 0
    return n + good_recursion(n - 1)
```

### 🔸 Recursion Limit

Python has a default recursion limit of **1000**.

```python
import sys
print(sys.getrecursionlimit())   # 1000

# You can change it (not recommended)
sys.setrecursionlimit(5000)
```

### 🔸 Recursion vs Iteration

| Aspect | Recursion | Iteration (Loop) |
|--------|-----------|-----------------|
| Readability | Cleaner for tree/graph problems | Cleaner for simple repetition |
| Performance | Slower (function call overhead) | Faster |
| Memory | Uses call stack (can overflow) | Uses constant memory |
| When to use | Trees, graphs, divide & conquer | Most other cases |

---

## 🔹 Nested Functions (Functions Inside Functions)

```python
def outer():
    print("Outer function")

    def inner():
        print("Inner function")

    inner()

outer()
```

Output:
```
Outer function
Inner function
```

✔ `inner()` can only be called **inside** `outer()`.

---

## 🔹 Functions as First-Class Objects

In Python, functions are **objects**. You can:

### 🔸 Assign a Function to a Variable

```python
def greet(name):
    return f"Hello, {name}"

say_hello = greet   # no parentheses — assigning the function itself
print(say_hello("Giridhar"))   # Hello, Giridhar
```

### 🔸 Pass a Function as an Argument

```python
def apply(func, value):
    return func(value)

def double(n):
    return n * 2

print(apply(double, 5))   # 10
```

### 🔸 Return a Function from a Function (Closures 🔥)

A **closure** is a function that **remembers the variables from its enclosing scope** even after the outer function has finished executing.

```python
def multiplier(factor):
    def multiply(n):
        return n * factor   # 'factor' is remembered from the enclosing scope
    return multiply

double = multiplier(2)
triple = multiplier(3)

print(double(5))   # 10
print(triple(5))   # 15
```

🧠 How it works:
- `multiplier(2)` returns the `multiply` function with `factor = 2` **locked in**
- `multiplier(3)` returns a **different** `multiply` function with `factor = 3`
- Each returned function **remembers** its own `factor` value — this is a **closure**

### 🔸 Why is "Closure" Important?

- It's a **common interview keyword** — interviewers expect you to name this pattern
- Closures are the foundation of **decorators** (advanced topic)
- They allow **data hiding** without using classes

### 🔸 Verifying a Closure

```python
def outer(x):
    def inner():
        return x
    return inner

my_func = outer(10)
print(my_func())                    # 10
print(my_func.__closure__)          # (<cell at 0x...>,)
print(my_func.__closure__[0].cell_contents)  # 10
```

✔ `__closure__` shows the variables the function has "closed over".

---

## 🔹 Type Hints in Functions (Python 3.5+)

```python
def add(a: int, b: int) -> int:
    return a + b

def greet(name: str) -> str:
    return f"Hello, {name}"

def is_even(n: int) -> bool:
    return n % 2 == 0
```

✔ Type hints are **not enforced** by Python. They're for documentation and IDE support.

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Calling Before Defining

```python
# ❌ Error
greet()

def greet():
    print("Hello")
```

✔ Define the function **before** calling it.

### 🔸 Mistake 2: Forgetting Return

```python
def add(a, b):
    result = a + b
    # forgot return!

total = add(3, 4)
print(total)   # None  ← not what you wanted!
```

### 🔸 Mistake 3: Modifying Global Variable Without global

```python
count = 0

def increment():
    count = count + 1   # ❌ UnboundLocalError

increment()
```

✔ Use `global count` or pass as parameter and return.

### 🔸 Mistake 4: Mutable Default Argument

```python
# ❌ Bug
def add_item(item, items=[]):
    items.append(item)
    return items

# ✅ Fix
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

---

## 🔹 Built-in Functions — Quick Reference 📌

| Function | Description | Example |
|----------|-------------|---------|
| `print()` | Display output | `print("Hi")` |
| `input()` | Get user input | `input("Name: ")` |
| `len()` | Length of sequence | `len("Hello")` → 5 |
| `type()` | Check type | `type(10)` → int |
| `int()` | Convert to int | `int("10")` → 10 |
| `float()` | Convert to float | `float("3.14")` → 3.14 |
| `str()` | Convert to string | `str(10)` → "10" |
| `bool()` | Convert to bool | `bool(0)` → False |
| `list()` | Convert to list | `list("abc")` → ['a','b','c'] |
| `range()` | Number sequence | `range(5)` → 0,1,2,3,4 |
| `sum()` | Sum of items | `sum([1,2,3])` → 6 |
| `max()` | Maximum value | `max(1,2,3)` → 3 |
| `min()` | Minimum value | `min(1,2,3)` → 1 |
| `abs()` | Absolute value | `abs(-5)` → 5 |
| `round()` | Round number | `round(3.7)` → 4 |
| `sorted()` | Sort items | `sorted([3,1,2])` → [1,2,3] |
| `reversed()` | Reverse items | `list(reversed([1,2,3]))` → [3,2,1] |
| `enumerate()` | Index + value | `enumerate(["a","b"])` |
| `zip()` | Pair items | `zip([1,2], ["a","b"])` |
| `map()` | Apply function | `map(str, [1,2,3])` |
| `filter()` | Filter items | `filter(bool, [0,1,2])` |
| `isinstance()` | Check type | `isinstance(10, int)` → True |
| `id()` | Memory address | `id(10)` |
| `hash()` | Hash value | `hash("hello")` |
| `help()` | Documentation | `help(print)` |
| `dir()` | List attributes | `dir(str)` |

---

## 🔹 Interview Programs 💡

### ✅ 1. Function to Check Palindrome

#### Manual way (using while loop — two pointers):

```python
def is_palindrome(text):
    text = text.lower()
    left = 0
    right = len(text) - 1

    while left < right:
        if text[left] != text[right]:
            return False
        left = left + 1
        right = right - 1

    return True

print(is_palindrome("Madam"))    # True
print(is_palindrome("Python"))   # False
```

🧠 How it works:
- Start with two pointers: one at the **beginning**, one at the **end**
- Compare characters at both positions
- If they don't match → not a palindrome
- Move both pointers inward and repeat

```
"madam"
 ↑   ↑     m == m ✅
  ↑ ↑      a == a ✅
   ↑       left meets right → Palindrome!
```

#### Manual way (using for loop — build reversed string):

```python
def is_palindrome(text):
    text = text.lower()
    reversed_text = ""

    for char in text:
        reversed_text = char + reversed_text

    return text == reversed_text

print(is_palindrome("Madam"))    # True
print(is_palindrome("Python"))   # False
```

#### Pythonic shortcut:

```python
def is_palindrome(text):
    text = text.lower()
    return text == text[::-1]

print(is_palindrome("Madam"))    # True
print(is_palindrome("Python"))   # False
```

✔ Understand the manual logic first, then use the shortcut in real code.

---

### ✅ 2. Function to Find GCD

#### Manual way:

```python
def gcd(a, b):
    while b != 0:
        temp = b
        b = a % b
        a = temp
    return a

print(gcd(12, 8))   # 4
```

#### Pythonic shortcut:

```python
import math
print(math.gcd(12, 8))   # 4
```

---

### ✅ 3. Function to Count Vowels

```python
def count_vowels(text):
    count = 0
    for char in text.lower():
        if char in "aeiou":
            count = count + 1
    return count

print(count_vowels("Python Programming"))   # 4
```

---

### ✅ 4. Function to Check Prime

```python
def is_prime(n):
    if n <= 1:
        return False
    i = 2
    while i * i <= n:
        if n % i == 0:
            return False
        i = i + 1
    return True

print(is_prime(29))   # True
print(is_prime(15))   # False
```

---

### ✅ 5. Recursive Function — Power

```python
def power(base, exp):
    if exp == 0:
        return 1
    return base * power(base, exp - 1)

print(power(2, 10))   # 1024
```

#### Pythonic shortcut:

```python
print(2 ** 10)       # 1024
print(pow(2, 10))    # 1024
```

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| `def` | Define a function |
| Parameters | Variables in function definition |
| Arguments | Values passed when calling |
| Positional args | Matched by position |
| Keyword args | Matched by name |
| Default params | Have default values |
| `*args` | Variable positional args (tuple) |
| `**kwargs` | Variable keyword args (dict) |
| `return` | Send back a value |
| Multiple returns | Returns a tuple |
| No return | Returns `None` |
| Local scope | Variable inside function |
| Global scope | Variable outside function |
| `global` | Modify global inside function |
| `nonlocal` | Modify enclosing scope variable |
| LEGB | Scope resolution order |
| Docstrings | Function documentation |
| Lambda | One-line anonymous function |
| `map()` | Apply function to all items |
| `filter()` | Keep items matching condition |
| `reduce()` | Reduce to single value |
| Recursion | Function calling itself |
| Base case | Stops recursion |
| First-class | Functions are objects |
| Type hints | Optional type annotations |

---

> 🚀 **Next:** Lists in Python →
