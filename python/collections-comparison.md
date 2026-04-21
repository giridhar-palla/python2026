# 🔄 Python Collections — Complete Comparison & Conversion Guide (Zero to Hero)

> Everything about **List, Tuple, Set, Dictionary, String** — differences, similarities, and how to convert between them.

---

## 🔹 The Big Picture — All 5 Collection Types

| Feature | String `str` | List `list` | Tuple `tuple` | Set `set` | Dictionary `dict` |
|---------|:---:|:---:|:---:|:---:|:---:|
| Syntax | `"hello"` | `[1, 2, 3]` | `(1, 2, 3)` | `{1, 2, 3}` | `{"a": 1}` |
| Ordered | ✅ | ✅ | ✅ | ❌ | ✅ (3.7+) |
| Mutable | ❌ | ✅ | ❌ | ✅ | ✅ |
| Duplicates | ✅ | ✅ | ✅ | ❌ | Keys: ❌, Values: ✅ |
| Indexed | ✅ | ✅ | ✅ | ❌ | By key |
| Sliceable | ✅ | ✅ | ✅ | ❌ | ❌ |
| Hashable | ✅ | ❌ | ✅ | ❌ | ❌ |
| As dict key | ✅ | ❌ | ✅ | ❌ | ❌ |
| As set element | ✅ | ❌ | ✅ | ❌ | ❌ |
| Empty creation | `""` | `[]` | `()` | `set()` | `{}` |

---

## 🔹 Mutable vs Immutable — The Core Difference

### 🔸 Mutable (Can Change After Creation)

```python
# List — can change
my_list = [1, 2, 3]
my_list[0] = 99
my_list.append(4)
print(my_list)   # [99, 2, 3, 4]

# Set — can change
my_set = {1, 2, 3}
my_set.add(4)
my_set.discard(1)
print(my_set)   # {2, 3, 4}

# Dict — can change
my_dict = {"a": 1}
my_dict["b"] = 2
my_dict["a"] = 99
print(my_dict)   # {'a': 99, 'b': 2}
```

### 🔸 Immutable (Cannot Change After Creation)

```python
# String — cannot change
text = "Hello"
text[0] = "J"   # ❌ TypeError

# Tuple — cannot change
my_tuple = (1, 2, 3)
my_tuple[0] = 99   # ❌ TypeError
my_tuple.append(4)  # ❌ AttributeError
```

### 🔸 Why Does It Matter?

| | Mutable | Immutable |
|---|---|---|
| Can be dict key? | ❌ | ✅ |
| Can be set element? | ❌ | ✅ |
| Thread safe? | ❌ | ✅ |
| Can be changed accidentally? | ✅ (careful!) | ❌ (safe) |

```python
# ✅ Immutable types as dict keys
d = {
    "hello": 1,       # string ✅
    (1, 2): 2,        # tuple ✅
    42: 3,             # int ✅
}

# ❌ Mutable types as dict keys
d = {
    [1, 2]: 1,         # list ❌ TypeError
    {1, 2}: 2,         # set ❌ TypeError
    {"a": 1}: 3,       # dict ❌ TypeError
}
```

---

## 🔹 Ordered vs Unordered

### 🔸 Ordered — Items Have a Fixed Position

```python
# String — ordered
text = "Python"
print(text[0])   # P  (always P)

# List — ordered
nums = [10, 20, 30]
print(nums[1])   # 20  (always 20)

# Tuple — ordered
point = (5, 10)
print(point[0])  # 5  (always 5)

# Dict — insertion ordered (Python 3.7+)
d = {"a": 1, "b": 2, "c": 3}
print(list(d.keys()))   # ['a', 'b', 'c']  (always this order)
```

### 🔸 Unordered — No Fixed Position

```python
# Set — unordered
s = {3, 1, 4, 1, 5}
print(s)   # {1, 3, 4, 5}  (order may vary!)

# Cannot index
print(s[0])   # ❌ TypeError
```

---

## 🔹 Duplicates Allowed vs Not Allowed

```python
# ✅ Duplicates allowed
my_list = [1, 2, 2, 3, 3, 3]       # [1, 2, 2, 3, 3, 3]
my_tuple = (1, 2, 2, 3, 3, 3)      # (1, 2, 2, 3, 3, 3)
my_string = "aabbcc"                 # "aabbcc"

# ❌ Duplicates NOT allowed
my_set = {1, 2, 2, 3, 3, 3}        # {1, 2, 3}  ← auto-removed
my_dict = {"a": 1, "a": 2}          # {'a': 2}   ← last value wins
```

---

## 🔹 Methods Count Comparison

| Type | Total Methods | Add | Remove | Sort | Search |
|------|:---:|:---:|:---:|:---:|:---:|
| `str` | 40+ | ❌ (immutable) | ❌ | ❌ | `find()`, `index()`, `count()` |
| `list` | 11 | `append()`, `extend()`, `insert()` | `remove()`, `pop()`, `clear()` | `sort()`, `reverse()` | `index()`, `count()` |
| `tuple` | 2 | ❌ (immutable) | ❌ | ❌ | `index()`, `count()` |
| `set` | 17 | `add()`, `update()` | `remove()`, `discard()`, `pop()`, `clear()` | ❌ | ❌ (use `in`) |
| `dict` | 11 | `update()`, `setdefault()` | `pop()`, `popitem()`, `clear()` | ❌ | `get()`, `keys()`, `values()`, `items()` |

---

# 🔄 CONVERSION GUIDE — Every Type to Every Type

---

## 🔹 String → Everything

### 🔸 String → List

```python
# Each character becomes a list item
text = "Python"
result = list(text)
print(result)   # ['P', 'y', 't', 'h', 'o', 'n']

# Split by separator (more common)
text = "apple,banana,cherry"
result = text.split(",")
print(result)   # ['apple', 'banana', 'cherry']

# Split by spaces
text = "hello world python"
result = text.split()
print(result)   # ['hello', 'world', 'python']
```

⚠️ **Common trap:** `list("hello")` gives `['h', 'e', 'l', 'l', 'o']`, NOT `["hello"]`.

### 🔸 String → Tuple

```python
text = "Python"
result = tuple(text)
print(result)   # ('P', 'y', 't', 'h', 'o', 'n')

# From split
text = "apple,banana,cherry"
result = tuple(text.split(","))
print(result)   # ('apple', 'banana', 'cherry')
```

### 🔸 String → Set

```python
text = "hello"
result = set(text)
print(result)   # {'h', 'e', 'l', 'o'}  ← duplicate 'l' removed, order may vary
```

### 🔸 String → Dictionary

```python
# Cannot directly convert — need key-value structure

# From a formatted string
text = "name=Giridhar,age=25,city=Hyderabad"
pairs = text.split(",")
result = {}
for pair in pairs:
    key, value = pair.split("=")
    result[key] = value

print(result)   # {'name': 'Giridhar', 'age': '25', 'city': 'Hyderabad'}
```

### 🔸 String → Integer / Float

```python
num = int("42")        # 42
price = float("3.14")  # 3.14
```

---

## 🔹 List → Everything

### 🔸 List → String

```python
# Join list of strings
words = ["Python", "is", "easy"]
result = " ".join(words)
print(result)   # "Python is easy"

# ⚠️ Only works with list of strings!
nums = [1, 2, 3]
# " ".join(nums)   # ❌ TypeError

# ✅ Convert to strings first
result = " ".join(str(n) for n in nums)
print(result)   # "1 2 3"

# str() gives literal representation (usually NOT what you want)
print(str([1, 2, 3]))   # "[1, 2, 3]"  ← includes brackets!
```

### 🔸 List → Tuple

```python
my_list = [1, 2, 3]
result = tuple(my_list)
print(result)   # (1, 2, 3)
```

### 🔸 List → Set (Removes Duplicates!)

```python
my_list = [1, 2, 2, 3, 3, 3]
result = set(my_list)
print(result)   # {1, 2, 3}
```

⚠️ **Order is NOT preserved** when converting to set.

### 🔸 List → Dictionary

```python
# From list of pairs (tuples or lists)
pairs = [("name", "Giridhar"), ("age", 25), ("city", "Hyderabad")]
result = dict(pairs)
print(result)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}

# From two separate lists using zip()
keys = ["name", "age", "city"]
values = ["Giridhar", 25, "Hyderabad"]
result = dict(zip(keys, values))
print(result)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}

# List as values with enumerate (index as key)
fruits = ["apple", "banana", "cherry"]
result = dict(enumerate(fruits))
print(result)   # {0: 'apple', 1: 'banana', 2: 'cherry'}
```

---

## 🔹 Tuple → Everything

### 🔸 Tuple → String

```python
chars = ('P', 'y', 't', 'h', 'o', 'n')
result = "".join(chars)
print(result)   # "Python"
```

### 🔸 Tuple → List

```python
my_tuple = (1, 2, 3)
result = list(my_tuple)
print(result)   # [1, 2, 3]
```

### 🔸 Tuple → Set

```python
my_tuple = (1, 2, 2, 3, 3)
result = set(my_tuple)
print(result)   # {1, 2, 3}
```

### 🔸 Tuple → Dictionary

```python
# From tuple of pairs
pairs = (("name", "Giridhar"), ("age", 25))
result = dict(pairs)
print(result)   # {'name': 'Giridhar', 'age': 25}

# Two tuples using zip
keys = ("name", "age", "city")
values = ("Giridhar", 25, "Hyderabad")
result = dict(zip(keys, values))
print(result)   # {'name': 'Giridhar', 'age': 25, 'city': 'Hyderabad'}
```

---

## 🔹 Set → Everything

### 🔸 Set → String

```python
chars = {'P', 'y', 't', 'h', 'o', 'n'}
result = "".join(chars)
print(result)   # order may vary! e.g., "nPyhto"

# ✅ If you need sorted order
result = "".join(sorted(chars))
print(result)   # "Phnoty"
```

### 🔸 Set → List

```python
my_set = {3, 1, 2}
result = list(my_set)
print(result)   # [1, 2, 3]  (order may vary)

# ✅ Sorted list
result = sorted(my_set)
print(result)   # [1, 2, 3]
```

### 🔸 Set → Tuple

```python
my_set = {3, 1, 2}
result = tuple(my_set)
print(result)   # (1, 2, 3)  (order may vary)
```

### 🔸 Set → Dictionary

```python
# Cannot directly — sets have no key-value structure
# But you can create one:

my_set = {"apple", "banana", "cherry"}
result = {item: len(item) for item in my_set}
print(result)   # {'apple': 5, 'banana': 6, 'cherry': 6}
```

---

## 🔹 Dictionary → Everything

### 🔸 Dictionary → String

```python
d = {"name": "Giridhar", "age": 25}

# str() gives literal representation
print(str(d))   # "{'name': 'Giridhar', 'age': 25}"

# Custom formatted string
result = ", ".join(f"{k}={v}" for k, v in d.items())
print(result)   # "name=Giridhar, age=25"
```

### 🔸 Dictionary → List

```python
d = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

# Keys only (default)
print(list(d))            # ['name', 'age', 'city']
print(list(d.keys()))     # ['name', 'age', 'city']

# Values only
print(list(d.values()))   # ['Giridhar', 25, 'Hyderabad']

# Key-value pairs as tuples
print(list(d.items()))    # [('name', 'Giridhar'), ('age', 25), ('city', 'Hyderabad')]
```

⚠️ **Common trap:** `list(dict)` gives **only keys**, not values!

### 🔸 Dictionary → Tuple

```python
d = {"name": "Giridhar", "age": 25}

print(tuple(d))            # ('name', 'age')           ← keys only!
print(tuple(d.values()))   # ('Giridhar', 25)          ← values only
print(tuple(d.items()))    # (('name', 'Giridhar'), ('age', 25))  ← pairs
```

### 🔸 Dictionary → Set

```python
d = {"name": "Giridhar", "age": 25}

print(set(d))            # {'name', 'age'}           ← keys only!
print(set(d.values()))   # {'Giridhar', 25}          ← values only
```

---

## 🔹 Complete Conversion Matrix 📌

| From ↓ / To → | `str` | `list` | `tuple` | `set` | `dict` |
|:---:|:---:|:---:|:---:|:---:|:---:|
| **`str`** | — | `list(s)` or `s.split()` | `tuple(s)` | `set(s)` | Need parsing |
| **`list`** | `"".join(l)` | — | `tuple(l)` | `set(l)` | `dict(pairs)` or `dict(zip())` |
| **`tuple`** | `"".join(t)` | `list(t)` | — | `set(t)` | `dict(pairs)` or `dict(zip())` |
| **`set`** | `"".join(s)` | `list(s)` | `tuple(s)` | — | Comprehension |
| **`dict`** | Custom format | `list(d)` = keys | `tuple(d)` = keys | `set(d)` = keys | — |

⚠️ **Key things to remember:**
- `list(string)` → splits into **characters**, not words. Use `.split()` for words.
- `list(dict)` → gives **keys only**. Use `.values()` or `.items()` for more.
- `set()` → **removes duplicates** and **loses order**.
- `"".join()` → only works with **strings**. Convert numbers first with `str()`.
- `dict()` → needs **pairs** (list of tuples, or two lists with `zip()`).

---

## 🔹 When to Use Which Collection?

| Situation | Best Choice | Why |
|-----------|:-----------:|-----|
| Ordered items that change | `list` | Mutable + ordered |
| Ordered items that don't change | `tuple` | Immutable + faster |
| Unique items, no order needed | `set` | Auto-removes duplicates |
| Key-value mapping | `dict` | Fast lookup by key |
| Text data | `str` | Built for text |
| Need as dict key | `tuple` or `str` | Must be immutable |
| Remove duplicates from list | `set(list)` | One-liner |
| Count frequencies | `dict` or `Counter` | Key = item, value = count |
| Fast membership check | `set` or `dict` | Direct lookup |
| Fixed config data | `tuple` | Cannot be changed accidentally |
| Function returning multiple values | `tuple` | `return x, y` |

---

## 🔹 Speed of `in` (Membership Check)

```python
# Conceptual comparison — NOT Big-O jargon

my_list = [1, 2, 3, ..., 1000000]
my_set = {1, 2, 3, ..., 1000000}
my_dict = {1: True, 2: True, ..., 1000000: True}
```

| Collection | How `in` Works | Speed |
|-----------|----------------|-------|
| `list` | Checks every item one by one | Slow for large data |
| `tuple` | Checks every item one by one | Slow for large data |
| `set` | Direct lookup (hashing) | Fast regardless of size |
| `dict` | Direct lookup on keys (hashing) | Fast regardless of size |
| `str` | Scans through characters | Depends on length |

✔ If you need to check membership frequently, **convert your list to a set**.

```python
# ❌ Slow — checking in a list repeatedly
names_list = ["Alice", "Bob", "Charlie", ...]
if "Zara" in names_list:   # checks every item
    pass

# ✅ Fast — convert to set first
names_set = set(names_list)
if "Zara" in names_set:    # direct lookup
    pass
```

---

## 🔹 Memory Usage Comparison

```python
import sys

data = list(range(1000))

print(f"List:  {sys.getsizeof(data)} bytes")
print(f"Tuple: {sys.getsizeof(tuple(data))} bytes")
print(f"Set:   {sys.getsizeof(set(data))} bytes")
```

General rule:
```
Tuple < List < Set < Dict
```

✔ Tuples use the **least memory** because Python doesn't need to allocate extra space for modifications.

---

## 🔹 Nesting Comparison

```python
# List of lists ✅
matrix = [[1, 2], [3, 4]]

# Tuple of tuples ✅
matrix = ((1, 2), (3, 4))

# List of dicts ✅ (very common!)
students = [
    {"name": "Alice", "age": 20},
    {"name": "Bob", "age": 22}
]

# Dict of lists ✅
grades = {
    "Alice": [90, 85, 92],
    "Bob": [78, 82, 88]
}

# Set of tuples ✅ (tuples are hashable)
points = {(1, 2), (3, 4), (5, 6)}

# ❌ Set of lists — NOT allowed (lists are unhashable)
# points = {[1, 2], [3, 4]}   # TypeError

# ❌ Dict with list keys — NOT allowed
# d = {[1, 2]: "point"}   # TypeError
```

---

## 🔹 Iteration Comparison

```python
# All support for loops
for char in "hello":       pass   # string
for item in [1, 2, 3]:    pass   # list
for item in (1, 2, 3):    pass   # tuple
for item in {1, 2, 3}:    pass   # set
for key in {"a": 1}:      pass   # dict (keys by default)

# With enumerate (index + value)
for i, item in enumerate([10, 20, 30]):
    print(f"{i}: {item}")

# Dict special iterations
d = {"a": 1, "b": 2}
for key in d:                    pass   # keys
for value in d.values():         pass   # values
for key, value in d.items():     pass   # both
```

---

## 🔹 Common Operations Comparison

### 🔸 Length

```python
print(len("hello"))          # 5
print(len([1, 2, 3]))        # 3
print(len((1, 2, 3)))        # 3
print(len({1, 2, 3}))        # 3
print(len({"a": 1, "b": 2})) # 2
```

### 🔸 Concatenation

```python
# String
print("Hello" + " World")        # "Hello World"

# List
print([1, 2] + [3, 4])           # [1, 2, 3, 4]

# Tuple
print((1, 2) + (3, 4))           # (1, 2, 3, 4)

# Set — NO concatenation with +
# {1, 2} + {3, 4}   # ❌ TypeError
# ✅ Use union
print({1, 2} | {3, 4})           # {1, 2, 3, 4}

# Dict — NO concatenation with +
# ✅ Use | (Python 3.9+)
print({"a": 1} | {"b": 2})       # {'a': 1, 'b': 2}
```

### 🔸 Repetition

```python
print("Ha" * 3)          # "HaHaHa"
print([0] * 3)            # [0, 0, 0]
print((0,) * 3)           # (0, 0, 0)

# Set — NO repetition
# {0} * 3   # ❌ TypeError

# Dict — NO repetition
```

### 🔸 Sorting

```python
# All use sorted() — returns a LIST
print(sorted("python"))           # ['h', 'n', 'o', 'p', 't', 'y']
print(sorted([3, 1, 2]))          # [1, 2, 3]
print(sorted((3, 1, 2)))          # [1, 2, 3]
print(sorted({3, 1, 2}))          # [1, 2, 3]
print(sorted({"c": 3, "a": 1}))   # ['a', 'c']  (sorts keys)

# Only list has in-place sort
nums = [3, 1, 2]
nums.sort()   # modifies original
```

### 🔸 Reversing

```python
# Slicing (string, list, tuple)
print("hello"[::-1])       # "olleh"
print([1, 2, 3][::-1])     # [3, 2, 1]
print((1, 2, 3)[::-1])     # (3, 2, 1)

# Set — NO reversing (unordered)
# Dict — NO reversing with slicing

# reversed() — works on sequences
print(list(reversed([1, 2, 3])))   # [3, 2, 1]

# Only list has in-place reverse
nums = [1, 2, 3]
nums.reverse()
```

---

## 🔹 Interview Quick-Fire Questions 💡

### Q1: Which collections are mutable?
**Answer:** `list`, `set`, `dict`

### Q2: Which collections are immutable?
**Answer:** `str`, `tuple`, `frozenset`

### Q3: Which can be used as dictionary keys?
**Answer:** Only **immutable** types: `str`, `int`, `float`, `tuple`, `bool`, `frozenset`

### Q4: Which allows duplicates?
**Answer:** `str`, `list`, `tuple` — YES. `set`, `dict` (keys) — NO.

### Q5: Which is ordered?
**Answer:** `str`, `list`, `tuple`, `dict` (3.7+) — YES. `set` — NO.

### Q6: How to remove duplicates from a list while preserving order?
```python
unique = list(dict.fromkeys(my_list))
```

### Q7: How to check if two lists have common elements?
```python
has_common = bool(set(list1) & set(list2))
```

### Q8: How to convert two lists into a dictionary?
```python
d = dict(zip(keys, values))
```

### Q9: How to get unique characters from a string?
```python
unique = set("hello")   # {'h', 'e', 'l', 'o'}
```

### Q10: What's the fastest way to check if an item exists?
**Answer:** Use a `set` or `dict`. They use direct lookup (hashing), which is fast regardless of size.

### Q11: What happens with `list(dict)`?
**Answer:** Returns **only keys**, not values. Use `.values()` or `.items()` for more.

### Q12: What's the difference between `sort()` and `sorted()`?
**Answer:** `sort()` modifies the original list (returns `None`). `sorted()` returns a new list (works on any iterable).

---

## 🔹 Complete Summary 📌

| | `str` | `list` | `tuple` | `set` | `dict` |
|---|:---:|:---:|:---:|:---:|:---:|
| **Mutable** | ❌ | ✅ | ❌ | ✅ | ✅ |
| **Ordered** | ✅ | ✅ | ✅ | ❌ | ✅ (3.7+) |
| **Duplicates** | ✅ | ✅ | ✅ | ❌ | Keys ❌ |
| **Indexed** | ✅ | ✅ | ✅ | ❌ | By key |
| **Hashable** | ✅ | ❌ | ✅ | ❌ | ❌ |
| **Dict key?** | ✅ | ❌ | ✅ | ❌ | ❌ |
| **Memory** | Low | Medium | Low | High | High |
| **Lookup speed** | Scan | Scan | Scan | Direct | Direct |
| **Best for** | Text | Ordered data | Fixed data | Unique items | Key-value |

---

> 🚀 Use this as your **quick reference** before interviews!
