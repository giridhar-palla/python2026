# 🔄 Type Casting in Python - Complete Guide (Zero to Hero)

> Type Casting means **converting one data type into another data type**.

---

## 🔹 What is Type Casting?

Type Casting (also called **Type Conversion**) is the process of converting a value from **one data type to another**.

### 🧠 Real-World Analogy

> 👉 Think of it like **converting currency**. You have Dollars and you want Rupees — the value changes form but represents the same thing.
>
> Similarly, `"100"` (string) can be converted to `100` (integer) — same value, different type.

---

## 🔹 Why Do We Need Type Casting?

```python
age = input("Enter your age: ")
print(type(age))   # <class 'str'>
```

⚠️ `input()` **always returns a string**, even if the user types a number.

```python
age = input("Enter your age: ")   # user types 25
print(age + 5)   # ❌ TypeError: can only concatenate str (not "int") to str
```

✔ To fix this, we need to **convert** the string to an integer:

```python
age = int(input("Enter your age: "))   # now age is an integer
print(age + 5)   # ✅ 30
```

---

## 🔹 Two Types of Type Casting

| Type | Meaning | Who Does It? |
|------|---------|-------------|
| **Implicit** (Automatic) | Python converts automatically | Python itself |
| **Explicit** (Manual) | You convert manually using functions | The programmer |

---

## 🔹 1️⃣ Implicit Type Casting (Automatic)

Python **automatically** converts a smaller data type to a larger data type to **prevent data loss**.

### 🔸 int → float (Automatic)

```python
a = 10      # int
b = 2.5     # float

result = a + b
print(result)        # 12.5
print(type(result))  # <class 'float'>
```

🧠 What happened?
- `a` is `int` (10)
- `b` is `float` (2.5)
- Python **automatically** converted `a` from `int` to `float` before adding
- Result is `float` (12.5)

### 🔸 int → float in Division

```python
result = 10 / 3
print(result)        # 3.3333333333333335
print(type(result))  # <class 'float'>
```

✔ Division (`/`) **always** returns a `float`, even if both numbers are integers.

```python
result = 10 / 2
print(result)        # 2.0  (not 2!)
print(type(result))  # <class 'float'>
```

### 🔸 bool → int (Automatic)

```python
a = True    # bool
b = 10      # int

result = a + b
print(result)        # 11
print(type(result))  # <class 'int'>
```

🧠 What happened?
- `True` is treated as `1`
- `False` is treated as `0`
- So `True + 10` = `1 + 10` = `11`

```python
print(True + True)     # 2
print(True + False)    # 1
print(False + False)   # 0
```

### 🔸 bool → float (Automatic)

```python
a = True     # bool
b = 3.5      # float

result = a + b
print(result)        # 4.5
print(type(result))  # <class 'float'>
```

### 🔸 Implicit Conversion Hierarchy

```
bool → int → float → complex
```

Python converts the **smaller type** to the **larger type** automatically.

```python
# bool + int → int
print(type(True + 10))       # <class 'int'>

# int + float → float
print(type(10 + 2.5))        # <class 'float'>

# float + complex → complex
print(type(2.5 + (3+4j)))    # <class 'complex'>
```

### 🔸 When Implicit Conversion Does NOT Happen ⚠️

```python
a = "10"    # str
b = 20      # int

result = a + b   # ❌ TypeError: can only concatenate str (not "int") to str
```

✔ Python does **NOT** automatically convert `str` to `int` or `int` to `str`. You must do it **manually** (explicit casting).

---

## 🔹 2️⃣ Explicit Type Casting (Manual)

You use **built-in functions** to convert types manually.

| Function | Converts To | Example |
|----------|------------|---------|
| `int()` | Integer | `int("10")` → `10` |
| `float()` | Float | `float("3.14")` → `3.14` |
| `str()` | String | `str(100)` → `"100"` |
| `bool()` | Boolean | `bool(1)` → `True` |
| `list()` | List | `list("abc")` → `['a','b','c']` |
| `tuple()` | Tuple | `tuple([1,2,3])` → `(1,2,3)` |
| `set()` | Set | `set([1,2,2,3])` → `{1,2,3}` |
| `dict()` | Dictionary | `dict([(a,1)])` → `{'a':1}` |
| `complex()` | Complex | `complex(2,3)` → `(2+3j)` |
| `ord()` | ASCII number | `ord("A")` → `65` |
| `chr()` | Character | `chr(65)` → `"A"` |
| `hex()` | Hexadecimal string | `hex(255)` → `"0xff"` |
| `oct()` | Octal string | `oct(8)` → `"0o10"` |
| `bin()` | Binary string | `bin(10)` → `"0b1010"` |

---

### 🔸 int() — Convert to Integer

#### String to Integer

```python
text = "100"
num = int(text)

print(num)          # 100
print(type(num))    # <class 'int'>
```

#### Float to Integer (Truncates — Removes Decimal Part)

```python
price = 99.99
num = int(price)

print(num)          # 99  (NOT rounded, just truncated!)
print(type(num))    # <class 'int'>
```

⚠️ **Important:** `int()` does NOT round. It **removes** the decimal part.

```python
print(int(3.9))     # 3   (not 4!)
print(int(3.1))     # 3
print(int(-3.9))    # -3  (not -4!)
print(int(-3.1))    # -3
```

#### Boolean to Integer

```python
print(int(True))    # 1
print(int(False))   # 0
```

#### ❌ What CANNOT Be Converted to int

```python
# String with decimal point
int("3.14")     # ❌ ValueError: invalid literal for int()

# String with letters
int("hello")    # ❌ ValueError: invalid literal for int()

# Empty string
int("")          # ❌ ValueError: invalid literal for int()

# None
int(None)        # ❌ TypeError: int() argument must be a string...
```

#### ✅ Fix: String with Decimal → First Convert to Float, Then to Int

```python
text = "3.14"

# ❌ Wrong
# num = int(text)   # ValueError

# ✅ Correct — two-step conversion
num = int(float(text))
print(num)   # 3
```

#### int() with Different Bases

```python
# Binary string to int
print(int("1010", 2))    # 10

# Octal string to int
print(int("12", 8))      # 10

# Hexadecimal string to int
print(int("A", 16))      # 10
print(int("FF", 16))     # 255
```

🧠 The second argument is the **base** of the number system.

---

### 🔸 float() — Convert to Float

#### String to Float

```python
text = "3.14"
num = float(text)

print(num)          # 3.14
print(type(num))    # <class 'float'>
```

#### Integer to Float

```python
num = float(10)
print(num)          # 10.0
print(type(num))    # <class 'float'>
```

#### Boolean to Float

```python
print(float(True))    # 1.0
print(float(False))   # 0.0
```

#### Special Float Values

```python
# Infinity
print(float("inf"))     # inf
print(float("-inf"))    # -inf
print(float("infinity"))  # inf

# Not a Number
print(float("nan"))     # nan
```

#### ❌ What CANNOT Be Converted to float

```python
float("hello")    # ❌ ValueError
float("")          # ❌ ValueError
float(None)        # ❌ TypeError
```

---

### 🔸 str() — Convert to String

#### Integer to String

```python
num = 100
text = str(num)

print(text)         # "100"
print(type(text))   # <class 'str'>
```

#### Float to String

```python
price = 99.5
text = str(price)

print(text)         # "99.5"
print(type(text))   # <class 'str'>
```

#### Boolean to String

```python
print(str(True))    # "True"
print(str(False))   # "False"
```

#### List / Tuple / Dict to String

```python
print(str([1, 2, 3]))          # "[1, 2, 3]"
print(str((1, 2, 3)))          # "(1, 2, 3)"
print(str({"a": 1}))           # "{'a': 1}"
```

#### None to String

```python
print(str(None))    # "None"
```

✔ `str()` can convert **almost anything** to a string. It rarely fails.

#### ⚠️ COMMON TRAP: str(list) vs "".join(list) (INTERVIEW FAVORITE 🔥)

90% of beginners make this mistake. They want to merge list items into a word or sentence and use `str()`.

```python
fruits = ["apple", "banana", "cherry"]

# ❌ What beginners try (WRONG for merging)
print(str(fruits))          # "['apple', 'banana', 'cherry']"  ← includes brackets and quotes!

# ✅ What you actually want (use join)
print(", ".join(fruits))    # "apple, banana, cherry"
print(" ".join(fruits))     # "apple banana cherry"
print("".join(fruits))      # "applebananacherry"
```

🧠 **Rule:**
- `str(list)` → gives the **literal representation** of the list (with brackets, commas, quotes)
- `"".join(list)` → **merges the elements** into a single string

```python
letters = ["P", "y", "t", "h", "o", "n"]

print(str(letters))         # "['P', 'y', 't', 'h', 'o', 'n']"  ❌ not what you want
print("".join(letters))     # "Python"  ✅ this is what you want
```

---

### 🔸 bool() — Convert to Boolean

#### 🧠 The Rule: Truthy and Falsy Values

**❌ Falsy Values** (convert to `False`):

```python
print(bool(0))        # False
print(bool(0.0))      # False
print(bool(""))       # False   (empty string)
print(bool([]))       # False   (empty list)
print(bool(()))       # False   (empty tuple)
print(bool({}))       # False   (empty dict)
print(bool(set()))    # False   (empty set)
print(bool(None))     # False
print(bool(False))    # False
```

**✅ Truthy Values** (convert to `True`):

```python
print(bool(1))        # True
print(bool(-1))       # True    (any non-zero number)
print(bool(3.14))     # True
print(bool("Hi"))     # True    (non-empty string)
print(bool([1,2]))    # True    (non-empty list)
print(bool({"a":1}))  # True    (non-empty dict)
```

#### ⚠️ Tricky Cases (INTERVIEW FAVORITE 🔥)

```python
print(bool("0"))       # True   ← string "0" is NOT empty, so True!
print(bool("False"))   # True   ← string "False" is NOT empty, so True!
print(bool(" "))       # True   ← string with space is NOT empty, so True!
```

🧠 **Remember:** For strings, only `""` (completely empty) is `False`. Any string with content (even `"0"` or `" "`) is `True`.

---

### 🔸 list() — Convert to List

#### String to List

```python
text = "Python"
chars = list(text)
print(chars)   # ['P', 'y', 't', 'h', 'o', 'n']
```

✔ Each **character** becomes a separate list item.

#### ⚠️ COMMON TRAP: list("string") vs "string".split() (VERY IMPORTANT 🔥)

Beginners often try `list()` on a comma-separated string expecting actual items:

```python
data = "1,2,3"

# ❌ What beginners expect: [1, 2, 3]
# ❌ What they actually get:
print(list(data))          # ['1', ',', '2', ',', '3']  ← every character separated!

# ✅ What you actually want (use split)
print(data.split(","))     # ['1', '2', '3']
```

Another example:

```python
names = "apple,banana,cherry"

# ❌ Wrong — splits every character
print(list(names))         # ['a', 'p', 'p', 'l', 'e', ',', 'b', ...]

# ✅ Correct — splits by comma
print(names.split(","))    # ['apple', 'banana', 'cherry']
```

🧠 **Rule:**
- `list("string")` → splits into **individual characters**
- `"string".split(separator)` → splits into **actual items** by the separator

#### Tuple to List

```python
my_tuple = (1, 2, 3)
my_list = list(my_tuple)
print(my_list)   # [1, 2, 3]
```

#### Set to List

```python
my_set = {3, 1, 2}
my_list = list(my_set)
print(my_list)   # [1, 2, 3]  (order may vary)
```

#### Range to List

```python
nums = list(range(5))
print(nums)   # [0, 1, 2, 3, 4]

nums2 = list(range(1, 6))
print(nums2)   # [1, 2, 3, 4, 5]
```

#### Dictionary to List (Keys Only)

```python
my_dict = {"a": 1, "b": 2, "c": 3}
keys = list(my_dict)
print(keys)   # ['a', 'b', 'c']
```

✔ `list(dict)` gives only **keys**, not values.

---

### 🔸 tuple() — Convert to Tuple

#### List to Tuple

```python
my_list = [1, 2, 3]
my_tuple = tuple(my_list)
print(my_tuple)   # (1, 2, 3)
```

#### String to Tuple

```python
text = "Python"
chars = tuple(text)
print(chars)   # ('P', 'y', 't', 'h', 'o', 'n')
```

#### Set to Tuple

```python
my_set = {3, 1, 2}
my_tuple = tuple(my_set)
print(my_tuple)   # (1, 2, 3)  (order may vary)
```

---

### 🔸 set() — Convert to Set

#### List to Set (Removes Duplicates!)

```python
my_list = [1, 2, 2, 3, 3, 3]
my_set = set(my_list)
print(my_set)   # {1, 2, 3}
```

✔ Sets **automatically remove duplicates**.

#### String to Set

```python
text = "hello"
chars = set(text)
print(chars)   # {'h', 'e', 'l', 'o'}  (no duplicate 'l', order may vary)
```

#### Tuple to Set

```python
my_tuple = (1, 2, 2, 3)
my_set = set(my_tuple)
print(my_set)   # {1, 2, 3}
```

---

### 🔸 dict() — Convert to Dictionary

#### List of Tuples to Dictionary

```python
pairs = [("a", 1), ("b", 2), ("c", 3)]
my_dict = dict(pairs)
print(my_dict)   # {'a': 1, 'b': 2, 'c': 3}
```

#### List of Lists to Dictionary

```python
pairs = [["name", "Python"], ["version", 3]]
my_dict = dict(pairs)
print(my_dict)   # {'name': 'Python', 'version': 3}
```

#### Using Keyword Arguments

```python
my_dict = dict(name="Python", version=3)
print(my_dict)   # {'name': 'Python', 'version': 3}
```

#### zip() to Dictionary

```python
keys = ["name", "age", "city"]
values = ["Giridhar", 25, "Hyderabad"]

my_dict = dict(zip(keys, values))
print(my_dict)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}
```

---

### 🔸 complex() — Convert to Complex Number

```python
# From two numbers
c = complex(2, 3)
print(c)          # (2+3j)
print(type(c))    # <class 'complex'>

# From integer
c = complex(5)
print(c)          # (5+0j)

# From string
c = complex("2+3j")
print(c)          # (2+3j)
```

⚠️ **No spaces in string:**
```python
complex("2 + 3j")   # ❌ ValueError
complex("2+3j")     # ✅ Works
```

---

### 🔸 ord() and chr() — Character ↔ ASCII Number

#### ord() — Character to Number

```python
print(ord("A"))   # 65
print(ord("a"))   # 97
print(ord("0"))   # 48
print(ord(" "))   # 32
print(ord("Z"))   # 90
```

#### chr() — Number to Character

```python
print(chr(65))    # A
print(chr(97))    # a
print(chr(48))    # 0
print(chr(32))    # (space)
```

#### Practical Use: Print A-Z

```python
i = 65
while i <= 90:
    print(chr(i), end=" ")
    i = i + 1
```
Output:
```
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
```

#### Using for loop:

```python
for i in range(65, 91):
    print(chr(i), end=" ")
```

---

### 🔸 hex(), oct(), bin() — Number System Conversions

#### bin() — Integer to Binary String

```python
print(bin(10))    # 0b1010
print(bin(255))   # 0b11111111
print(bin(0))     # 0b0
```

#### oct() — Integer to Octal String

```python
print(oct(8))     # 0o10
print(oct(10))    # 0o12
print(oct(255))   # 0o377
```

#### hex() — Integer to Hexadecimal String

```python
print(hex(10))    # 0xa
print(hex(255))   # 0xff
print(hex(16))    # 0x10
```

⚠️ These return **strings**, not numbers:
```python
result = bin(10)
print(type(result))   # <class 'str'>
```

#### Convert Back to Integer

```python
print(int("0b1010", 2))    # 10  (binary to int)
print(int("0o12", 8))      # 10  (octal to int)
print(int("0xa", 16))      # 10  (hex to int)
```

---

## 🔹 Complete Type Conversion Matrix (INTERVIEW FAVORITE 🔥)

This table shows **what can be converted to what**:

| From ↓ / To → | int | float | str | bool | list | tuple | set |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **int** | — | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ |
| **float** | ✅ (truncates) | — | ✅ | ✅ | ❌ | ❌ | ❌ |
| **str** | ✅ (if numeric) | ✅ (if numeric) | — | ✅ | ✅ (chars) | ✅ (chars) | ✅ (chars) |
| **bool** | ✅ | ✅ | ✅ | — | ❌ | ❌ | ❌ |
| **list** | ❌ | ❌ | ✅ | ✅ | — | ✅ | ✅ |
| **tuple** | ❌ | ❌ | ✅ | ✅ | ✅ | — | ✅ |
| **set** | ❌ | ❌ | ✅ | ✅ | ✅ | ✅ | — |
| **dict** | ❌ | ❌ | ✅ | ✅ | ✅ (keys) | ✅ (keys) | ✅ (keys) |
| **None** | ❌ | ❌ | ✅ ("None") | ✅ (False) | ❌ | ❌ | ❌ |

---

## 🔹 Data Loss in Type Casting ⚠️

### 🔸 float → int (Decimal Part Lost)

```python
num = 9.99
result = int(num)
print(result)   # 9  ← lost 0.99
```

### 🔸 int → bool (Information Lost)

```python
num = 42
result = bool(num)
print(result)   # True  ← lost the actual value 42
```

### 🔸 list → set (Duplicates Lost + Order Lost)

```python
my_list = [3, 1, 2, 2, 3]
my_set = set(my_list)
print(my_set)   # {1, 2, 3}  ← lost duplicates and order
```

### 🔸 dict → list (Values Lost)

```python
my_dict = {"a": 1, "b": 2}
my_list = list(my_dict)
print(my_list)   # ['a', 'b']  ← lost all values!
```

✔ To keep values:
```python
print(list(my_dict.values()))   # [1, 2]
print(list(my_dict.items()))    # [('a', 1), ('b', 2)]
```

---

## 🔹 int() Truncation vs round() (IMPORTANT 🔥)

```python
# int() — just removes decimal (truncates toward zero)
print(int(3.7))      # 3
print(int(-3.7))     # -3

# round() — rounds to nearest integer
print(round(3.7))    # 4
print(round(-3.7))   # -4
print(round(3.5))    # 4
print(round(4.5))    # 4   ← Banker's rounding! (rounds to even)

# math.floor() — always rounds DOWN
import math
print(math.floor(3.7))    # 3
print(math.floor(-3.7))   # -4

# math.ceil() — always rounds UP
print(math.ceil(3.2))     # 4
print(math.ceil(-3.2))    # -3
```

| Function | 3.7 | -3.7 | 3.5 | 4.5 |
|----------|:---:|:---:|:---:|:---:|
| `int()` | 3 | -3 | 3 | 4 |
| `round()` | 4 | -4 | 4 | 4 |
| `math.floor()` | 3 | -4 | 3 | 4 |
| `math.ceil()` | 4 | -3 | 4 | 5 |

⚠️ **Banker's Rounding:** `round(0.5)` = `0`, `round(1.5)` = `2`, `round(2.5)` = `2`. Python rounds `.5` to the **nearest even number**. This is a common interview trick question.

---

## 🔹 Type Checking — type() vs isinstance()

### 🔸 type() — Returns Exact Type

```python
print(type(10))         # <class 'int'>
print(type(3.14))       # <class 'float'>
print(type("hello"))    # <class 'str'>
print(type(True))       # <class 'bool'>
print(type([1,2]))      # <class 'list'>
print(type(None))       # <class 'NoneType'>
```

#### Comparing types:

```python
x = 10

if type(x) == int:
    print("It's an integer")
```

### 🔸 isinstance() — Checks Type Including Inheritance (BETTER ✅)

```python
x = 10

print(isinstance(x, int))      # True
print(isinstance(x, float))    # False
print(isinstance(x, (int, float)))  # True  (check multiple types)
```

### 🔸 type() vs isinstance() — Key Difference (INTERVIEW 🔥)

```python
# bool is a SUBCLASS of int in Python
x = True

print(type(x) == int)        # False  (type is bool, not int)
print(type(x) == bool)       # True

print(isinstance(x, int))    # True   (bool inherits from int!)
print(isinstance(x, bool))   # True
```

✔ `isinstance()` checks the **inheritance chain**, `type()` checks **exact type only**.

✔ **Best practice:** Use `isinstance()` in most cases.

---

## 🔹 Safe Type Conversion (Error Handling)

In real-world programs, conversions can fail. Always handle errors.

### 🔸 Using try-except (Basic Way)

```python
text = "hello"

try:
    num = int(text)
    print(num)
except ValueError:
    print("Cannot convert to integer!")
```

Output:
```
Cannot convert to integer!
```

### 🔸 Check Before Converting

```python
text = "123"

if text.isdigit():
    num = int(text)
    print(num)   # 123
else:
    print("Not a valid number")
```

⚠️ **Limitation of isdigit():**
```python
print("-5".isdigit())     # False  (negative numbers)
print("3.14".isdigit())   # False  (decimals)
```

### 🔸 Safe Conversion Function (Real-World Pattern)

```python
def safe_int(value, default=0):
    try:
        return int(value)
    except (ValueError, TypeError):
        return default

print(safe_int("42"))       # 42
print(safe_int("hello"))    # 0  (default)
print(safe_int(None))       # 0  (default)
print(safe_int("abc", -1))  # -1 (custom default)
```

### 🔸 Safe Float Conversion

```python
def safe_float(value, default=0.0):
    try:
        return float(value)
    except (ValueError, TypeError):
        return default

print(safe_float("3.14"))     # 3.14
print(safe_float("hello"))    # 0.0
print(safe_float(None))       # 0.0
```

---

## 🔹 Implicit vs Explicit — When to Use What?

| Situation | Use |
|-----------|-----|
| Math with int + float | Implicit (Python handles it) |
| User input (always string) | Explicit: `int(input(...))` |
| Displaying numbers in text | Explicit: `str(num)` or f-string |
| Comparing different types | Explicit: convert first |
| Reading from files/APIs | Explicit: always convert |
| Boolean checks | Implicit (truthy/falsy) |

---

## 🔹 Common Mistakes & Gotchas ⚠️

### 🔸 Mistake 1: Forgetting input() returns string

```python
# ❌ Wrong
age = input("Age: ")
if age > 18:          # TypeError: '>' not supported between str and int
    print("Adult")

# ✅ Correct
age = int(input("Age: "))
if age > 18:
    print("Adult")
```

### 🔸 Mistake 2: int() on decimal string

```python
# ❌ Wrong
num = int("3.14")     # ValueError

# ✅ Correct
num = int(float("3.14"))   # 3
```

### 🔸 Mistake 3: Confusing str "0" with int 0

```python
print(bool(0))      # False
print(bool("0"))    # True   ← NOT the same!
```

### 🔸 Mistake 4: Assuming list(dict) gives key-value pairs

```python
d = {"a": 1, "b": 2}
print(list(d))          # ['a', 'b']  ← only keys!
print(list(d.items()))  # [('a', 1), ('b', 2)]  ← key-value pairs
```

### 🔸 Mistake 5: Comparing types with == instead of isinstance

```python
x = True

# ❌ Misleading
print(type(x) == int)       # False

# ✅ Better
print(isinstance(x, int))   # True  (bool is subclass of int)
```

### 🔸 Mistake 6: round() with .5 values

```python
print(round(0.5))   # 0   ← NOT 1! (Banker's rounding)
print(round(1.5))   # 2
print(round(2.5))   # 2   ← NOT 3!
```

---

## 🔹 Interview Questions & Programs 💡

### ✅ Q1: What is the output?

```python
print(type(True + 10))
```

**Answer:** `<class 'int'>` — `True` is `1`, so `1 + 10 = 11` (int)

---

### ✅ Q2: What is the output?

```python
print(int(3.99))
```

**Answer:** `3` — `int()` truncates, does NOT round.

---

### ✅ Q3: What is the output?

```python
print(bool("False"))
```

**Answer:** `True` — `"False"` is a non-empty string, so it's truthy.

---

### ✅ Q4: What is the output?

```python
print(bool([]))
print(bool([0]))
```

**Answer:**
- `False` — empty list is falsy
- `True` — list with one element (even 0) is truthy

---

### ✅ Q5: What is the output?

```python
print(int("0b1010", 2))
```

**Answer:** `10` — binary `1010` = decimal `10`

---

### ✅ Q6: What is the output?

```python
print(float(True) + float(False))
```

**Answer:** `1.0` — `float(True)` = `1.0`, `float(False)` = `0.0`

---

### ✅ Q7: Will this work?

```python
int(None)
```

**Answer:** ❌ `TypeError` — `None` cannot be converted to int.

---

### ✅ Q8: What is the output?

```python
x = "10"
y = 20
print(int(x) + y)
```

**Answer:** `30` — `int("10")` = `10`, then `10 + 20 = 30`

---

### ✅ Q9: What is the output?

```python
print(list("hello"))
```

**Answer:** `['h', 'e', 'l', 'l', 'o']`

---

### ✅ Q10: What is the output?

```python
print(round(2.5))
print(round(3.5))
```

**Answer:** `2` and `4` — Banker's rounding (rounds to nearest even).

---

### ✅ Program 1: Check if a String Can Be Converted to a Number

```python
text = "123.45"

try:
    float(text)
    print(f"'{text}' is a valid number")
except ValueError:
    print(f"'{text}' is NOT a valid number")
```

---

### ✅ Program 2: Convert Temperature (String Input)

```python
celsius_str = input("Enter temperature in Celsius: ")
celsius = float(celsius_str)
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C = {fahrenheit}°F")
```

---

### ✅ Program 3: Sum of Digits in a Number

```python
num = 12345
text = str(num)
total = 0

for char in text:
    total = total + int(char)

print(f"Sum of digits: {total}")   # Sum of digits: 15
```

---

### ✅ Program 4: Convert List of Strings to List of Integers

#### Using while loop (basic way):

```python
str_list = ["10", "20", "30", "40"]
int_list = []
i = 0

while i < len(str_list):
    int_list.append(int(str_list[i]))
    i = i + 1

print(int_list)   # [10, 20, 30, 40]
```

#### Using for loop:

```python
str_list = ["10", "20", "30", "40"]
int_list = []

for item in str_list:
    int_list.append(int(item))

print(int_list)   # [10, 20, 30, 40]
```

---

### ✅ Program 5: Swap Two Variables Without Temp (Using Type Trick)

```python
a = 10
b = 20

# Python way (no type casting needed, but shows understanding)
a, b = b, a

print(a)   # 20
print(b)   # 10
```

---

## 🔹 All Conversion Functions — Quick Reference 📌

| Function | What It Does | Example | Result |
|----------|-------------|---------|--------|
| `int()` | To integer | `int("10")` | `10` |
| `float()` | To float | `float("3.14")` | `3.14` |
| `str()` | To string | `str(100)` | `"100"` |
| `bool()` | To boolean | `bool(0)` | `False` |
| `list()` | To list | `list("abc")` | `['a','b','c']` |
| `tuple()` | To tuple | `tuple([1,2])` | `(1, 2)` |
| `set()` | To set | `set([1,1,2])` | `{1, 2}` |
| `dict()` | To dictionary | `dict([("a",1)])` | `{'a': 1}` |
| `complex()` | To complex | `complex(2,3)` | `(2+3j)` |
| `ord()` | Char → number | `ord("A")` | `65` |
| `chr()` | Number → char | `chr(65)` | `"A"` |
| `bin()` | Int → binary | `bin(10)` | `"0b1010"` |
| `oct()` | Int → octal | `oct(8)` | `"0o10"` |
| `hex()` | Int → hex | `hex(255)` | `"0xff"` |
| `round()` | Round number | `round(3.7)` | `4` |

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| Type Casting | Converting one data type to another |
| Implicit | Python converts automatically (int→float, bool→int) |
| Explicit | You convert manually using functions |
| Hierarchy | `bool → int → float → complex` |
| `int()` | Truncates float, converts numeric strings |
| `float()` | Adds decimal, supports `inf` and `nan` |
| `str()` | Converts anything to string |
| `bool()` | Falsy: `0, 0.0, "", [], {}, None, False` |
| `list()` | String→chars, dict→keys |
| `set()` | Removes duplicates |
| Data Loss | float→int loses decimal, list→set loses duplicates |
| `int()` vs `round()` | int truncates, round rounds (banker's rounding) |
| `type()` vs `isinstance()` | type = exact, isinstance = includes inheritance |
| Safe Conversion | Use try-except to handle errors |
| `ord()` / `chr()` | Character ↔ ASCII number |
| `bin()` / `oct()` / `hex()` | Number system conversions |

---

> 🚀 **What's Next?**
> 👉 Operators in Python
> 👉 Conditional Statements (if/elif/else)
> 👉 Loops (for, while)
