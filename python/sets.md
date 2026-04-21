# 🔵 Sets in Python - Complete Guide (Zero to Hero)

> A set is an **unordered, mutable collection** with **no duplicate elements**.

---

## 🔹 What is a Set?

A set is a collection where:
- Every element is **unique** (no duplicates)
- Elements have **no fixed order**
- You can **add and remove** items

### 🧠 Real-World Analogy

> 👉 Think of a set like a **bag of unique marbles**:
> - You can't have two identical marbles
> - There's no "first" or "second" marble — they're just in the bag
> - You can add or remove marbles

---

## 🔹 Creating Sets

### 🔸 Using Curly Braces `{}`

```python
# Set of integers
numbers = {1, 2, 3, 4, 5}

# Set of strings
fruits = {"apple", "banana", "cherry"}

# Mixed types
mixed = {1, "hello", 3.14, True}
```

⚠️ **Cannot create an empty set with `{}`!**

```python
# ❌ This creates an empty DICTIONARY, not a set!
empty = {}
print(type(empty))   # <class 'dict'>

# ✅ Use set() for empty set
empty = set()
print(type(empty))   # <class 'set'>
```

### 🔸 Using `set()` Constructor

```python
# From a list
nums = set([1, 2, 2, 3, 3, 3])
print(nums)   # {1, 2, 3}  ← duplicates removed!

# From a string
chars = set("hello")
print(chars)   # {'h', 'e', 'l', 'o'}  ← duplicate 'l' removed, order may vary

# From a tuple
nums = set((1, 2, 3))
print(nums)   # {1, 2, 3}

# From a range
nums = set(range(5))
print(nums)   # {0, 1, 2, 3, 4}
```

### 🔸 Duplicates Are Automatically Removed

```python
numbers = {1, 2, 2, 3, 3, 3, 4, 4, 4, 4}
print(numbers)   # {1, 2, 3, 4}
```

✔ This is the **#1 use case** for sets — removing duplicates.

---

## 🔹 Set Characteristics

| Property | Value |
|----------|-------|
| Ordered | ❌ No fixed order |
| Mutable | ✅ Can add/remove items |
| Duplicates | ❌ Not allowed |
| Indexed | ❌ Cannot access by position |
| Elements must be immutable | ✅ str, int, float, tuple (NOT list, dict, set) |

### 🔸 Elements Must Be Hashable (Immutable)

```python
# ✅ Valid elements
s = {1, "hello", 3.14, (1, 2), True}

# ❌ Invalid elements
s = {[1, 2]}      # TypeError: unhashable type: 'list'
s = {{"a": 1}}    # TypeError: unhashable type: 'dict'
s = {{1, 2}}      # TypeError: unhashable type: 'set'
```

### 🔸 Bool/Int Collision (Same as Dicts)

```python
s = {True, 1, False, 0}
print(s)   # {True, False}  ← True==1 and False==0, treated as same
```

---

## 🔹 Cannot Access by Index ⚠️

```python
fruits = {"apple", "banana", "cherry"}

# ❌ No indexing
print(fruits[0])   # TypeError: 'set' object is not subscriptable

# ❌ No slicing
print(fruits[0:2])   # TypeError
```

✔ To access set elements, use **loops** or convert to a **list**.

```python
# Using a loop
for fruit in fruits:
    print(fruit)

# Convert to list
fruit_list = list(fruits)
print(fruit_list[0])   # first element (order may vary)
```

---

## 🔹 Adding Items

### 🔸 add() — Add ONE Item

```python
fruits = {"apple", "banana"}
fruits.add("cherry")
print(fruits)   # {'apple', 'banana', 'cherry'}

# Adding a duplicate — no error, just ignored
fruits.add("apple")
print(fruits)   # {'apple', 'banana', 'cherry'}  ← no change
```

### 🔸 update() — Add MULTIPLE Items

```python
fruits = {"apple", "banana"}
fruits.update(["cherry", "date"])
print(fruits)   # {'apple', 'banana', 'cherry', 'date'}
```

✔ `update()` accepts **any iterable** — list, tuple, set, string:

```python
s = {1, 2}
s.update((3, 4))        # tuple
s.update({5, 6})         # set
s.update(range(7, 9))   # range
print(s)   # {1, 2, 3, 4, 5, 6, 7, 8}
```

⚠️ **String trap** (same as list's `extend()`):

```python
s = {"apple"}
s.update("hi")
print(s)   # {'apple', 'h', 'i'}  ← each character added separately!

# ✅ To add the whole string as one element, use add()
s = {"apple"}
s.add("hi")
print(s)   # {'apple', 'hi'}
```

### 🔸 add() vs update()

| Method | Adds | Example |
|--------|------|---------|
| `add(x)` | One element | `s.add("cherry")` |
| `update(iterable)` | Multiple elements from iterable | `s.update(["cherry", "date"])` |

---

## 🔹 Removing Items

### 🔸 remove() — Remove by Value (Error if Missing)

```python
fruits = {"apple", "banana", "cherry"}
fruits.remove("banana")
print(fruits)   # {'apple', 'cherry'}

fruits.remove("grape")   # ❌ KeyError: 'grape'
```

### 🔸 discard() — Remove by Value (NO Error if Missing)

```python
fruits = {"apple", "banana", "cherry"}
fruits.discard("banana")
print(fruits)   # {'apple', 'cherry'}

fruits.discard("grape")   # ✅ No error, just ignored
```

### 🔸 remove() vs discard() (INTERVIEW FAVORITE 🔥)

| Method | Missing Element? |
|--------|:---:|
| `remove(x)` | ❌ KeyError |
| `discard(x)` | ✅ No error |

✔ **Use `discard()` when you're unsure if the element exists.**

### 🔸 pop() — Remove a Random Element

```python
fruits = {"apple", "banana", "cherry"}
removed = fruits.pop()
print(removed)   # (random element)
print(fruits)    # remaining elements
```

⚠️ You **cannot control** which element is removed. Sets are unordered.

### 🔸 clear() — Remove All Elements

```python
fruits = {"apple", "banana", "cherry"}
fruits.clear()
print(fruits)   # set()
```

---

## 🔹 Set Operations (VERY IMPORTANT 🔥)

This is where sets truly shine. Set operations come from **mathematical set theory**.

Let's use these two sets for all examples:

```python
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}
```

### 🔸 Union — All Elements from Both Sets

```
A ∪ B = everything in A or B (or both)
```

```python
print(a | b)            # {1, 2, 3, 4, 5, 6, 7, 8}
print(a.union(b))       # {1, 2, 3, 4, 5, 6, 7, 8}
```

### 🔸 Intersection — Only Common Elements

```
A ∩ B = only what's in BOTH A and B
```

```python
print(a & b)                # {4, 5}
print(a.intersection(b))    # {4, 5}
```

### 🔸 Difference — In A but NOT in B

```
A - B = what's in A but not in B
```

```python
print(a - b)              # {1, 2, 3}
print(a.difference(b))    # {1, 2, 3}

print(b - a)              # {6, 7, 8}
print(b.difference(a))    # {6, 7, 8}
```

⚠️ **Order matters!** `a - b` ≠ `b - a`

### 🔸 Symmetric Difference — In A or B, but NOT Both

```
A △ B = what's in A or B, but NOT in both
```

```python
print(a ^ b)                        # {1, 2, 3, 6, 7, 8}
print(a.symmetric_difference(b))    # {1, 2, 3, 6, 7, 8}
```

### 🔸 Visual Summary

```
A = {1, 2, 3, 4, 5}
B = {4, 5, 6, 7, 8}

Union (A | B):              {1, 2, 3, 4, 5, 6, 7, 8}
Intersection (A & B):       {4, 5}
Difference (A - B):         {1, 2, 3}
Difference (B - A):         {6, 7, 8}
Symmetric Diff (A ^ B):     {1, 2, 3, 6, 7, 8}
```

### 🔸 Operations Summary Table

| Operation | Operator | Method | Result |
|-----------|:--------:|--------|--------|
| Union | `\|` | `union()` | All from both |
| Intersection | `&` | `intersection()` | Common only |
| Difference | `-` | `difference()` | In A, not in B |
| Symmetric Diff | `^` | `symmetric_difference()` | In A or B, not both |

---

## 🔹 Update Operations (Modify In-Place)

The operations above return **new sets**. These modify the **original set**:

```python
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}

# Union update
a_copy = a.copy()
a_copy |= b                          # or a_copy.update(b)
print(a_copy)   # {1, 2, 3, 4, 5, 6, 7, 8}

# Intersection update
a_copy = a.copy()
a_copy &= b                          # or a_copy.intersection_update(b)
print(a_copy)   # {4, 5}

# Difference update
a_copy = a.copy()
a_copy -= b                           # or a_copy.difference_update(b)
print(a_copy)   # {1, 2, 3}

# Symmetric difference update
a_copy = a.copy()
a_copy ^= b                           # or a_copy.symmetric_difference_update(b)
print(a_copy)   # {1, 2, 3, 6, 7, 8}
```

---

## 🔹 Set Comparisons

### 🔸 Subset — Is A Contained in B?

```python
a = {1, 2, 3}
b = {1, 2, 3, 4, 5}

print(a <= b)            # True
print(a.issubset(b))     # True
print(b.issubset(a))     # False
```

### 🔸 Superset — Does A Contain B?

```python
print(b >= a)              # True
print(b.issuperset(a))     # True
```

### 🔸 Proper Subset / Superset

```python
a = {1, 2, 3}
b = {1, 2, 3}

print(a <= b)   # True   (subset — can be equal)
print(a < b)    # False  (proper subset — must be strictly smaller)

c = {1, 2, 3, 4}
print(a < c)    # True   (proper subset)
```

### 🔸 Disjoint — No Common Elements?

```python
a = {1, 2, 3}
b = {4, 5, 6}
c = {3, 4, 5}

print(a.isdisjoint(b))   # True   (no common elements)
print(a.isdisjoint(c))   # False  (3 is common)
```

---

## 🔹 Frozen Sets (Immutable Sets)

A `frozenset` is a set that **cannot be changed** after creation.

```python
fs = frozenset([1, 2, 3, 4, 5])
print(fs)        # frozenset({1, 2, 3, 4, 5})
print(type(fs))  # <class 'frozenset'>

# ❌ Cannot modify
fs.add(6)       # AttributeError
fs.remove(1)    # AttributeError
```

### 🔸 Why Use Frozensets?

Because they're **immutable and hashable**, they can be:

```python
# ✅ Used as dictionary keys
d = {frozenset({1, 2}): "pair"}
print(d[frozenset({1, 2})])   # pair

# ✅ Used as elements of another set
s = {frozenset({1, 2}), frozenset({3, 4})}
print(s)   # {frozenset({1, 2}), frozenset({3, 4})}

# ❌ Regular sets cannot do this
s = {{1, 2}, {3, 4}}   # TypeError: unhashable type: 'set'
```

### 🔸 Frozenset Operations

All **read-only** operations work (union, intersection, etc.):

```python
a = frozenset({1, 2, 3})
b = frozenset({3, 4, 5})

print(a | b)    # frozenset({1, 2, 3, 4, 5})
print(a & b)    # frozenset({3})
print(a - b)    # frozenset({1, 2})
```

---

## 🔹 Set Comprehensions

```python
# Normal way
squares = set()
for i in range(5):
    squares.add(i * i)

# Comprehension
squares = {i * i for i in range(5)}
print(squares)   # {0, 1, 4, 9, 16}
```

### 🔸 With Condition

```python
evens = {i for i in range(20) if i % 2 == 0}
print(evens)   # {0, 2, 4, 6, 8, 10, 12, 14, 16, 18}
```

### 🔸 From a String

```python
text = "hello world"
unique_chars = {char for char in text if char != " "}
print(unique_chars)   # {'h', 'e', 'l', 'o', 'w', 'r', 'd'}
```

---

## 🔹 Iterating Through Sets

### 🔸 Using for loop

```python
fruits = {"apple", "banana", "cherry"}

for fruit in fruits:
    print(fruit)
```

⚠️ Order is **not guaranteed** and may vary between runs.

### 🔸 With enumerate()

```python
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

---

## 🔹 Built-in Functions with Sets

```python
nums = {3, 1, 4, 1, 5, 9}   # duplicates removed: {1, 3, 4, 5, 9}

print(len(nums))      # 5
print(sum(nums))      # 22
print(min(nums))      # 1
print(max(nums))      # 9
print(sorted(nums))   # [1, 3, 4, 5, 9]  ← returns a LIST
```

### 🔸 any() and all()

```python
print(any({0, 0, 1}))    # True
print(all({1, 2, 3}))    # True
print(all({0, 1, 2}))    # False
```

---

## 🔹 Converting Between Sets and Other Types

```python
# List to Set (removes duplicates)
my_list = [1, 2, 2, 3, 3]
my_set = set(my_list)
print(my_set)   # {1, 2, 3}

# Set to List
my_list = list(my_set)
print(my_list)   # [1, 2, 3]

# String to Set
chars = set("hello")
print(chars)   # {'h', 'e', 'l', 'o'}

# Set to Tuple
my_tuple = tuple(my_set)

# Set to Sorted List
sorted_list = sorted(my_set)
```

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Empty Set with `{}`

```python
# ❌ This is a dict, not a set!
empty = {}
print(type(empty))   # <class 'dict'>

# ✅ Correct
empty = set()
```

### 🔸 Mistake 2: Trying to Index a Set

```python
s = {1, 2, 3}
print(s[0])   # ❌ TypeError: 'set' object is not subscriptable
```

### 🔸 Mistake 3: Adding Mutable Elements

```python
s = set()
s.add([1, 2])   # ❌ TypeError: unhashable type: 'list'

# ✅ Use a tuple instead
s.add((1, 2))   # Works!
```

### 🔸 Mistake 4: Expecting Order

```python
s = {3, 1, 4, 1, 5}
print(s)   # {1, 3, 4, 5}  ← order is NOT guaranteed!

# If you need order, convert to sorted list
print(sorted(s))   # [1, 3, 4, 5]
```

### 🔸 Mistake 5: update() with a String

```python
s = {"apple"}
s.update("hi")
print(s)   # {'apple', 'h', 'i'}  ← characters added separately!

# ✅ Use add() for a single string
s.add("hi")
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Remove Duplicates from a List

#### Manual way:

```python
nums = [1, 2, 2, 3, 4, 3, 5]
unique = []

for num in nums:
    if num not in unique:
        unique.append(num)

print(unique)   # [1, 2, 3, 4, 5]
```

#### Pythonic shortcut (order preserved — Python 3.7+):

```python
unique = list(dict.fromkeys(nums))
print(unique)   # [1, 2, 3, 4, 5]
```

#### Using set (**⚠️ order NOT guaranteed**):

```python
unique = list(set(nums))
```

---

### ✅ 2. Find Common Elements in Two Lists

#### Manual way:

```python
list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]
common = []

for item in list1:
    if item in list2 and item not in common:
        common.append(item)

print(common)   # [4, 5]
```

#### Pythonic shortcut:

```python
common = list(set(list1) & set(list2))
print(common)   # [4, 5]
```

---

### ✅ 3. Find Elements in List1 but NOT in List2

#### Manual way:

```python
list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]
diff = []

for item in list1:
    if item not in list2:
        diff.append(item)

print(diff)   # [1, 2, 3]
```

#### Pythonic shortcut:

```python
diff = list(set(list1) - set(list2))
print(diff)   # [1, 2, 3]
```

---

### ✅ 4. Check if Two Lists Have Any Common Elements

#### Manual way:

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]
has_common = False

for item in list1:
    if item in list2:
        has_common = True
        break

print(has_common)   # False
```

#### Pythonic shortcut:

```python
has_common = not set(list1).isdisjoint(set(list2))
print(has_common)   # False

# Alternative using intersection
has_common = bool(set(list1) & set(list2))
print(has_common)   # False
```

---

### ✅ 5. Count Unique Elements

#### Manual way:

```python
nums = [1, 2, 2, 3, 3, 3, 4]
unique = []

for num in nums:
    if num not in unique:
        unique.append(num)

print(f"Unique count: {len(unique)}")   # Unique count: 4
```

#### Pythonic shortcut:

```python
print(f"Unique count: {len(set(nums))}")   # Unique count: 4
```

---

### ✅ 6. Find Symmetric Difference (Elements in Either but Not Both)

#### Manual way:

```python
list1 = [1, 2, 3, 4]
list2 = [3, 4, 5, 6]
sym_diff = []

for item in list1:
    if item not in list2:
        sym_diff.append(item)

for item in list2:
    if item not in list1:
        sym_diff.append(item)

print(sym_diff)   # [1, 2, 5, 6]
```

#### Pythonic shortcut:

```python
sym_diff = list(set(list1) ^ set(list2))
print(sym_diff)   # [1, 2, 5, 6]
```

---

### ✅ 7. Check if One List is a Subset of Another

#### Manual way:

```python
list1 = [1, 2, 3]
list2 = [1, 2, 3, 4, 5]
is_subset = True

for item in list1:
    if item not in list2:
        is_subset = False
        break

print(f"Subset: {is_subset}")   # Subset: True
```

#### Pythonic shortcut:

```python
print(f"Subset: {set(list1) <= set(list2)}")   # Subset: True
```

---

## 🔹 All Set Methods — Quick Reference 📌

| Method | Description |
|--------|-------------|
| `add(x)` | Add one element |
| `update(iterable)` | Add multiple elements |
| `remove(x)` | Remove element (KeyError if missing) |
| `discard(x)` | Remove element (no error if missing) |
| `pop()` | Remove and return random element |
| `clear()` | Remove all elements |
| `union(s)` or `\|` | All from both sets |
| `intersection(s)` or `&` | Common elements |
| `difference(s)` or `-` | In self, not in other |
| `symmetric_difference(s)` or `^` | In either, not both |
| `issubset(s)` or `<=` | Is self contained in other? |
| `issuperset(s)` or `>=` | Does self contain other? |
| `isdisjoint(s)` | No common elements? |
| `copy()` | Shallow copy |

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| Set | Unordered, mutable, no duplicates |
| Creating | `{1, 2, 3}`, `set()`, `set(list)` |
| Empty set | `set()` (NOT `{}`) |
| No indexing | Cannot access by position |
| Elements | Must be immutable (hashable) |
| `add()` | Add one element |
| `update()` | Add multiple elements |
| `remove()` vs `discard()` | Error vs no error on missing |
| Union `\|` | All from both |
| Intersection `&` | Common only |
| Difference `-` | In A, not in B |
| Symmetric Diff `^` | In A or B, not both |
| Subset `<=` | Is A inside B? |
| Disjoint | No common elements? |
| Frozenset | Immutable set, can be dict key |
| Comprehension | `{x for x in ... if ...}` |
| Main use | Remove duplicates, membership testing, set math |

---

> 🚀 **What's Next?**
> 👉 Exception Handling
> 👉 OOP (Classes, Objects, Inheritance)
> 👉 File Handling
