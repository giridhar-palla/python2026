# 📖 Dictionaries in Python - Complete Guide (Zero to Hero)

> A dictionary is an **unordered (Python <3.7) / insertion-ordered (Python 3.7+), mutable collection** of **key-value pairs**.

---

## 🔹 What is a Dictionary?

A dictionary stores data as **key-value pairs**. Each key maps to a value, like a real dictionary maps a word to its definition.

### 🧠 Real-World Analogy

> 👉 Think of a dictionary like a **phone book**:
> - The **name** is the key
> - The **phone number** is the value
> - You look up a name to find the number
>
> `{"Giridhar": "9876543210", "Ravi": "1234567890"}`

---

## 🔹 Creating Dictionaries

### 🔸 Using Curly Braces `{}`

```python
# Empty dictionary
empty = {}

# Simple dictionary
person = {
    "name": "Giridhar",
    "age": 25,
    "city": "Hyderabad"
}

# Mixed value types
mixed = {
    "name": "Python",
    "version": 3.12,
    "is_free": True,
    "features": ["easy", "powerful"]
}
```

### 🔸 Using `dict()` Constructor

```python
# Using keyword arguments
person = dict(name="Giridhar", age=25, city="Hyderabad")
print(person)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}

# From list of tuples
pairs = [("name", "Giridhar"), ("age", 25)]
person = dict(pairs)
print(person)   # {'name': 'Giridhar', 'age': 25}

# From zip
keys = ["name", "age", "city"]
values = ["Giridhar", 25, "Hyderabad"]
person = dict(zip(keys, values))
print(person)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}
```

### 🔸 Using dict.fromkeys() — Same Value for All Keys

```python
keys = ["a", "b", "c"]
d = dict.fromkeys(keys, 0)
print(d)   # {'a': 0, 'b': 0, 'c': 0}

# Default value is None
d = dict.fromkeys(keys)
print(d)   # {'a': None, 'b': None, 'c': None}
```

⚠️ **Trap with mutable default:**

```python
# ❌ All keys share the SAME list object!
d = dict.fromkeys(["a", "b"], [])
d["a"].append(1)
print(d)   # {'a': [1], 'b': [1]}  ← both changed!

# ✅ Use a comprehension instead
d = {key: [] for key in ["a", "b"]}
d["a"].append(1)
print(d)   # {'a': [1], 'b': []}  ← only 'a' changed
```

---

## 🔹 Dictionary Characteristics

| Property | Value |
|----------|-------|
| Ordered | ✅ Insertion order preserved (Python 3.7+) |
| Mutable | ✅ Can add, remove, change items |
| Keys must be unique | ✅ Duplicate keys overwrite |
| Keys must be immutable | ✅ str, int, float, tuple (NOT list, dict, set) |
| Values can be anything | ✅ Any type, including lists, dicts, etc. |
| Indexed by key | ✅ Access by key, NOT by position |

### 🔸 Dictionary Length

```python
person = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}
print(len(person))   # 3  (3 key-value pairs)
```

### 🔸 Keys Must Be Unique

```python
d = {"a": 1, "b": 2, "a": 3}
print(d)   # {'a': 3, 'b': 2}  ← last value wins
```

### 🔸 Keys Must Be Immutable (Hashable)

```python
# ✅ Valid keys
d = {
    "name": "Python",     # string
    42: "answer",          # int
    3.14: "pi",            # float
    (1, 2): "tuple",       # tuple
    True: "yes",           # bool
}

# ❌ Invalid keys
d = {[1, 2]: "list"}      # TypeError: unhashable type: 'list'
d = {{}: "dict"}           # TypeError: unhashable type: 'dict'
```

### 🔸 Bool and Int Key Collision (INTERVIEW TRAP 🔥)

```python
d = {True: "yes", 1: "one", False: "no", 0: "zero"}
print(d)   # {True: 'one', False: 'zero'}
```

🧠 Why? Because `True == 1` and `False == 0` in Python. They're treated as the **same key**, so the later value overwrites the earlier one.

---

## 🔹 Accessing Values

### 🔸 Using Square Brackets `[]`

```python
person = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

print(person["name"])   # Giridhar
print(person["age"])    # 25
```

⚠️ If key doesn't exist:

```python
print(person["email"])   # ❌ KeyError: 'email'
```

### 🔸 Using `get()` — Safe Access (IMPORTANT 🔥)

```python
print(person.get("name"))     # Giridhar
print(person.get("email"))    # None  (no error!)
print(person.get("email", "Not found"))   # Not found  (custom default)
```

### 🔸 `[]` vs `get()` (INTERVIEW FAVORITE 🔥)

| Method | Key Missing? | Returns |
|--------|:-----------:|---------|
| `d["key"]` | ❌ KeyError | — |
| `d.get("key")` | ✅ No error | `None` |
| `d.get("key", default)` | ✅ No error | `default` |

✔ **Use `get()` when you're unsure if the key exists.**

---

## 🔹 Adding and Updating Items

### 🔸 Add/Update with `[]`

```python
person = {"name": "Giridhar", "age": 25}

# Add new key
person["city"] = "Hyderabad"
print(person)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}

# Update existing key
person["age"] = 26
print(person)   # {'name': 'Giridhar', 'age': 26, 'city': 'Hyderabad'}
```

### 🔸 update() — Merge Dictionaries

```python
person = {"name": "Giridhar", "age": 25}
extra = {"city": "Hyderabad", "age": 26}

person.update(extra)
print(person)   # {'name': 'Giridhar', 'age': 26, 'city': 'Hyderabad'}
```

✔ Existing keys are **overwritten**. New keys are **added**.

### 🔸 Merge with `|` Operator (Python 3.9+)

```python
a = {"x": 1, "y": 2}
b = {"y": 3, "z": 4}

# Creates a NEW dictionary
merged = a | b
print(merged)   # {'x': 1, 'y': 3, 'z': 4}

# Update in-place
a |= b
print(a)   # {'x': 1, 'y': 3, 'z': 4}
```

### 🔸 Merge with `**` Unpacking (Python 3.5+)

```python
a = {"x": 1, "y": 2}
b = {"y": 3, "z": 4}

merged = {**a, **b}
print(merged)   # {'x': 1, 'y': 3, 'z': 4}
```

### 🔸 setdefault() — Add Only If Key Doesn't Exist

```python
person = {"name": "Giridhar", "age": 25}

# Key exists → returns existing value, doesn't change
result = person.setdefault("name", "Unknown")
print(result)   # Giridhar
print(person)   # {'name': 'Giridhar', 'age': 25}

# Key doesn't exist → adds it with the default value
result = person.setdefault("city", "Hyderabad")
print(result)   # Hyderabad
print(person)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}
```

---

## 🔹 Removing Items

### 🔸 pop() — Remove by Key (Returns Value)

```python
person = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

removed = person.pop("age")
print(removed)   # 25
print(person)    # {'name': 'Giridhar', 'city': 'Hyderabad'}
```

⚠️ If key doesn't exist:

```python
person.pop("email")   # ❌ KeyError

# ✅ Safe with default
person.pop("email", None)   # Returns None, no error
```

### 🔸 popitem() — Remove Last Inserted Item

```python
person = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

last = person.popitem()
print(last)      # ('city', 'Hyderabad')
print(person)    # {'name': 'Giridhar', 'age': 25}
```

### 🔸 del — Delete by Key

```python
person = {"name": "Giridhar", "age": 25}

del person["age"]
print(person)   # {'name': 'Giridhar'}

# Delete entire dictionary
del person
# print(person)   # ❌ NameError
```

### 🔸 clear() — Remove All Items

```python
person = {"name": "Giridhar", "age": 25}
person.clear()
print(person)   # {}
```

### 🔸 Removal Methods Summary

| Method | Removes By | Returns | Error if Missing? |
|--------|-----------|---------|:-:|
| `pop(key)` | Key | Value | ✅ KeyError |
| `pop(key, default)` | Key | default | ❌ |
| `popitem()` | Last item | (key, value) tuple | ✅ if empty |
| `del d[key]` | Key | Nothing | ✅ KeyError |
| `clear()` | All items | Nothing | ❌ |

---

## 🔹 Checking if Key Exists

### 🔸 Using `in` (Checks KEYS, Not Values!)

```python
person = {"name": "Giridhar", "age": 25}

print("name" in person)       # True
print("email" in person)      # False
print("Giridhar" in person)   # False  ← checks KEYS only!
```

### 🔸 Check if Value Exists

```python
print("Giridhar" in person.values())   # True
print(25 in person.values())           # True
```

### 🔸 Check if Key-Value Pair Exists

```python
print(("name", "Giridhar") in person.items())   # True
```

---

## 🔹 Dictionary Views: keys(), values(), items()

### 🔸 keys() — All Keys

```python
person = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

print(person.keys())   # dict_keys(['name', 'age', 'city'])
print(list(person.keys()))   # ['name', 'age', 'city']
```

### 🔸 values() — All Values

```python
print(person.values())   # dict_values(['Giridhar', 25, 'Hyderabad'])
print(list(person.values()))   # ['Giridhar', 25, 'Hyderabad']
```

### 🔸 items() — All Key-Value Pairs (as Tuples)

```python
print(person.items())
# dict_items([('name', 'Giridhar'), ('age', 25), ('city', 'Hyderabad')])
```

### 🔸 Views Are Dynamic

```python
keys = person.keys()
print(keys)   # dict_keys(['name', 'age', 'city'])

person["email"] = "giri@email.com"
print(keys)   # dict_keys(['name', 'age', 'city', 'email'])  ← auto-updated!
```

✔ Views reflect changes to the dictionary **automatically**.

### 🔸 Dictionary Views Are Set-Like (ADVANCED INTERVIEW 🔥)

`.keys()` and `.items()` return **set-like objects**, meaning you can perform set operations directly on them:

```python
d1 = {"a": 1, "b": 2, "c": 3}
d2 = {"b": 4, "c": 5, "d": 6}

# Common keys (intersection)
print(d1.keys() & d2.keys())    # {'b', 'c'}

# Keys only in d1 (difference)
print(d1.keys() - d2.keys())    # {'a'}

# All keys (union)
print(d1.keys() | d2.keys())    # {'a', 'b', 'c', 'd'}
```

⚠️ `.values()` does **NOT** support set operations (because values can have duplicates and aren't hashable).

✔ This is why `d1.keys() & d2.keys()` works without converting to sets first.

---

## 🔹 Iterating Through Dictionaries

### 🔸 Loop Through Keys (Default)

```python
person = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

for key in person:
    print(key)
```

Output:
```
name
age
city
```

### 🔸 Loop Through Values

```python
for value in person.values():
    print(value)
```

### 🔸 Loop Through Key-Value Pairs

```python
for key, value in person.items():
    print(f"{key}: {value}")
```

Output:
```
name: Giridhar
age: 25
city: Hyderabad
```

### 🔸 Loop with Index — Using enumerate()

```python
for index, (key, value) in enumerate(person.items()):
    print(f"{index}: {key} = {value}")
```

---

## 🔹 Dictionary Comprehensions (VERY IMPORTANT 🔥)

### 🔸 Basic Comprehension

```python
# Normal way
squares = {}
for i in range(5):
    squares[i] = i * i

# Comprehension
squares = {i: i * i for i in range(5)}
print(squares)   # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### 🔸 With Condition

```python
# Only even numbers
even_squares = {i: i * i for i in range(10) if i % 2 == 0}
print(even_squares)   # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

### 🔸 Swap Keys and Values

```python
original = {"a": 1, "b": 2, "c": 3}
swapped = {value: key for key, value in original.items()}
print(swapped)   # {1: 'a', 2: 'b', 3: 'c'}
```

### 🔸 From Two Lists

```python
keys = ["name", "age", "city"]
values = ["Giridhar", 25, "Hyderabad"]

d = {k: v for k, v in zip(keys, values)}
print(d)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}
```

#### Pythonic shortcut:

```python
d = dict(zip(keys, values))   # same result, cleaner
```

---

## 🔹 Nested Dictionaries

### 🔸 Creating

```python
students = {
    "student1": {
        "name": "Alice",
        "age": 20,
        "grades": [90, 85, 92]
    },
    "student2": {
        "name": "Bob",
        "age": 22,
        "grades": [78, 82, 88]
    }
}
```

### 🔸 Accessing Nested Values

```python
print(students["student1"]["name"])        # Alice
print(students["student2"]["grades"][0])   # 78
```

### 🔸 Modifying Nested Values

```python
students["student1"]["age"] = 21
students["student2"]["grades"].append(95)
```

### 🔸 Iterating Nested Dictionaries

```python
for student_id, info in students.items():
    print(f"\n{student_id}:")
    for key, value in info.items():
        print(f"  {key}: {value}")
```

### 🔸 Safe Nested Access

```python
# ❌ Dangerous — KeyError if any key is missing
# print(students["student3"]["name"])

# ✅ Safe with get()
print(students.get("student3", {}).get("name", "Not found"))   # Not found
```

---

## 🔹 Copying Dictionaries

### 🔸 `=` is NOT a Copy

```python
original = {"a": 1, "b": 2}
copy = original

copy["c"] = 3
print(original)   # {'a': 1, 'b': 2, 'c': 3}  ← original also changed!
```

### 🔸 Shallow Copy

```python
original = {"a": 1, "b": 2}

# Method 1: .copy()
copy1 = original.copy()

# Method 2: dict()
copy2 = dict(original)

# Method 3: unpacking
copy3 = {**original}
```

### 🔸 Shallow Copy Limitation (Nested Dicts)

```python
original = {"a": [1, 2, 3]}
copy = original.copy()

copy["a"].append(4)
print(original)   # {'a': [1, 2, 3, 4]}  ← inner list shared!
```

### 🔸 Deep Copy

```python
import copy

original = {"a": [1, 2, 3]}
deep = copy.deepcopy(original)

deep["a"].append(4)
print(original)   # {'a': [1, 2, 3]}  ← safe!
```

---

## 🔹 defaultdict — Auto-Create Missing Keys (IMPORTANT 🔥)

From the `collections` module. Automatically creates a default value when accessing a missing key.

```python
from collections import defaultdict

# Normal dict — KeyError on missing key
d = {}
# d["count"] += 1   # ❌ KeyError

# defaultdict — auto-creates default value
d = defaultdict(int)   # default value is 0
d["count"] += 1
print(d["count"])   # 1

d = defaultdict(list)   # default value is []
d["fruits"].append("apple")
print(d["fruits"])   # ['apple']
```

### 🔸 Common Use: Counting Frequency

```python
from collections import defaultdict

text = "hello world"
freq = defaultdict(int)

for char in text:
    freq[char] += 1

print(dict(freq))
# {'h': 1, 'e': 1, 'l': 3, 'o': 2, ' ': 1, 'w': 1, 'r': 1, 'd': 1}
```

### 🔸 Common Use: Grouping

```python
from collections import defaultdict

students = [("Alice", "Math"), ("Bob", "Science"), ("Alice", "Science"), ("Bob", "Math")]
groups = defaultdict(list)

for name, subject in students:
    groups[name].append(subject)

print(dict(groups))
# {'Alice': ['Math', 'Science'], 'Bob': ['Science', 'Math']}
```

---

## 🔹 Counter — Count Frequencies Easily (IMPORTANT 🔥)

```python
from collections import Counter

# Count characters
text = "banana"
freq = Counter(text)
print(freq)   # Counter({'a': 3, 'n': 2, 'b': 1})

# Count list items
nums = [1, 2, 2, 3, 3, 3]
freq = Counter(nums)
print(freq)   # Counter({3: 3, 2: 2, 1: 1})

# Most common
print(freq.most_common(2))   # [(3, 3), (2, 2)]
```

---

## 🔹 OrderedDict (Python < 3.7)

Before Python 3.7, regular dicts didn't preserve insertion order. `OrderedDict` was used for that.

```python
from collections import OrderedDict

d = OrderedDict()
d["a"] = 1
d["b"] = 2
d["c"] = 3

print(d)   # OrderedDict([('a', 1), ('b', 2), ('c', 3)])
```

✔ In Python 3.7+, regular `dict` preserves insertion order. `OrderedDict` is still useful for:
- `move_to_end()` method
- Equality checks that consider order

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Using `[]` for Missing Keys

```python
d = {"name": "Python"}
print(d["version"])   # ❌ KeyError

# ✅ Use get()
print(d.get("version", "Unknown"))   # Unknown
```

### 🔸 Mistake 2: `in` Checks Keys, Not Values

```python
d = {"name": "Python"}
print("Python" in d)           # False  ← checks keys!
print("Python" in d.values())  # True   ← checks values
```

### 🔸 Mistake 3: Modifying Dict While Iterating

```python
d = {"a": 1, "b": 2, "c": 3}

# ❌ RuntimeError: dictionary changed size during iteration
for key in d:
    if d[key] < 3:
        del d[key]

# ✅ Iterate over a copy of keys
for key in list(d.keys()):
    if d[key] < 3:
        del d[key]
```

### 🔸 Mistake 4: Mutable Default with fromkeys()

```python
# ❌ All values share the same list
d = dict.fromkeys(["a", "b"], [])

# ✅ Use comprehension
d = {k: [] for k in ["a", "b"]}
```

### 🔸 Mistake 5: Bool/Int Key Collision

```python
d = {True: "yes", 1: "one"}
print(d)   # {True: 'one'}  ← True and 1 are the same key!
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Count Character Frequency

#### Manual way:

```python
text = "hello world"
freq = {}

for char in text:
    if char in freq:
        freq[char] = freq[char] + 1
    else:
        freq[char] = 1

print(freq)
```

#### Pythonic shortcut:

```python
from collections import Counter
print(Counter(text))
```

---

### ✅ 2. Find the Most Frequent Element

#### Manual way:

```python
nums = [1, 2, 2, 3, 3, 3, 4]
freq = {}

for num in nums:
    if num in freq:
        freq[num] = freq[num] + 1
    else:
        freq[num] = 1

max_key = None
max_count = 0

for key, count in freq.items():
    if count > max_count:
        max_count = count
        max_key = key

print(f"Most frequent: {max_key} ({max_count} times)")
```

#### Pythonic shortcut:

```python
from collections import Counter
most = Counter(nums).most_common(1)[0]
print(f"Most frequent: {most[0]} ({most[1]} times)")
```

---

### ✅ 3. Merge Two Dictionaries

#### Manual way:

```python
d1 = {"a": 1, "b": 2}
d2 = {"b": 3, "c": 4}
merged = {}

for key, value in d1.items():
    merged[key] = value

for key, value in d2.items():
    merged[key] = value

print(merged)   # {'a': 1, 'b': 3, 'c': 4}
```

#### Pythonic shortcuts:

```python
merged = {**d1, **d2}       # unpacking
merged = d1 | d2            # Python 3.9+
```

---

### ✅ 4. Invert a Dictionary (Swap Keys and Values)

#### Manual way:

```python
original = {"a": 1, "b": 2, "c": 3}
inverted = {}

for key, value in original.items():
    inverted[value] = key

print(inverted)   # {1: 'a', 2: 'b', 3: 'c'}
```

#### Pythonic shortcut:

```python
inverted = {v: k for k, v in original.items()}
```

---

### ✅ 5. Group Words by First Letter

#### Manual way:

```python
words = ["apple", "banana", "avocado", "blueberry", "cherry", "apricot"]
groups = {}

for word in words:
    first_letter = word[0]
    if first_letter in groups:
        groups[first_letter].append(word)
    else:
        groups[first_letter] = [word]

print(groups)
# {'a': ['apple', 'avocado', 'apricot'], 'b': ['banana', 'blueberry'], 'c': ['cherry']}
```

#### Pythonic shortcut:

```python
from collections import defaultdict

groups = defaultdict(list)
for word in words:
    groups[word[0]].append(word)
```

---

### ✅ 6. Find Common Keys in Two Dictionaries

#### Manual way:

```python
d1 = {"a": 1, "b": 2, "c": 3}
d2 = {"b": 4, "c": 5, "d": 6}
common = []

for key in d1:
    if key in d2:
        common.append(key)

print(common)   # ['b', 'c']
```

#### Pythonic shortcut:

```python
common = list(d1.keys() & d2.keys())
print(common)   # ['b', 'c']
```

---

### ✅ 7. Sort Dictionary by Value

#### Manual way:

```python
scores = {"Alice": 85, "Bob": 92, "Charlie": 78}
sorted_items = []

# Simple selection sort on items
items = list(scores.items())
i = 0
while i < len(items):
    j = i + 1
    while j < len(items):
        if items[j][1] > items[i][1]:
            items[i], items[j] = items[j], items[i]
        j = j + 1
    i = i + 1

sorted_dict = dict(items)
print(sorted_dict)   # {'Bob': 92, 'Alice': 85, 'Charlie': 78}
```

#### Pythonic shortcut:

```python
sorted_dict = dict(sorted(scores.items(), key=lambda item: item[1], reverse=True))
print(sorted_dict)   # {'Bob': 92, 'Alice': 85, 'Charlie': 78}
```

---

### ✅ 8. Two Sum Problem (CLASSIC INTERVIEW 🔥)

Given a list and a target, find two numbers that add up to the target.

#### Manual way (brute force):

```python
nums = [2, 7, 11, 15]
target = 9

i = 0
while i < len(nums):
    j = i + 1
    while j < len(nums):
        if nums[i] + nums[j] == target:
            print(f"Found: {nums[i]} + {nums[j]} = {target}")
            break
        j = j + 1
    i = i + 1
```

#### Using dictionary (efficient approach):

```python
nums = [2, 7, 11, 15]
target = 9
seen = {}

for num in nums:
    complement = target - num
    if complement in seen:
        print(f"Found: {complement} + {num} = {target}")
        break
    seen[num] = True
```

🧠 The dictionary stores numbers we've already seen. For each new number, we check if its complement (target - num) was seen before. This finds the answer in a single pass through the list.

---

## 🔹 All Dictionary Methods — Quick Reference 📌

| Method | Description | Returns |
|--------|-------------|---------|
| `get(key, default)` | Safe access | Value or default |
| `keys()` | All keys | dict_keys view |
| `values()` | All values | dict_values view |
| `items()` | All key-value pairs | dict_items view |
| `update(other)` | Merge/update | None |
| `setdefault(key, val)` | Get or set default | Value |
| `pop(key, default)` | Remove and return | Value |
| `popitem()` | Remove last item | (key, value) tuple |
| `clear()` | Remove all | None |
| `copy()` | Shallow copy | New dict |
| `fromkeys(keys, val)` | Create from keys | New dict |

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| Dictionary | Mutable collection of key-value pairs |
| Creating | `{}`, `dict()`, `dict.fromkeys()`, `dict(zip())` |
| Access | `d["key"]` (KeyError) or `d.get("key")` (safe) |
| Add/Update | `d["key"] = value`, `d.update()`, `d \| d2` |
| Remove | `pop()`, `popitem()`, `del`, `clear()` |
| Check key | `"key" in d` (checks keys only!) |
| Check value | `"val" in d.values()` |
| Views | `keys()`, `values()`, `items()` — dynamic |
| Iteration | `for k, v in d.items()` |
| Comprehension | `{k: v for k, v in ...}` |
| Nested | `d["outer"]["inner"]` |
| Copy | `.copy()` (shallow), `deepcopy()` (deep) |
| `defaultdict` | Auto-creates missing keys |
| `Counter` | Count frequencies easily |
| `setdefault()` | Add only if key missing |
| Key rules | Must be immutable, unique, `True == 1` trap |

---

> 🚀 **Next:** Sets in Python →
