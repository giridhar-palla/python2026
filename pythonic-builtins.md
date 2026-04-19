# 🐍 Pythonic Built-in Functions - Complete Guide (Zero to Hero)

> Python's built-in functions let you write in **one line** what other languages need **ten lines** for. But you must understand the manual logic first.

---

# 1️⃣ Iteration Superpowers

---

## 🔹 enumerate() — Index + Value Together

### 🧠 Analogy

> 👉 Imagine a teacher calling attendance. Without `enumerate`, the teacher reads names and manually counts "1... 2... 3...". With `enumerate`, the attendance sheet already has numbers printed next to each name.

### 🔸 Concept

`enumerate()` gives you both the **index** and the **value** while looping — no manual counter needed.

### 🔸 Manual Way (Raw Loop with Counter)

```python
fruits = ["apple", "banana", "cherry"]
i = 0

while i < len(fruits):
    print(f"{i}: {fruits[i]}")
    i = i + 1
```

Output:
```
0: apple
1: banana
2: cherry
```

### 🔸 Pythonic Way — enumerate()

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

Same output — cleaner code, no manual counter.

### 🔸 Custom Start Index

```python
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")
```

Output:
```
1. apple
2. banana
3. cherry
```

### 🔸 Common Trap ⚠️

```python
# ❌ Flipped order — index and value swapped!
for fruit, index in enumerate(fruits):
    print(f"{index}: {fruit}")
# "index" is actually the value, "fruit" is actually the index!

# ✅ Always: index first, value second
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

🧠 `enumerate()` yields `(index, value)` — always in **that order**.

---

## 🔹 zip() — Loop Multiple Sequences Together

### 🧠 Analogy

> 👉 Think of a **zipper** on a jacket — it joins two sides together, tooth by tooth, in parallel.

### 🔸 Concept

`zip()` pairs up items from two (or more) sequences, element by element.

### 🔸 Manual Way (Using Index)

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

i = 0
while i < len(names):
    print(f"{names[i]} is {ages[i]} years old")
    i = i + 1
```

### 🔸 Pythonic Way — zip()

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

for name, age in zip(names, ages):
    print(f"{name} is {age} years old")
```

### 🔸 zip() with Three or More Sequences

```python
names = ["Alice", "Bob"]
ages = [25, 30]
cities = ["Delhi", "Mumbai"]

for name, age, city in zip(names, ages, cities):
    print(f"{name}, {age}, {city}")
```

### 🔸 Common Trap: zip() Stops at the SHORTEST ⚠️

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30]

for name, age in zip(names, ages):
    print(f"{name}: {age}")
```

Output:
```
Alice: 25
Bob: 30
```

✔ "Charlie" is **silently dropped** because `ages` ran out first.

### 🔸 Fix: Use `itertools.zip_longest`

```python
from itertools import zip_longest

names = ["Alice", "Bob", "Charlie"]
ages = [25, 30]

for name, age in zip_longest(names, ages, fillvalue="Unknown"):
    print(f"{name}: {age}")
```

Output:
```
Alice: 25
Bob: 30
Charlie: Unknown
```

### 🔸 Unzipping with zip()

```python
pairs = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]

names, ages = zip(*pairs)
print(names)   # ('Alice', 'Bob', 'Charlie')
print(ages)    # (25, 30, 35)
```

🧠 `zip(*pairs)` unpacks the list of tuples and re-zips them by column.

---

## 🔹 reversed() — Safe Backward Iteration

### 🧠 Analogy

> 👉 Like reading a book **from the last page to the first** — the book itself doesn't change, you just read it backwards.

### 🔸 Concept

`reversed()` lets you iterate backwards **without modifying** the original sequence.

### 🔸 Manual Way (Backward Index)

```python
nums = [10, 20, 30, 40, 50]
i = len(nums) - 1

while i >= 0:
    print(nums[i])
    i = i - 1
```

### 🔸 Pythonic Way — reversed()

```python
nums = [10, 20, 30, 40, 50]

for num in reversed(nums):
    print(num)
```

### 🔸 reversed() Does NOT Modify the Original

```python
nums = [1, 2, 3, 4, 5]

for num in reversed(nums):
    print(num, end=" ")   # 5 4 3 2 1

print()
print(nums)   # [1, 2, 3, 4, 5]  ← unchanged!
```

### 🔸 reversed() vs [::-1]

| | `reversed()` | `[::-1]` |
|---|---|---|
| Creates new list? | ❌ No (returns iterator) | ✅ Yes (new list/string) |
| Memory | Efficient — iterates without copying | Uses extra memory for the copy |
| Works on | Lists, tuples, ranges, strings | Lists, tuples, strings |

```python
nums = [1, 2, 3, 4, 5]

# reversed() — memory efficient, no new list
for num in reversed(nums):
    print(num)

# [::-1] — creates a brand new list in memory
new_list = nums[::-1]
```

✔ Use `reversed()` when you just need to **iterate**. Use `[::-1]` when you need a **new reversed copy**.

---

# 2️⃣ Functional Programming Tools (Highly Tested 🔥)

---

## 🔹 map() — Apply a Function to Every Item

### 🧠 Analogy

> 👉 Like a **factory assembly line** — every item goes through the same machine (function) and comes out transformed.

### 🔸 Concept

`map()` applies a function to **every item** in a sequence and returns the results.

### 🔸 Manual Way (Loop + Append)

```python
nums = [1, 2, 3, 4, 5]
squared = []

i = 0
while i < len(nums):
    squared.append(nums[i] * nums[i])
    i = i + 1

print(squared)   # [1, 4, 9, 16, 25]
```

### 🔸 Pythonic Way — map()

```python
nums = [1, 2, 3, 4, 5]

squared = list(map(lambda x: x * x, nums))
print(squared)   # [1, 4, 9, 16, 25]
```

### 🔸 map() with a Named Function

```python
def double(n):
    return n * 2

nums = [1, 2, 3, 4, 5]
result = list(map(double, nums))
print(result)   # [2, 4, 6, 8, 10]
```

### 🔸 map() with Multiple Sequences

```python
a = [1, 2, 3]
b = [10, 20, 30]

result = list(map(lambda x, y: x + y, a, b))
print(result)   # [11, 22, 33]
```

### 🔸 Common Use: Convert Types

```python
str_nums = ["1", "2", "3", "4"]

# Manual way
int_nums = []
for s in str_nums:
    int_nums.append(int(s))

# Pythonic way
int_nums = list(map(int, str_nums))
print(int_nums)   # [1, 2, 3, 4]
```

### 🔸 Common Trap: map() Returns an Iterator ⚠️

```python
result = map(str, [1, 2, 3])
print(result)        # <map object at 0x...>  ← NOT a list!
print(list(result))  # ['1', '2', '3']       ← wrap with list()
```

---

## 🔹 filter() — Keep Items That Match a Condition

### 🧠 Analogy

> 👉 Like a **coffee filter** — it lets the good stuff through and blocks the rest.

### 🔸 Concept

`filter()` keeps only the items where the function returns `True`.

### 🔸 Manual Way (Loop + If + Append)

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = []

i = 0
while i < len(nums):
    if nums[i] % 2 == 0:
        evens.append(nums[i])
    i = i + 1

print(evens)   # [2, 4, 6, 8, 10]
```

### 🔸 Pythonic Way — filter()

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)   # [2, 4, 6, 8, 10]
```

### 🔸 filter() with None — Remove Falsy Values

```python
data = [0, 1, "", "hello", None, 42, [], [1, 2], False, True]

truthy = list(filter(None, data))
print(truthy)   # [1, 'hello', 42, [1, 2], True]
```

🧠 Passing `None` as the function keeps only **truthy** values.

### 🔸 Common Trap: filter() Also Returns an Iterator ⚠️

```python
result = filter(lambda x: x > 3, [1, 2, 3, 4, 5])
print(result)        # <filter object at 0x...>
print(list(result))  # [4, 5]
```

---

## 🔹 reduce() — Reduce All Items to a Single Value

### 🧠 Analogy

> 👉 Like a **snowball rolling downhill** — it picks up each item and accumulates into one big result.

### 🔸 Concept

`reduce()` takes a function and applies it **cumulatively** to the items, reducing the sequence to a single value.

⚠️ `reduce()` is in the `functools` module — must import it.

### 🔸 Manual Way (Cumulative Loop)

```python
nums = [1, 2, 3, 4, 5]
product = 1

i = 0
while i < len(nums):
    product = product * nums[i]
    i = i + 1

print(f"Product: {product}")   # Product: 120
```

### 🔸 Pythonic Way — reduce()

```python
from functools import reduce

nums = [1, 2, 3, 4, 5]

product = reduce(lambda a, b: a * b, nums)
print(f"Product: {product}")   # Product: 120
```

🧠 Step by step:
```
Step 1: a=1, b=2 → 1*2 = 2
Step 2: a=2, b=3 → 2*3 = 6
Step 3: a=6, b=4 → 6*4 = 24
Step 4: a=24, b=5 → 24*5 = 120
```

### 🔸 reduce() with Initial Value

```python
from functools import reduce

nums = [1, 2, 3]
result = reduce(lambda a, b: a + b, nums, 100)
print(result)   # 106  (starts from 100, then adds 1+2+3)
```

### 🔸 When to Use reduce() vs Built-ins

```python
# For sum — use sum(), not reduce
print(sum([1, 2, 3, 4, 5]))   # 15  ✅ cleaner

# For product — reduce is appropriate (no built-in product)
from functools import reduce
print(reduce(lambda a, b: a * b, [1, 2, 3, 4, 5]))   # 120

# Python 3.8+ has math.prod
import math
print(math.prod([1, 2, 3, 4, 5]))   # 120  ✅ even cleaner
```

---

# 3️⃣ Boolean Aggregators

---

## 🔹 any() — Is At Least ONE Item True?

### 🔸 Manual Way

```python
nums = [0, 0, 0, 1, 0]
found_truthy = False

for num in nums:
    if num:
        found_truthy = True
        break

print(found_truthy)   # True
```

### 🔸 Pythonic Way

```python
print(any([0, 0, 0, 1, 0]))     # True   (at least one truthy)
print(any([0, 0, 0, 0, 0]))     # False  (all falsy)
print(any([]))                    # False  (empty = nothing is true)
```

### 🔸 any() with Conditions

```python
nums = [1, 3, 5, 7, 8, 9]

has_even = any(n % 2 == 0 for n in nums)
print(has_even)   # True  (8 is even)
```

---

## 🔹 all() — Are ALL Items True?

### 🔸 Manual Way

```python
nums = [1, 2, 3, 4, 5]
all_positive = True

for num in nums:
    if num <= 0:
        all_positive = False
        break

print(all_positive)   # True
```

### 🔸 Pythonic Way

```python
print(all([1, 2, 3, 4, 5]))     # True   (all truthy)
print(all([1, 0, 3, 4, 5]))     # False  (0 is falsy)
print(all([]))                    # True   (empty = vacuously true)
```

### 🔸 all() with Conditions

```python
nums = [2, 4, 6, 8]

all_even = all(n % 2 == 0 for n in nums)
print(all_even)   # True
```

### 🔸 any() vs all() Summary

| Function | Returns True When | Empty List |
|----------|------------------|:---:|
| `any()` | At least one item is truthy | `False` |
| `all()` | Every item is truthy | `True` |

---

# 4️⃣ Advanced Sorting

---

## 🔹 sorted() — Create a New Sorted List

### 🔸 Manual Way (Bubble Sort)

```python
nums = [64, 34, 25, 12, 22, 11, 90]
temp = list(nums)   # work on a copy

i = 0
while i < len(temp):
    j = 0
    while j < len(temp) - 1 - i:
        if temp[j] > temp[j + 1]:
            temp[j], temp[j + 1] = temp[j + 1], temp[j]
        j = j + 1
    i = i + 1

print(temp)   # [11, 12, 22, 25, 34, 64, 90]
print(nums)   # [64, 34, 25, 12, 22, 11, 90]  ← original unchanged
```

### 🔸 Pythonic Way — sorted()

```python
nums = [64, 34, 25, 12, 22, 11, 90]

result = sorted(nums)
print(result)   # [11, 12, 22, 25, 34, 64, 90]
print(nums)     # [64, 34, 25, 12, 22, 11, 90]  ← original unchanged
```

### 🔸 Reverse Sort

```python
print(sorted(nums, reverse=True))   # [90, 64, 34, 25, 22, 12, 11]
```

### 🔸 The `key` Parameter (CRUCIAL FOR INTERVIEWS 🔥)

The `key` parameter tells `sorted()` **what to sort by**.

#### Sort Strings by Length

```python
words = ["banana", "pie", "apple", "kiwi"]

# Manual way — Bubble Sort by length
temp = list(words)
i = 0
while i < len(temp):
    j = 0
    while j < len(temp) - 1 - i:
        if len(temp[j]) > len(temp[j + 1]):
            temp[j], temp[j + 1] = temp[j + 1], temp[j]
        j = j + 1
    i = i + 1

print(temp)   # ['pie', 'kiwi', 'apple', 'banana']

# Pythonic way
print(sorted(words, key=len))   # ['pie', 'kiwi', 'apple', 'banana']
```

#### Sort Dictionaries by a Specific Value

```python
students = [
    {"name": "Charlie", "age": 20},
    {"name": "Alice", "age": 25},
    {"name": "Bob", "age": 22}
]

# Manual way — Bubble Sort by age
temp = list(students)
i = 0
while i < len(temp):
    j = 0
    while j < len(temp) - 1 - i:
        if temp[j]["age"] > temp[j + 1]["age"]:
            temp[j], temp[j + 1] = temp[j + 1], temp[j]
        j = j + 1
    i = i + 1

for s in temp:
    print(s)

# Pythonic way
sorted_students = sorted(students, key=lambda x: x["age"])
for s in sorted_students:
    print(s)
```

Output:
```
{'name': 'Charlie', 'age': 20}
{'name': 'Bob', 'age': 22}
{'name': 'Alice', 'age': 25}
```

#### Sort by Multiple Criteria

```python
students = [
    {"name": "Alice", "grade": 90},
    {"name": "Bob", "grade": 90},
    {"name": "Charlie", "grade": 85}
]

# Sort by grade (descending), then by name (ascending)
result = sorted(students, key=lambda x: (-x["grade"], x["name"]))

for s in result:
    print(s)
```

Output:
```
{'name': 'Alice', 'grade': 90}
{'name': 'Bob', 'grade': 90}
{'name': 'Charlie', 'grade': 85}
```

### 🔸 sorted() vs .sort() Reminder

| | `sorted()` | `.sort()` |
|---|---|---|
| Returns | New sorted list | `None` |
| Modifies original | ❌ | ✅ |
| Works on | Any iterable | Lists only |

---

# 5️⃣ Object Introspection (Debugging Superpowers 🔥)

---

## 🔹 isinstance() — Safe Type Checking

### 🔸 Why Not `type(x) == y`?

```python
# type() doesn't handle inheritance
x = True

print(type(x) == int)        # False  (type is bool, not int)
print(type(x) == bool)       # True

# isinstance() handles inheritance correctly
print(isinstance(x, int))    # True   (bool IS a subclass of int)
print(isinstance(x, bool))   # True
```

### 🔸 Check Multiple Types

```python
x = 3.14

print(isinstance(x, (int, float)))   # True  (is it int OR float?)
```

✔ **Always use `isinstance()` over `type() ==`** — it respects inheritance.

---

## 🔹 dir() — See All Available Methods

### 🧠 Analogy

> 👉 Like opening the **table of contents** of a book — you see everything that's available.

```python
text = "hello"
print(dir(text))
```

Output (truncated):
```
['__add__', '__class__', ..., 'capitalize', 'count', 'endswith', 'find',
 'format', 'index', 'isalpha', 'isdigit', 'join', 'lower', 'replace',
 'split', 'strip', 'upper', ...]
```

### 🔸 Filter Out Dunder Methods

```python
text = "hello"
methods = [m for m in dir(text) if not m.startswith("_")]
print(methods)
```

✔ `dir()` is your **best friend** when you forget what methods an object has. Use it in the interactive shell constantly.

---

## 🔹 id() — Memory Address

```python
a = [1, 2, 3]
b = a          # b points to the SAME object
c = a.copy()   # c is a NEW object

print(id(a))   # 140234567890
print(id(b))   # 140234567890  ← same as a!
print(id(c))   # 140234567999  ← different!

print(a is b)  # True   (same object)
print(a is c)  # False  (different objects)
```

✔ `id()` proves whether two variables point to the **same object** or different ones.

---

## 🔹 hasattr(), getattr(), setattr() — Dynamic Attribute Access

### 🔸 hasattr() — Check if Attribute Exists

```python
class Person:
    def __init__(self, name):
        self.name = name

p = Person("Giridhar")

print(hasattr(p, "name"))    # True
print(hasattr(p, "email"))   # False
```

### 🔸 getattr() — Get Attribute Safely

```python
# ❌ Direct access — crashes if missing
# print(p.email)   # AttributeError

# ✅ Safe access with default
print(getattr(p, "name", "Unknown"))    # Giridhar
print(getattr(p, "email", "Unknown"))   # Unknown  (no error!)
```

### 🔸 setattr() — Set Attribute Dynamically

```python
setattr(p, "email", "giri@email.com")
print(p.email)   # giri@email.com
```

### 🔸 Real-World Use: Dynamic Configuration

```python
class Config:
    pass

config = Config()
settings = {"debug": True, "port": 8080, "host": "localhost"}

for key, value in settings.items():
    setattr(config, key, value)

print(config.debug)   # True
print(config.port)    # 8080
print(config.host)    # localhost
```

---

# 6️⃣ Math Built-ins

---

## 🔹 abs() — Absolute Value

```python
print(abs(-5))      # 5
print(abs(5))       # 5
print(abs(-3.14))   # 3.14
```

### Manual way:

```python
num = -5
if num < 0:
    result = num * -1
else:
    result = num
print(result)   # 5

# Pythonic
print(abs(-5))   # 5
```

---

## 🔹 sum() — Sum of All Items

```python
nums = [1, 2, 3, 4, 5]
```

### Manual way:

```python
total = 0
i = 0
while i < len(nums):
    total = total + nums[i]
    i = i + 1
print(total)   # 15
```

### Pythonic way:

```python
print(sum(nums))          # 15
print(sum(nums, 100))     # 115  (start from 100)
```

---

## 🔹 round() — Round a Number

```python
print(round(3.14159))       # 3
print(round(3.14159, 2))    # 3.14
print(round(3.14159, 4))    # 3.1416
```

### ⚠️ Banker's Rounding Trap (INTERVIEW 🔥)

```python
print(round(0.5))   # 0   ← NOT 1!
print(round(1.5))   # 2
print(round(2.5))   # 2   ← NOT 3!
print(round(3.5))   # 4
```

🧠 Python rounds `.5` to the **nearest even number**. This is called **Banker's Rounding**.

---

## 🔹 divmod() — Division + Remainder in One Shot

```python
quotient, remainder = divmod(17, 5)
print(f"17 / 5 = {quotient} remainder {remainder}")
# 17 / 5 = 3 remainder 2
```

### Manual way:

```python
a = 17
b = 5
quotient = a // b
remainder = a % b
print(f"{a} / {b} = {quotient} remainder {remainder}")
```

### Pythonic way:

```python
q, r = divmod(17, 5)
```

### 🔸 Practical Use: Convert Seconds to Minutes

```python
total_seconds = 3725

minutes, seconds = divmod(total_seconds, 60)
hours, minutes = divmod(minutes, 60)

print(f"{hours}h {minutes}m {seconds}s")   # 1h 2m 5s
```

---

# 📌 Complete Summary — Quick Cheat Sheet

| Function | What It Does | Manual Equivalent |
|----------|-------------|-------------------|
| `enumerate(seq)` | Index + value in loop | `i = 0; while i < len(seq)` |
| `zip(a, b)` | Pair items from sequences | `for i in range(len(a))` |
| `reversed(seq)` | Iterate backwards (no copy) | `i = len(seq) - 1; while i >= 0` |
| `map(func, seq)` | Apply function to all items | `for x in seq: result.append(func(x))` |
| `filter(func, seq)` | Keep items where func is True | `for x in seq: if func(x): result.append(x)` |
| `reduce(func, seq)` | Accumulate to single value | `acc = seq[0]; for x in seq[1:]` |
| `any(seq)` | At least one truthy? | `for x: if x: return True` |
| `all(seq)` | All truthy? | `for x: if not x: return False` |
| `sorted(seq)` | New sorted list | Bubble sort loop |
| `sorted(key=...)` | Sort by custom criteria | Bubble sort with custom comparison |
| `isinstance(x, T)` | Safe type check (with inheritance) | `type(x) == T` (unsafe) |
| `dir(obj)` | List all methods/attributes | No equivalent |
| `id(obj)` | Memory address | No equivalent |
| `hasattr(obj, name)` | Check if attribute exists | `try: obj.name except AttributeError` |
| `getattr(obj, name, default)` | Safe attribute access | `if hasattr: obj.name else: default` |
| `setattr(obj, name, val)` | Set attribute dynamically | `obj.name = val` |
| `abs(n)` | Absolute value | `if n < 0: n * -1` |
| `sum(seq)` | Sum all items | `total = 0; for x: total += x` |
| `round(n, digits)` | Round number | Manual math |
| `divmod(a, b)` | Quotient + remainder | `a // b, a % b` |

---

> 🚀 Use this as your **interview quick-reference** for Python's most powerful built-in tools!
