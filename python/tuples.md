# 📌 Tuples in Python - Complete Guide (Zero to Hero)

> A tuple is an **ordered, immutable collection** that allows **duplicates**.

---

## 🔹 What is a Tuple?

A tuple is like a list, but **you cannot change it** after creation. Once created, items cannot be added, removed, or modified.

### 🧠 Real-World Analogy

> 👉 Think of a tuple like a **birth certificate**:
> - The information is **fixed** — your name, date of birth, place of birth
> - You can **read** it anytime
> - But you **cannot change** it after it's issued
>
> A list is like a **to-do list** (changeable). A tuple is like a **birth certificate** (permanent).

---

## 🔹 Creating Tuples

### 🔸 Using Parentheses `()`

```python
# Empty tuple
empty = ()

# Tuple of integers
numbers = (1, 2, 3, 4, 5)

# Tuple of strings
fruits = ("apple", "banana", "cherry")

# Mixed types
mixed = (1, "hello", 3.14, True, None)

# Nested tuple
nested = ((1, 2), (3, 4), (5, 6))
```

### 🔸 Without Parentheses (Tuple Packing)

```python
# Parentheses are optional!
numbers = 1, 2, 3, 4, 5
print(numbers)        # (1, 2, 3, 4, 5)
print(type(numbers))  # <class 'tuple'>
```

✔ Python recognizes comma-separated values as a tuple even without parentheses. This is called **tuple packing**.

### 🔸 Single Element Tuple (VERY IMPORTANT ⚠️)

```python
# ❌ This is NOT a tuple — it's just an integer in parentheses
not_a_tuple = (5)
print(type(not_a_tuple))   # <class 'int'>

# ✅ This IS a tuple — note the trailing comma
single_tuple = (5,)
print(type(single_tuple))  # <class 'tuple'>

# Also works without parentheses
single_tuple = 5,
print(type(single_tuple))  # <class 'tuple'>
```

🧠 **The comma makes the tuple, not the parentheses!** This is one of the most common Python gotchas.

### 🔸 Using `tuple()` Constructor

```python
# From a list
nums = tuple([1, 2, 3])
print(nums)   # (1, 2, 3)

# From a string
chars = tuple("Python")
print(chars)   # ('P', 'y', 't', 'h', 'o', 'n')

# From a range
nums = tuple(range(5))
print(nums)   # (0, 1, 2, 3, 4)

# From a set (order may vary)
nums = tuple({3, 1, 2})
print(nums)   # (1, 2, 3)
```

---

## 🔹 Tuple Characteristics

| Property | Value |
|----------|-------|
| Ordered | ✅ Items have a fixed position |
| Immutable | ✅ Cannot add, remove, or change items |
| Allows Duplicates | ✅ Same value can appear multiple times |
| Allows Mixed Types | ✅ Can hold int, str, bool, etc. together |
| Indexed | ✅ Access items by position (starting from 0) |
| Hashable | ✅ Can be used as dictionary keys and set elements |

---

## 🔹 Accessing Items (Indexing)

Works exactly like lists.

```python
fruits = ("apple", "banana", "cherry", "date", "elderberry")
```

### 🔸 Positive Indexing

```python
print(fruits[0])   # apple
print(fruits[1])   # banana
print(fruits[4])   # elderberry
```

### 🔸 Negative Indexing

```python
print(fruits[-1])   # elderberry  (last item)
print(fruits[-2])   # date
print(fruits[-5])   # apple       (first item)
```

### 🔸 Index Out of Range

```python
print(fruits[10])   # ❌ IndexError: tuple index out of range
```

---

## 🔹 Tuple Slicing

Works exactly like list slicing.

```python
nums = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)

print(nums[2:6])     # (2, 3, 4, 5)
print(nums[:4])       # (0, 1, 2, 3)
print(nums[5:])       # (5, 6, 7, 8, 9)
print(nums[::2])      # (0, 2, 4, 6, 8)
print(nums[::-1])     # (9, 8, 7, 6, 5, 4, 3, 2, 1, 0)
```

✔ Slicing a tuple returns a **new tuple**.

---

## 🔹 Tuple Length

```python
fruits = ("apple", "banana", "cherry")
print(len(fruits))   # 3
```

---

## 🔹 Tuple Immutability (VERY IMPORTANT 🔥)

> 👉 Tuples **cannot be changed** after creation.

```python
fruits = ("apple", "banana", "cherry")

# ❌ Cannot change an item
fruits[0] = "avocado"   # TypeError: 'tuple' object does not support item assignment

# ❌ Cannot add items
fruits.append("date")   # AttributeError: 'tuple' object has no attribute 'append'

# ❌ Cannot remove items
del fruits[0]            # TypeError: 'tuple' object doesn't support item deletion
```

### 🔸 But Wait — Mutable Objects INSIDE a Tuple CAN Change! ⚠️

```python
# Tuple containing a list
data = (1, 2, [3, 4, 5])

# ❌ Cannot replace the list itself
# data[2] = [6, 7, 8]   # TypeError

# ✅ But CAN modify the list's contents!
data[2][0] = 99
print(data)   # (1, 2, [99, 4, 5])

data[2].append(6)
print(data)   # (1, 2, [99, 4, 5, 6])
```

🧠 The tuple holds a **reference** to the list. The reference doesn't change (tuple is immutable), but the list object itself can be modified (list is mutable).

This is a **very common interview question**.

### 🔸 Workaround: Convert to List, Modify, Convert Back

```python
fruits = ("apple", "banana", "cherry")

# Convert to list
temp = list(fruits)

# Modify
temp[0] = "avocado"
temp.append("date")

# Convert back to tuple
fruits = tuple(temp)
print(fruits)   # ('avocado', 'banana', 'cherry', 'date')
```

⚠️ This creates a **new tuple**. The original is not modified (because tuples are immutable).

---

## 🔹 Tuple Unpacking (VERY IMPORTANT 🔥)

### 🔸 Basic Unpacking

```python
point = (10, 20)
x, y = point

print(x)   # 10
print(y)   # 20
```

```python
person = ("Giridhar", 25, "Hyderabad")
name, age, city = person

print(name)   # Giridhar
print(age)    # 25
print(city)   # Hyderabad
```

### 🔸 Count Must Match

```python
# ❌ Too many values
a, b = (1, 2, 3)       # ValueError: too many values to unpack

# ❌ Not enough values
a, b, c = (1, 2)       # ValueError: not enough values to unpack
```

### 🔸 `*` Splat Unpacking — Catch Extra Items

```python
first, *rest = (1, 2, 3, 4, 5)
print(first)   # 1
print(rest)    # [2, 3, 4, 5]  ← note: rest is a LIST, not tuple

first, *middle, last = (1, 2, 3, 4, 5)
print(first)    # 1
print(middle)   # [2, 3, 4]
print(last)     # 5
```

### 🔸 Ignoring Values with `_`

```python
name, _, city = ("Giridhar", 25, "Hyderabad")
print(name)   # Giridhar
print(city)   # Hyderabad
# age is ignored
```

✔ `_` is a convention for "I don't care about this value."

### 🔸 Swap Variables Using Tuple Unpacking

```python
a = 10
b = 20

a, b = b, a   # tuple packing + unpacking in one line

print(a)   # 20
print(b)   # 10
```

🧠 The right side `b, a` creates a tuple `(20, 10)`, then it's unpacked into `a, b`.

### 🔸 Unpacking in Loops

```python
points = [(1, 2), (3, 4), (5, 6)]

for x, y in points:
    print(f"x={x}, y={y}")
```

Output:
```
x=1, y=2
x=3, y=4
x=5, y=6
```

```python
students = [("Alice", 90), ("Bob", 85), ("Charlie", 92)]

for name, score in students:
    print(f"{name}: {score}")
```

---

## 🔹 Tuple Methods

Tuples have only **2 methods** (because they're immutable — no add/remove/sort).

### 🔸 count() — Count Occurrences

```python
nums = (1, 2, 3, 2, 1, 2)
print(nums.count(2))   # 3
print(nums.count(5))   # 0
```

### 🔸 index() — Find Position of First Occurrence

```python
nums = (10, 20, 30, 20, 40)
print(nums.index(20))   # 1  (first occurrence)
print(nums.index(40))   # 4
```

⚠️ If not found:

```python
nums.index(99)   # ❌ ValueError: tuple.index(x): x is not in tuple
```

### 🔸 That's It — Only 2 Methods!

Compare with lists:

| | List Methods | Tuple Methods |
|---|:---:|:---:|
| Count | `count()` | `count()` |
| Find | `index()` | `index()` |
| Add | `append()`, `extend()`, `insert()` | ❌ |
| Remove | `remove()`, `pop()`, `clear()` | ❌ |
| Sort | `sort()`, `reverse()` | ❌ |
| Copy | `copy()` | ❌ |

---

## 🔹 Tuple Operations

### 🔸 Concatenation with `+`

```python
a = (1, 2, 3)
b = (4, 5, 6)
c = a + b
print(c)   # (1, 2, 3, 4, 5, 6)
```

✔ Creates a **new tuple**. Originals unchanged.

### 🔸 Repetition with `*`

```python
t = (0,) * 5
print(t)   # (0, 0, 0, 0, 0)

pattern = (1, 2) * 3
print(pattern)   # (1, 2, 1, 2, 1, 2)
```

### 🔸 Membership with `in`

```python
fruits = ("apple", "banana", "cherry")

print("banana" in fruits)       # True
print("grape" not in fruits)    # True
```

---

## 🔹 Iterating Through Tuples

### 🔸 Using while loop

```python
fruits = ("apple", "banana", "cherry")
i = 0

while i < len(fruits):
    print(fruits[i])
    i = i + 1
```

### 🔸 Using for loop

```python
for fruit in fruits:
    print(fruit)
```

### 🔸 With enumerate()

```python
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

---

## 🔹 Tuple vs List (INTERVIEW FAVORITE 🔥)

| Feature | List | Tuple |
|---------|------|-------|
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` |
| Mutable? | ✅ Yes | ❌ No |
| Methods | 11 methods | 2 methods |
| Speed | Slower | Faster |
| Memory | More memory | Less memory |
| As dict key? | ❌ No (unhashable) | ✅ Yes (hashable) |
| As set element? | ❌ No | ✅ Yes |
| Use when | Data changes | Data is fixed |

### 🔸 Speed Comparison

```python
import sys

my_list = [1, 2, 3, 4, 5]
my_tuple = (1, 2, 3, 4, 5)

print(sys.getsizeof(my_list))    # 104 bytes (approx)
print(sys.getsizeof(my_tuple))   # 80 bytes (approx)
```

✔ Tuples use **less memory** than lists because Python doesn't need to allocate extra space for potential modifications.

### 🔸 Tuples as Dictionary Keys

```python
# ✅ Tuple as key (immutable → hashable)
locations = {
    (28.6139, 77.2090): "Delhi",
    (19.0760, 72.8777): "Mumbai"
}

print(locations[(28.6139, 77.2090)])   # Delhi

# ❌ List as key (mutable → unhashable)
locations = {
    [28.6139, 77.2090]: "Delhi"   # TypeError: unhashable type: 'list'
}
```

### 🔸 Tuples as Set Elements

```python
# ✅ Tuples in a set
points = {(1, 2), (3, 4), (1, 2)}
print(points)   # {(1, 2), (3, 4)}  ← duplicate removed

# ❌ Lists in a set
points = {[1, 2], [3, 4]}   # TypeError: unhashable type: 'list'
```

---

## 🔹 When to Use Tuples?

| Use Case | Why Tuple? |
|----------|-----------|
| Function returning multiple values | `return x, y` returns a tuple |
| Dictionary keys | Only immutable types allowed |
| Fixed configuration data | Coordinates, RGB colors, database records |
| Protecting data from modification | Prevents accidental changes |
| Iterating over constant data | Slightly faster than lists |
| Unpacking | `x, y = point` |

### 🔸 Real-World Examples

```python
# Coordinates
location = (28.6139, 77.2090)

# RGB Color
red = (255, 0, 0)
green = (0, 255, 0)

# Database record
employee = ("Giridhar", "Developer", 50000)

# Function returning multiple values
def get_dimensions():
    return 1920, 1080   # returns a tuple

width, height = get_dimensions()
print(f"{width}x{height}")   # 1920x1080

# Days of the week (shouldn't change)
DAYS = ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")
```

---

## 🔹 Named Tuples (IMPORTANT 🔥)

Regular tuples access items by **index** which is hard to read. Named tuples let you access by **name**.

### 🔸 The Problem with Regular Tuples

```python
person = ("Giridhar", 25, "Hyderabad")

# What is person[0]? person[1]? Hard to remember!
print(person[0])   # Giridhar
print(person[1])   # 25
```

### 🔸 Named Tuple — Access by Name

```python
from collections import namedtuple

# Define a named tuple type
Person = namedtuple("Person", ["name", "age", "city"])

# Create an instance
person = Person(name="Giridhar", age=25, city="Hyderabad")

# Access by name (readable!)
print(person.name)   # Giridhar
print(person.age)    # 25
print(person.city)   # Hyderabad

# Still works by index too
print(person[0])     # Giridhar
```

### 🔸 Named Tuple is Still Immutable

```python
person.age = 26   # ❌ AttributeError: can't set attribute
```

### 🔸 Named Tuple Methods

```python
# Convert to dictionary
print(person._asdict())   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}

# Create a modified copy (returns NEW named tuple)
older = person._replace(age=26)
print(older)   # Person(name='Giridhar', age=26, city='Hyderabad')
print(person)  # Person(name='Giridhar', age=25, city='Hyderabad')  ← original unchanged
```

### 🔸 Named Tuple vs Dictionary vs Class

| Feature | Named Tuple | Dictionary | Class |
|---------|:-----------:|:----------:|:-----:|
| Access by name | ✅ | ✅ | ✅ |
| Immutable | ✅ | ❌ | ❌ |
| Memory efficient | ✅ | ❌ | ❌ |
| Hashable | ✅ | ❌ | Depends |
| Easy to create | ✅ | ✅ | ❌ |

### 🔸 Modern Alternative: typing.NamedTuple (Python 3.6+)

The modern way to define named tuples uses `typing.NamedTuple` with **type hints** and a class-like syntax:

```python
from typing import NamedTuple

class Person(NamedTuple):
    name: str
    age: int
    city: str

person = Person(name="Giridhar", age=25, city="Hyderabad")

print(person.name)   # Giridhar
print(person.age)    # 25
print(person[0])     # Giridhar  (still works by index)
```

✔ Same behavior as `collections.namedtuple`, but with **type hints** built in and a cleaner class-style definition. Preferred in modern codebases.

---

## 🔹 Tuple Comprehension? — No! It's a Generator

```python
# This looks like a tuple comprehension, but it's NOT
result = (x * x for x in range(5))
print(result)        # <generator object ...>
print(type(result))  # <class 'generator'>

# To get a tuple, wrap with tuple()
result = tuple(x * x for x in range(5))
print(result)   # (0, 1, 4, 9, 16)
```

✔ Python has list comprehensions `[...]`, dict comprehensions `{k:v ...}`, set comprehensions `{...}`, but **no tuple comprehension**. `(...)` creates a **generator expression**.

---

## 🔹 Built-in Functions with Tuples

```python
nums = (3, 1, 4, 1, 5, 9, 2, 6)

print(len(nums))      # 8
print(sum(nums))      # 31
print(min(nums))      # 1
print(max(nums))      # 9
print(sorted(nums))   # [1, 1, 2, 3, 4, 5, 6, 9]  ← returns a LIST, not tuple!

# To get a sorted tuple
print(tuple(sorted(nums)))   # (1, 1, 2, 3, 4, 5, 6, 9)
```

### 🔸 any() and all()

```python
print(any((0, 0, 1)))    # True   (at least one truthy)
print(all((1, 2, 3)))    # True   (all truthy)
print(all((0, 1, 2)))    # False  (0 is falsy)
```

---

## 🔹 Converting Between Tuples and Lists

```python
# List to Tuple
my_list = [1, 2, 3]
my_tuple = tuple(my_list)
print(my_tuple)   # (1, 2, 3)

# Tuple to List
my_tuple = (1, 2, 3)
my_list = list(my_tuple)
print(my_list)   # [1, 2, 3]
```

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Forgetting the Comma for Single-Element Tuple

```python
# ❌ Not a tuple
t = (5)
print(type(t))   # <class 'int'>

# ✅ Tuple
t = (5,)
print(type(t))   # <class 'tuple'>
```

### 🔸 Mistake 2: Trying to Modify a Tuple

```python
t = (1, 2, 3)
t[0] = 10   # ❌ TypeError
```

### 🔸 Mistake 3: Assuming Tuple Contents Are Always Immutable

```python
t = (1, [2, 3], 4)
t[1].append(99)
print(t)   # (1, [2, 3, 99], 4)  ← the list inside changed!
```

### 🔸 Mistake 4: sorted() Returns a List, Not a Tuple

```python
t = (3, 1, 2)
result = sorted(t)
print(type(result))   # <class 'list'>  ← not a tuple!

# ✅ Wrap with tuple()
result = tuple(sorted(t))
```

### 🔸 Mistake 5: Unpacking Count Mismatch

```python
point = (1, 2, 3)
x, y = point   # ❌ ValueError: too many values to unpack

# ✅ Use * to catch extras
x, *rest = point
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Find the Largest Element in a Tuple

#### Manual way:

```python
nums = (3, 7, 2, 9, 4)
largest = nums[0]

i = 1
while i < len(nums):
    if nums[i] > largest:
        largest = nums[i]
    i = i + 1

print(f"Largest: {largest}")   # Largest: 9
```

#### Pythonic shortcut:

```python
print(f"Largest: {max(nums)}")   # Largest: 9
```

---

### ✅ 2. Count Occurrences of an Element

#### Manual way:

```python
nums = (1, 2, 3, 2, 1, 2, 4)
target = 2
count = 0

for num in nums:
    if num == target:
        count = count + 1

print(f"{target} appears {count} times")   # 2 appears 3 times
```

#### Pythonic shortcut:

```python
print(f"2 appears {nums.count(2)} times")   # 2 appears 3 times
```

---

### ✅ 3. Reverse a Tuple

#### Manual way:

```python
nums = (1, 2, 3, 4, 5)
reversed_tuple = ()

i = len(nums) - 1
while i >= 0:
    reversed_tuple = reversed_tuple + (nums[i],)
    i = i - 1

print(reversed_tuple)   # (5, 4, 3, 2, 1)
```

⚠️ **Memory Warning:** Because tuples are immutable, `reversed_tuple = reversed_tuple + (nums[i],)` doesn't just add an item — it **copies the entire tuple to a new memory location** every single iteration. For large datasets, this destroys RAM. The standard practice is to build a list first, then convert:

```python
nums = (1, 2, 3, 4, 5)
temp = []

i = len(nums) - 1
while i >= 0:
    temp.append(nums[i])
    i = i - 1

reversed_tuple = tuple(temp)
print(reversed_tuple)   # (5, 4, 3, 2, 1)
```

#### Pythonic shortcut:

```python
print(nums[::-1])   # (5, 4, 3, 2, 1)
```

---

### ✅ 4. Check if Element Exists

#### Manual way:

```python
fruits = ("apple", "banana", "cherry")
target = "banana"
found = False

for fruit in fruits:
    if fruit == target:
        found = True
        break

if found:
    print(f"{target} found!")
else:
    print(f"{target} not found")
```

#### Pythonic shortcut:

```python
if "banana" in fruits:
    print("banana found!")
```

---

### ✅ 5. Convert Tuple of Strings to Tuple of Integers

#### Manual way:

```python
str_nums = ("10", "20", "30", "40")
int_nums = ()

for s in str_nums:
    int_nums = int_nums + (int(s),)

print(int_nums)   # (10, 20, 30, 40)
```

#### Pythonic shortcut:

```python
int_nums = tuple(int(s) for s in str_nums)
print(int_nums)   # (10, 20, 30, 40)
```

---

### ✅ 6. Find Common Elements Between Two Tuples

#### Manual way:

```python
t1 = (1, 2, 3, 4, 5)
t2 = (4, 5, 6, 7, 8)
common = ()

for item in t1:
    if item in t2:
        common = common + (item,)

print(common)   # (4, 5)
```

#### Pythonic shortcut:

```python
common = tuple(set(t1) & set(t2))
print(common)   # (4, 5)
```

---

### ✅ 7. Sort a Tuple

Since tuples are immutable, you can't sort in-place. Create a new sorted tuple.

#### Manual way (bubble sort logic):

```python
nums = (3, 1, 4, 1, 5, 9)
temp = list(nums)

i = 0
while i < len(temp):
    j = 0
    while j < len(temp) - 1 - i:
        if temp[j] > temp[j + 1]:
            temp[j], temp[j + 1] = temp[j + 1], temp[j]
        j = j + 1
    i = i + 1

sorted_tuple = tuple(temp)
print(sorted_tuple)   # (1, 1, 3, 4, 5, 9)
```

#### Pythonic shortcut:

```python
sorted_tuple = tuple(sorted(nums))
print(sorted_tuple)   # (1, 1, 3, 4, 5, 9)
```

---

### ✅ 8. Remove Duplicates from a Tuple

#### Manual way (preserving order):

```python
nums = (1, 2, 2, 3, 4, 3, 5)
unique = ()

for num in nums:
    if num not in unique:
        unique = unique + (num,)

print(unique)   # (1, 2, 3, 4, 5)
```

#### Pythonic shortcut (preserving order — Python 3.7+):

```python
unique = tuple(dict.fromkeys(nums))
print(unique)   # (1, 2, 3, 4, 5)
```

---

## 🔹 All Tuple Operations — Quick Reference 📌

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Create | `(1, 2, 3)` or `1, 2, 3` | Parentheses optional |
| Single element | `(5,)` | Trailing comma required! |
| Access | `t[0]`, `t[-1]` | Indexing |
| Slice | `t[1:3]`, `t[::-1]` | Returns new tuple |
| Length | `len(t)` | Number of items |
| Count | `t.count(x)` | Occurrences of x |
| Find | `t.index(x)` | Position of first x |
| Membership | `x in t` | Check existence |
| Concatenate | `t1 + t2` | New tuple |
| Repeat | `t * 3` | New tuple |
| Unpack | `a, b = t` | Assign to variables |
| Splat unpack | `a, *b = t` | Catch extras |
| Convert | `list(t)`, `tuple(lst)` | Between types |
| Sort | `tuple(sorted(t))` | Returns new tuple |
| Min/Max/Sum | `min(t)`, `max(t)`, `sum(t)` | Built-in functions |

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| Tuple | Ordered, immutable, allows duplicates |
| Creating | `()`, `tuple()`, comma-separated values |
| Single element | Must have trailing comma: `(5,)` |
| Immutable | Cannot add, remove, or change items |
| Mutable inside | Lists inside tuples CAN be modified |
| Indexing | Same as lists: `t[0]`, `t[-1]` |
| Slicing | Same as lists: `t[1:3]`, `t[::-1]` |
| Methods | Only 2: `count()` and `index()` |
| Unpacking | `a, b, c = tuple` |
| `*` unpacking | `first, *rest = tuple` |
| vs List | Faster, less memory, hashable |
| Dict keys | ✅ Tuples can be dict keys |
| Named tuple | Access by name: `person.name` |
| No comprehension | `(x for x in ...)` creates a generator |
| Sorting | `tuple(sorted(t))` — returns new tuple |

---

> 🚀 **Next:** Dictionaries in Python →
