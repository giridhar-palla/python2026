# 📦 Variables & Data Types in Python - Complete Guide (Zero to Hero)

> A variable is a **name that stores a value** in memory.

---

## 🔹 What is a Variable?

A variable is like a **container** or **label** that holds a value.

### 🧠 Real-World Analogy

> 👉 Think of a variable as a **labeled box**.
> - The **label** is the variable name
> - The **item inside** is the value
>
> Box labeled "age" → contains 25
> Box labeled "name" → contains "Giridhar"

---

## 🔹 Creating Variables

In Python, you **don't need to declare** the type. Just assign a value.

```python
name = "Giridhar"
age = 25
price = 99.5
is_student = True
```

✔ No `int`, `float`, `string` keyword needed — Python figures it out automatically. This is called **dynamic typing**.

### ⚠️ COMMON TRAP: Forgetting Quotes on Strings (NameError 🔥)

```python
# ✅ Correct — text inside quotes
name = "Giridhar"

# ❌ Wrong — no quotes
name = Giridhar   # NameError: name 'Giridhar' is not defined
```

🧠 Without quotes, Python thinks `Giridhar` is a **variable name** and tries to look it up. Since no variable called `Giridhar` exists, it throws a `NameError`.

**Rule:** Text values **always** need quotes. Numbers do not.

```python
city = "Hyderabad"   # ✅ string — needs quotes
age = 25             # ✅ number — no quotes needed
```

### 🔸 Variable Assignment — What Happens Internally?

```python
x = 10
```

🧠 Step by step:
1. Python creates an **integer object** `10` in memory
2. Python creates a **variable name** `x`
3. Python makes `x` **point to** (reference) that object

```python
x = 10
print(id(x))   # memory address of the object 10
```

---

## 🔹 Variable Naming Rules (VERY IMPORTANT 🔥)

### ✅ Valid Names

```python
name = "Python"
_name = "Python"
__name = "Python"
name1 = "Python"
my_name = "Python"
myName = "Python"
MY_NAME = "Python"
```

### ❌ Invalid Names

```python
1name = "Python"     # ❌ Cannot start with a number
my-name = "Python"   # ❌ Cannot use hyphens
my name = "Python"   # ❌ Cannot have spaces
class = "Python"     # ❌ Cannot use Python keywords
@name = "Python"     # ❌ Cannot use special characters
```

### 🔸 Rules Summary

| Rule | Example | Valid? |
|------|---------|:---:|
| Can start with letter | `name` | ✅ |
| Can start with underscore | `_name` | ✅ |
| Cannot start with number | `1name` | ❌ |
| Can contain letters, numbers, underscores | `my_name1` | ✅ |
| Cannot contain spaces | `my name` | ❌ |
| Cannot contain special characters | `my@name` | ❌ |
| Cannot be a Python keyword | `class` | ❌ |
| Case-sensitive | `Name` ≠ `name` | ✅ |

---

## 🔹 Variable Naming Conventions (Best Practices)

| Convention | Style | Used For |
|-----------|-------|----------|
| snake_case | `my_variable` | Variables, functions |
| UPPER_SNAKE_CASE | `MAX_VALUE` | Constants |
| camelCase | `myVariable` | Not common in Python |
| PascalCase | `MyClass` | Class names |
| _single_leading_underscore | `_private` | Private variables |
| __double_leading_underscore | `__very_private` | Name mangling |

```python
# ✅ Good Python style
first_name = "Giridhar"
max_retries = 3
is_logged_in = True

# ❌ Not Pythonic (but works)
firstName = "Giridhar"
MaxRetries = 3
```

---

## 🔹 Multiple Assignment

### 🔸 Assign Same Value to Multiple Variables

```python
a = b = c = 10

print(a)   # 10
print(b)   # 10
print(c)   # 10
```

### 🔸 Assign Different Values in One Line

```python
a, b, c = 10, 20, 30

print(a)   # 10
print(b)   # 20
print(c)   # 30
```

### 🔸 Swap Two Variables

```python
a = 10
b = 20

# Python way — no temp variable needed!
a, b = b, a

print(a)   # 20
print(b)   # 10
```

### ⚠️ Unpacking Mismatch Error (IMPORTANT 🔥)

The number of variables on the left **must match** the number of values on the right.

```python
# ❌ Too many values
a, b = 10, 20, 30
# ValueError: too many values to unpack (expected 2)

# ❌ Not enough values
a, b, c = 10, 20
# ValueError: not enough values to unpack (expected 3, got 2)

# ✅ Correct — counts match
a, b, c = 10, 20, 30
```

#### Using `*` to Catch Extra Values

```python
a, *b = 10, 20, 30, 40

print(a)   # 10
print(b)   # [20, 30, 40]
```

```python
a, *b, c = 10, 20, 30, 40, 50

print(a)   # 10
print(b)   # [20, 30, 40]
print(c)   # 50
```

✔ The `*` variable collects **all the extra values** into a list.

---

## 🔹 Variable Reassignment

```python
x = 10
print(x)        # 10
print(type(x))  # <class 'int'>

x = "Hello"
print(x)        # Hello
print(type(x))  # <class 'str'>
```

✔ In Python, a variable can **change its type** at any time. This is **dynamic typing**.

### 🔸 What Happens in Memory?

```python
x = 10
print(id(x))   # address A (points to integer 10)

x = "Hello"
print(id(x))   # address B (now points to string "Hello")
```

✔ The old object `10` is **not modified**. `x` simply **points to a new object**.

---

## 🔹 Deleting Variables

```python
x = 10
print(x)   # 10

del x
print(x)   # ❌ NameError: name 'x' is not defined
```

✔ `del` removes the variable name. The object in memory gets cleaned up by **garbage collection** if nothing else references it.

---

## 🔹 Constants in Python

Python does **NOT** have true constants. By convention, we use **UPPER_SNAKE_CASE** to indicate a value should not be changed.

```python
PI = 3.14159
MAX_USERS = 100
BASE_URL = "https://api.example.com"

# ⚠️ Python won't stop you from changing it
PI = 3.14   # No error, but BAD practice
```

---

## 🔹 Checking Variable Type — type()

```python
name = "Python"
age = 25
price = 99.5
is_active = True

print(type(name))       # <class 'str'>
print(type(age))        # <class 'int'>
print(type(price))      # <class 'float'>
print(type(is_active))  # <class 'bool'>
```

---

## 🔹 Checking Variable Identity — id()

Every object in Python has a **unique identity** (memory address).

```python
a = 10
b = 10

print(id(a))   # same address
print(id(b))   # same address (Python reuses small integers)

print(a is b)  # True (same object)
```

⚠️ **Small Integer Caching:** Python caches integers from **-5 to 256**. So:

```python
a = 256
b = 256
print(a is b)   # True  (cached)

a = 257
b = 257
print(a is b)   # May be False (not cached)
```

✔ Always use `==` for value comparison, not `is`.

---

# 📊 Data Types in Python

---

## 🔹 What is a Data Type?

A data type tells Python **what kind of value** a variable holds.

### 🧠 Real-World Analogy

> 👉 Think of data types as **different types of containers**:
> - A **jar** holds liquids (float)
> - A **box** holds solid items (int)
> - A **notebook** holds text (str)
> - A **switch** is on/off (bool)

---

## 🔹 Python Data Types — Complete List

### 🔸 Basic (Primitive) Types

| Type | Keyword | Example | Description |
|------|---------|---------|-------------|
| Integer | `int` | `10`, `-5`, `0` | Whole numbers |
| Float | `float` | `3.14`, `-2.5` | Decimal numbers |
| String | `str` | `"Hello"`, `'Hi'` | Text |
| Boolean | `bool` | `True`, `False` | Yes/No values |
| Complex | `complex` | `3+4j` | Complex numbers |
| NoneType | `None` | `None` | No value / empty |

### 🔸 Collection (Container) Types

| Type | Keyword | Example | Ordered? | Mutable? | Duplicates? |
|------|---------|---------|:---:|:---:|:---:|
| List | `list` | `[1, 2, 3]` | ✅ | ✅ | ✅ |
| Tuple | `tuple` | `(1, 2, 3)` | ✅ | ❌ | ✅ |
| Set | `set` | `{1, 2, 3}` | ❌ | ✅ | ❌ |
| Frozen Set | `frozenset` | `frozenset({1,2})` | ❌ | ❌ | ❌ |
| Dictionary | `dict` | `{"a": 1}` | ✅ (3.7+) | ✅ | Keys: ❌ |

### 🔸 Binary Types

| Type | Keyword | Example |
|------|---------|---------|
| Bytes | `bytes` | `b"hello"` |
| Byte Array | `bytearray` | `bytearray(5)` |
| Memory View | `memoryview` | `memoryview(b"hello")` |

---

## 🔹 Integer (int)

Whole numbers — positive, negative, or zero. **No decimal point**.

```python
a = 10
b = -5
c = 0
d = 1000000

print(type(a))   # <class 'int'>
```

### 🔸 No Size Limit!

Unlike other languages (C, Java), Python integers have **no maximum size**.

```python
big_num = 99999999999999999999999999999999
print(big_num)        # works perfectly!
print(type(big_num))  # <class 'int'>
```

### 🔸 Underscores for Readability

```python
population = 1_000_000_000
print(population)   # 1000000000
```

✔ Underscores are **ignored** by Python. They just make big numbers easier to read.

### 🔸 Integer in Different Bases

```python
decimal = 10        # base 10 (normal)
binary = 0b1010     # base 2 (prefix 0b)
octal = 0o12        # base 8 (prefix 0o)
hexadecimal = 0xA   # base 16 (prefix 0x)

print(decimal)       # 10
print(binary)        # 10
print(octal)         # 10
print(hexadecimal)   # 10
```

✔ All four represent the **same value** (10), just written in different number systems.

---

## 🔹 Float (float)

Numbers with a **decimal point**.

```python
a = 3.14
b = -2.5
c = 0.0

print(type(a))   # <class 'float'>
```

### 🔸 Float Precision Issue ⚠️ (INTERVIEW FAVORITE 🔥)

```python
print(0.1 + 0.2)   # 0.30000000000000004  (NOT 0.3!)
```

🧠 Why?
- Computers store floats in **binary** (base 2)
- Some decimal numbers **cannot be represented exactly** in binary
- This is NOT a Python bug — it happens in ALL programming languages

### 🔸 How to Fix Precision Issues

```python
# Method 1: round()
print(round(0.1 + 0.2, 1))   # 0.3

# Method 2: decimal module (for exact calculations)
from decimal import Decimal
print(Decimal("0.1") + Decimal("0.2"))   # 0.3
```

### 🔸 Special Float Values

```python
print(float("inf"))     # inf  (positive infinity)
print(float("-inf"))    # -inf (negative infinity)
print(float("nan"))     # nan  (not a number)

# Checking
import math
print(math.isinf(float("inf")))   # True
print(math.isnan(float("nan")))   # True
```

### 🔸 Integer Division vs Float Division

```python
print(10 / 3)    # 3.3333333333333335  (float division)
print(10 // 3)   # 3                   (integer/floor division)
```

### 🔸 Scientific Notation (e notation)

Python supports writing floats using `e` or `E` for powers of 10.

```python
a = 1.5e3
print(a)          # 1500.0
print(type(a))    # <class 'float'>

b = 2.5e-4
print(b)          # 0.00025

c = 1e6
print(c)          # 1000000.0
```

🧠 How it works:
- `1.5e3` means `1.5 × 10³` = `1500.0`
- `2.5e-4` means `2.5 × 10⁻⁴` = `0.00025`
- `1e6` means `1 × 10⁶` = `1000000.0`

✔ Very common in **data science** (Pandas, NumPy) and when working with very large or very small numbers.

```python
# Avogadro's number
avogadro = 6.022e23
print(avogadro)   # 6.022e+23

# Electron mass in kg
electron_mass = 9.109e-31
print(electron_mass)   # 9.109e-31
```

---

## 🔹 String (str)

A sequence of characters inside quotes. (Covered in detail in `strings.md`)

```python
name = "Python"
greeting = 'Hello'
multiline = """This is
multi-line"""

print(type(name))   # <class 'str'>
```

---

## 🔹 Boolean (bool)

Only two values: `True` or `False`.

```python
is_active = True
is_deleted = False

print(type(is_active))   # <class 'bool'>
```

### 🔸 Boolean is a Subclass of int (INTERVIEW 🔥)

```python
print(isinstance(True, int))   # True

print(True + True)     # 2
print(True + 1)        # 2
print(False + 0)       # 0
```

### 🔸 Truthy and Falsy Values

**Falsy** (evaluate to `False`):
```python
# All of these are False in boolean context
bool(0)        # False
bool(0.0)      # False
bool("")       # False
bool([])       # False
bool(())       # False
bool({})       # False
bool(set())    # False
bool(None)     # False
```

**Truthy** (evaluate to `True`):
```python
# Everything else is True
bool(1)        # True
bool(-1)       # True
bool("Hi")     # True
bool([1])      # True
bool({"a":1})  # True
```

---

## 🔹 Complex (complex)

Numbers with a **real** and **imaginary** part.

```python
c = 3 + 4j

print(c)          # (3+4j)
print(type(c))    # <class 'complex'>
print(c.real)     # 3.0
print(c.imag)     # 4.0
```

⚠️ Python uses `j` for imaginary part (not `i` like in math).

---

## 🔹 NoneType (None)

`None` represents **no value** or **nothing**.

```python
x = None

print(x)          # None
print(type(x))    # <class 'NoneType'>
```

### 🔸 None is NOT the Same as 0, False, or ""

```python
print(None == 0)       # False
print(None == False)   # False
print(None == "")      # False
print(None is None)    # True
```

### 🔸 Common Use of None

```python
# Default value for a variable
result = None

# Function that doesn't return anything
def greet():
    print("Hello")

x = greet()
print(x)   # None
```

### 🔸 Checking for None

```python
x = None

# ✅ Correct way
if x is None:
    print("x has no value")

# ❌ Not recommended
if x == None:
    print("x has no value")
```

✔ Always use `is None`, not `== None`. (Because `is` checks identity, `==` can be overridden.)

---

## 🔹 List (list) — Brief Overview

An **ordered, mutable** collection that allows **duplicates**.

```python
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]

print(type(fruits))   # <class 'list'>
```

✔ Detailed coverage in a separate `lists.md` file.

---

## 🔹 Tuple (tuple) — Brief Overview

An **ordered, immutable** collection that allows **duplicates**.

```python
colors = ("red", "green", "blue")
point = (10, 20)

print(type(colors))   # <class 'tuple'>
```

✔ Like a list, but **cannot be changed** after creation.

---

## 🔹 Set (set) — Brief Overview

An **unordered, mutable** collection with **no duplicates**.

```python
unique_nums = {1, 2, 3, 2, 1}
print(unique_nums)   # {1, 2, 3}  (duplicates removed)

print(type(unique_nums))   # <class 'set'>
```

---

## 🔹 Dictionary (dict) — Brief Overview

A collection of **key-value pairs**. Keys must be unique.

```python
person = {
    "name": "Giridhar",
    "age": 25,
    "city": "Hyderabad"
}

print(person["name"])   # Giridhar
print(type(person))     # <class 'dict'>
```

---

## 🔹 Mutable vs Immutable (VERY IMPORTANT 🔥)

| Type | Mutable? | Can Change After Creation? |
|------|:---:|:---:|
| `int` | ❌ | No |
| `float` | ❌ | No |
| `str` | ❌ | No |
| `bool` | ❌ | No |
| `tuple` | ❌ | No |
| `frozenset` | ❌ | No |
| `list` | ✅ | Yes |
| `dict` | ✅ | Yes |
| `set` | ✅ | Yes |
| `bytearray` | ✅ | Yes |

### 🔸 What Does Immutable Mean?

```python
# String is immutable
text = "Hello"
text[0] = "J"   # ❌ TypeError

# List is mutable
nums = [1, 2, 3]
nums[0] = 10    # ✅ Works
print(nums)     # [10, 2, 3]
```

### 🔸 Why Does It Matter?

- **Immutable objects** can be used as **dictionary keys** and **set elements**
- **Mutable objects** cannot be used as dictionary keys

```python
# ✅ Tuple as dict key (immutable)
d = {(1, 2): "point"}

# ❌ List as dict key (mutable)
d = {[1, 2]: "point"}   # TypeError: unhashable type: 'list'
```

---

## 🔹 Dynamic Typing vs Static Typing

### 🔸 Python = Dynamic Typing

```python
x = 10          # x is int
x = "Hello"     # now x is str
x = [1, 2, 3]   # now x is list
```

✔ Variable type can **change at runtime**. No need to declare type.

### 🔸 Static Typing (Other Languages like Java, C)

```java
int x = 10;       // x is always int
x = "Hello";      // ❌ Error in Java
```

### 🔸 Type Hints (Python 3.5+) — Optional

Python supports **optional type hints** for readability and tooling:

```python
name: str = "Giridhar"
age: int = 25
price: float = 99.5
is_active: bool = True
```

⚠️ Type hints are **NOT enforced** by Python. They're just for documentation and IDE support.

```python
age: int = 25
age = "twenty-five"   # ✅ No error! Python doesn't enforce it.
```

---

## 🔹 Checking Types — type() vs isinstance()

```python
x = 10

# type() — exact type
print(type(x))              # <class 'int'>
print(type(x) == int)       # True

# isinstance() — includes inheritance (BETTER ✅)
print(isinstance(x, int))   # True
print(isinstance(True, int))  # True  (bool is subclass of int)
```

✔ Use `isinstance()` in most cases. It handles inheritance properly.

---

## 🔹 Interview Questions 💡

### ✅ Q1: What is dynamic typing?

**Answer:** In Python, you don't declare variable types. The type is determined at runtime based on the assigned value, and can change anytime.

---

### ✅ Q2: What is the difference between `is` and `==`?

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)   # True   (same value)
print(a is b)   # False  (different objects in memory)
```

**Answer:** `==` checks **value equality**, `is` checks **identity** (same object in memory).

---

### ✅ Q3: What is the output?

```python
a = 256
b = 256
print(a is b)

c = 257
d = 257
print(c is d)
```

**Answer:** `True` then possibly `False`. Python caches integers -5 to 256.

---

### ✅ Q4: Can a variable name start with a number?

**Answer:** No. Variable names must start with a letter or underscore.

---

### ✅ Q5: What is None?

**Answer:** `None` is Python's null value. It represents the absence of a value. Its type is `NoneType`. Always check with `is None`, not `== None`.

---

### ✅ Q6: Why is `0.1 + 0.2 != 0.3`?

**Answer:** Floating-point numbers are stored in binary. Some decimal fractions cannot be represented exactly in binary, causing tiny precision errors. Use `round()` or `decimal.Decimal` for exact comparisons.

---

### ✅ Q7: What is the difference between mutable and immutable?

**Answer:** Mutable objects (list, dict, set) can be changed after creation. Immutable objects (int, str, tuple) cannot. Immutable objects can be used as dictionary keys; mutable objects cannot.

---

### ✅ Q8: What is the output?

```python
x = 10
y = x
x = 20

print(y)
```

**Answer:** `10`. `y` still points to the original object `10`. Reassigning `x` doesn't affect `y`.

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| Variable | A name that stores a value |
| Dynamic Typing | Type determined at runtime, can change |
| Naming Rules | Start with letter/underscore, no spaces/special chars |
| `type()` | Check the type of a variable |
| `id()` | Check the memory address |
| `del` | Delete a variable |
| `int` | Whole numbers, no size limit |
| `float` | Decimal numbers, precision issues |
| `str` | Text in quotes |
| `bool` | True / False |
| `complex` | Real + imaginary (3+4j) |
| `None` | No value, check with `is None` |
| `list` | Ordered, mutable, allows duplicates |
| `tuple` | Ordered, immutable, allows duplicates |
| `set` | Unordered, mutable, no duplicates |
| `dict` | Key-value pairs, keys unique |
| Mutable | list, dict, set — can change |
| Immutable | int, str, tuple, frozenset — cannot change |
| Type Hints | Optional annotations, not enforced |

---

> 🚀 **Next:** Operators in Python →
