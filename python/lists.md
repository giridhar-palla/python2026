# 📋 Lists in Python - Complete Guide (Zero to Hero)

> A list is an **ordered, mutable collection** that can hold items of **any type** and allows **duplicates**.

---

## 🔹 What is a List?

A list is a collection of items stored in a **specific order**. You can add, remove, and change items after creation.

### 🧠 Real-World Analogy

> 👉 Think of a list like a **shopping list**:
> - Items are in a specific order (first item, second item...)
> - You can add new items
> - You can cross out (remove) items
> - You can change an item (replace "milk" with "almond milk")
> - You can have the same item twice

---

## 🔹 Creating Lists

### 🔸 Using Square Brackets `[]`

```python
# Empty list
empty = []

# List of integers
numbers = [1, 2, 3, 4, 5]

# List of strings
fruits = ["apple", "banana", "cherry"]

# Mixed types
mixed = [1, "hello", 3.14, True, None]

# Nested list (list inside a list)
nested = [[1, 2], [3, 4], [5, 6]]
```

### 🔸 Using `list()` Constructor

```python
# From a string
chars = list("Python")
print(chars)   # ['P', 'y', 't', 'h', 'o', 'n']

# From a tuple
nums = list((1, 2, 3))
print(nums)   # [1, 2, 3]

# From a range
nums = list(range(5))
print(nums)   # [0, 1, 2, 3, 4]

# From a set (order may vary)
nums = list({3, 1, 2})
print(nums)   # [1, 2, 3]
```

### 🔸 Checking the Type

```python
fruits = ["apple", "banana"]
print(type(fruits))   # <class 'list'>
```

---

## 🔹 List Characteristics

| Property | Value |
|----------|-------|
| Ordered | ✅ Items have a fixed position |
| Mutable | ✅ Can add, remove, change items |
| Allows Duplicates | ✅ Same value can appear multiple times |
| Allows Mixed Types | ✅ Can hold int, str, bool, etc. together |
| Indexed | ✅ Access items by position (starting from 0) |

---

## 🔹 Accessing Items (Indexing)

Each item has a **position (index)** starting from **0**.

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]
```

| Index | 0 | 1 | 2 | 3 | 4 |
|-------|---|---|---|---|---|
| Item | apple | banana | cherry | date | elderberry |

### 🔸 Positive Indexing (Left to Right)

```python
print(fruits[0])   # apple
print(fruits[1])   # banana
print(fruits[4])   # elderberry
```

### 🔸 Negative Indexing (Right to Left)

| Index | -5 | -4 | -3 | -2 | -1 |
|-------|----|----|----|----|-----|
| Item | apple | banana | cherry | date | elderberry |

```python
print(fruits[-1])   # elderberry  (last item)
print(fruits[-2])   # date
print(fruits[-5])   # apple       (first item)
```

### 🔸 Index Out of Range ⚠️

```python
print(fruits[10])   # ❌ IndexError: list index out of range
```

---

## 🔹 List Slicing

Extract a **portion** of the list.

### Syntax:

```
list[start : end : step]
```

- `start` → included ✅
- `end` → excluded ❌

```python
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(nums[2:6])      # [2, 3, 4, 5]
print(nums[:4])        # [0, 1, 2, 3]       (start defaults to 0)
print(nums[5:])        # [5, 6, 7, 8, 9]    (end defaults to last)
print(nums[:])         # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]  (full copy)
print(nums[::2])       # [0, 2, 4, 6, 8]    (every 2nd item)
print(nums[1::2])      # [1, 3, 5, 7, 9]    (every 2nd, starting from index 1)
print(nums[::-1])      # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]  (reversed)
```

### 🔸 Slicing Creates a NEW List

```python
original = [1, 2, 3, 4, 5]
sliced = original[1:4]

sliced[0] = 99
print(sliced)     # [99, 3, 4]
print(original)   # [1, 2, 3, 4, 5]  ← original unchanged
```

✔ Slicing creates a **shallow copy**. Modifying the slice doesn't affect the original.

---

## 🔹 List Length

```python
fruits = ["apple", "banana", "cherry"]
print(len(fruits))   # 3
```

### 🔸 Empty List Check

```python
items = []

# ❌ Verbose way
if len(items) == 0:
    print("Empty")

# ✅ Pythonic way
if not items:
    print("Empty")
```

---

## 🔹 List Unpacking (IMPORTANT 🔥)

### 🔸 Basic Unpacking

```python
nums = [10, 20, 30]

a, b, c = nums
print(a)   # 10
print(b)   # 20
print(c)   # 30
```

⚠️ Count must match:

```python
a, b = [10, 20, 30]      # ❌ ValueError: too many values to unpack
a, b, c, d = [10, 20]    # ❌ ValueError: not enough values to unpack
```

### 🔸 `*` Splat Unpacking — Catch Extra Items

```python
head, *tail = [1, 2, 3, 4, 5]
print(head)   # 1
print(tail)   # [2, 3, 4, 5]

first, *middle, last = [1, 2, 3, 4, 5]
print(first)    # 1
print(middle)   # [2, 3, 4]
print(last)     # 5

*rest, last = [1, 2, 3, 4, 5]
print(rest)   # [1, 2, 3, 4]
print(last)   # 5
```

✔ The `*` variable collects all the extra values into a **list**.

### 🔸 Combining Lists via Unpacking

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

# Using + (normal way)
combined = list1 + list2
print(combined)   # [1, 2, 3, 4, 5, 6]

# Using * unpacking (modern Pythonic way)
combined = [*list1, *list2]
print(combined)   # [1, 2, 3, 4, 5, 6]

# You can even add extra items in between
combined = [*list1, 99, *list2]
print(combined)   # [1, 2, 3, 99, 4, 5, 6]
```

### 🔸 Swap Using Unpacking

```python
a = 10
b = 20

a, b = b, a
print(a, b)   # 20 10
```

---

## 🔹 Changing Items (Lists are Mutable! 🔥)

### 🔸 Change a Single Item

```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "blueberry"
print(fruits)   # ['apple', 'blueberry', 'cherry']
```

### 🔸 Change Multiple Items (Slice Assignment)

```python
nums = [1, 2, 3, 4, 5]
nums[1:4] = [20, 30, 40]
print(nums)   # [1, 20, 30, 40, 5]
```

### 🔸 Replace with Different Number of Items

```python
nums = [1, 2, 3, 4, 5]
nums[1:4] = [20, 30]
print(nums)   # [1, 20, 30, 5]  ← list shrunk!

nums = [1, 2, 3, 4, 5]
nums[1:3] = [20, 30, 40, 50]
print(nums)   # [1, 20, 30, 40, 50, 4, 5]  ← list grew!
```

---

## 🔹 Adding Items

### 🔸 append() — Add ONE Item to the End

```python
fruits = ["apple", "banana"]
fruits.append("cherry")
print(fruits)   # ['apple', 'banana', 'cherry']
```

⚠️ `append()` adds the item **as a single element**, even if it's a list:

```python
fruits = ["apple", "banana"]
fruits.append(["cherry", "date"])
print(fruits)   # ['apple', 'banana', ['cherry', 'date']]  ← nested list!
```

### 🔸 extend() — Add MULTIPLE Items (Merge Lists)

```python
fruits = ["apple", "banana"]
fruits.extend(["cherry", "date"])
print(fruits)   # ['apple', 'banana', 'cherry', 'date']
```

✔ `extend()` works with **any iterable** — list, tuple, set, range, string:

```python
nums = [1, 2, 3]

nums.extend((4, 5))        # tuple
print(nums)   # [1, 2, 3, 4, 5]

nums.extend({6, 7})        # set (order may vary)
print(nums)   # [1, 2, 3, 4, 5, 6, 7]

nums.extend(range(8, 10))  # range
print(nums)   # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### ⚠️ TRAP: extend() with a String

```python
fruits = ["apple", "banana"]
fruits.extend("kiwi")
print(fruits)   # ['apple', 'banana', 'k', 'i', 'w', 'i']  ← each CHARACTER added!
```

🧠 Because a string is an iterable of characters, `extend()` adds **each character separately**. If you want to add the whole string as one item, use `append()`:

```python
fruits = ["apple", "banana"]
fruits.append("kiwi")
print(fruits)   # ['apple', 'banana', 'kiwi']  ✅
```

### 🔸 append() vs extend() (INTERVIEW FAVORITE 🔥)

```python
a = [1, 2, 3]
a.append([4, 5])
print(a)   # [1, 2, 3, [4, 5]]   ← adds as ONE nested item

b = [1, 2, 3]
b.extend([4, 5])
print(b)   # [1, 2, 3, 4, 5]     ← adds EACH item individually
```

| Method | What It Does | Result |
|--------|-------------|--------|
| `append(x)` | Adds `x` as a single element | `[1, 2, [3, 4]]` |
| `extend(x)` | Adds each item from `x` | `[1, 2, 3, 4]` |

### 🔸 insert() — Add at a Specific Position

```python
fruits = ["apple", "cherry"]
fruits.insert(1, "banana")
print(fruits)   # ['apple', 'banana', 'cherry']
```

`insert(index, item)` — inserts `item` **before** the given index.

```python
nums = [1, 3, 4]
nums.insert(0, 0)     # insert at beginning
print(nums)   # [0, 1, 3, 4]

nums.insert(2, 2)     # insert at index 2
print(nums)   # [0, 1, 2, 3, 4]
```

⚠️ **Conceptual note:** Inserting anywhere other than the end forces Python to **shift all the following items over** to make room. For very large lists, inserting at the beginning or middle can be slow. `append()` (adding to the end) does not have this problem.

⚠️ **Conceptual note:** Inserting anywhere other than the end forces Python to **shift all the following items** over to make room. Inserting at the beginning of a very large list is slow because every single item must be moved. `append()` (adding to the end) does not have this problem.

### 🔸 Concatenation with `+`

```python
a = [1, 2, 3]
b = [4, 5, 6]
c = a + b
print(c)   # [1, 2, 3, 4, 5, 6]
```

⚠️ This creates a **new list**. The originals are unchanged.

### 🔸 Repetition with `*`

```python
zeros = [0] * 5
print(zeros)   # [0, 0, 0, 0, 0]

pattern = [1, 2] * 3
print(pattern)   # [1, 2, 1, 2, 1, 2]
```

⚠️ **Trap with mutable items:**

```python
# ❌ Dangerous — all inner lists are the SAME object!
matrix = [[0]] * 3
print(matrix)        # [[0], [0], [0]]

matrix[0][0] = 99
print(matrix)        # [[99], [99], [99]]  ← ALL changed!

# ✅ Safe way
matrix = [[0] for i in range(3)]
matrix[0][0] = 99
print(matrix)        # [[99], [0], [0]]  ← only first changed
```

---

## 🔹 Removing Items

### 🔸 remove() — Remove by VALUE (First Occurrence)

```python
fruits = ["apple", "banana", "cherry", "banana"]
fruits.remove("banana")
print(fruits)   # ['apple', 'cherry', 'banana']  ← only first "banana" removed
```

⚠️ If value doesn't exist:

```python
fruits.remove("grape")   # ❌ ValueError: list.remove(x): x not in list
```

✔ Check first:

```python
if "grape" in fruits:
    fruits.remove("grape")
```

⚠️ **Conceptual note:** Like `insert()`, removing an item from the beginning or middle forces Python to **shift all the following items** to fill the gap. Removing from the end (`pop()`) does not have this problem.

### 🔸 pop() — Remove by INDEX (Returns the Item)

```python
fruits = ["apple", "banana", "cherry"]

removed = fruits.pop(1)
print(removed)   # banana
print(fruits)    # ['apple', 'cherry']
```

#### pop() with No Argument — Removes Last Item

```python
fruits = ["apple", "banana", "cherry"]
last = fruits.pop()
print(last)      # cherry
print(fruits)    # ['apple', 'banana']
```

### 🔸 del — Delete by Index or Slice

```python
fruits = ["apple", "banana", "cherry", "date"]

del fruits[1]
print(fruits)   # ['apple', 'cherry', 'date']

del fruits[0:2]
print(fruits)   # ['date']
```

#### Delete Entire List

```python
del fruits   # list is completely deleted
# print(fruits)   # ❌ NameError
```

### 🔸 clear() — Remove All Items (Keep the List)

```python
fruits = ["apple", "banana", "cherry"]
fruits.clear()
print(fruits)   # []  (empty list, but list still exists)
```

### 🔸 remove() vs pop() vs del vs clear()

| Method | Removes By | Returns Removed? | Error if Missing? |
|--------|-----------|:---:|:---:|
| `remove(value)` | Value | ❌ | ✅ ValueError |
| `pop(index)` | Index | ✅ Yes | ✅ IndexError |
| `pop()` | Last item | ✅ Yes | ✅ IndexError (if empty) |
| `del list[i]` | Index/Slice | ❌ | ✅ IndexError |
| `clear()` | All items | ❌ | ❌ |

---

## 🔹 Searching in Lists

### 🔸 `in` — Check if Item Exists

```python
fruits = ["apple", "banana", "cherry"]

print("banana" in fruits)       # True
print("grape" in fruits)        # False
print("grape" not in fruits)    # True
```

### 🔸 index() — Find Position of Item

```python
fruits = ["apple", "banana", "cherry", "banana"]

print(fruits.index("banana"))   # 1  (first occurrence)
print(fruits.index("cherry"))   # 2
```

⚠️ If not found:

```python
fruits.index("grape")   # ❌ ValueError
```

✔ Check with `in` first, or use try-except.

### 🔸 count() — Count Occurrences

```python
nums = [1, 2, 3, 2, 1, 2]
print(nums.count(2))   # 3
print(nums.count(5))   # 0
```

---

## 🔹 Sorting Lists (VERY IMPORTANT 🔥)

### 🔸 sort() — Sort In-Place (Modifies Original)

```python
nums = [3, 1, 4, 1, 5, 9, 2, 6]
nums.sort()
print(nums)   # [1, 1, 2, 3, 4, 5, 6, 9]
```

#### Reverse Sort

```python
nums = [3, 1, 4, 1, 5, 9]
nums.sort(reverse=True)
print(nums)   # [9, 5, 4, 3, 1, 1]
```

#### Sort Strings

```python
names = ["Charlie", "Alice", "Bob"]
names.sort()
print(names)   # ['Alice', 'Bob', 'Charlie']
```

#### Sort by Custom Key

```python
names = ["Charlie", "Alice", "Bob"]

# Sort by length
names.sort(key=len)
print(names)   # ['Bob', 'Alice', 'Charlie']

# Sort by last character
names.sort(key=lambda name: name[-1])
print(names)   # ['Charlie', 'Alice', 'Bob']
```

### 🔸 sorted() — Returns a NEW Sorted List (Original Unchanged)

```python
nums = [3, 1, 4, 1, 5]

sorted_nums = sorted(nums)
print(sorted_nums)   # [1, 1, 3, 4, 5]
print(nums)          # [3, 1, 4, 1, 5]  ← original unchanged!
```

### 🔸 sort() vs sorted() (INTERVIEW FAVORITE 🔥)

| Feature | `sort()` | `sorted()` |
|---------|----------|------------|
| Modifies original? | ✅ Yes | ❌ No (returns new list) |
| Returns | `None` | New sorted list |
| Works on | Lists only | Any iterable |

```python
nums = [3, 1, 2]

# ❌ Common mistake
result = nums.sort()
print(result)   # None!  (sort() returns None)

# ✅ Correct
result = sorted(nums)
print(result)   # [1, 2, 3]
```

### 🔸 reverse() — Reverse In-Place

```python
nums = [1, 2, 3, 4, 5]
nums.reverse()
print(nums)   # [5, 4, 3, 2, 1]
```

#### reversed() — Returns Iterator (Original Unchanged)

```python
nums = [1, 2, 3, 4, 5]
rev = list(reversed(nums))
print(rev)    # [5, 4, 3, 2, 1]
print(nums)   # [1, 2, 3, 4, 5]  ← unchanged
```

---

## 🔹 Copying Lists (VERY IMPORTANT 🔥)

### 🔸 The Problem: Assignment is NOT a Copy

```python
original = [1, 2, 3]
copy = original   # NOT a copy! Both point to the SAME list

copy.append(4)
print(copy)       # [1, 2, 3, 4]
print(original)   # [1, 2, 3, 4]  ← original also changed!
```

🧠 `copy = original` makes both variables point to the **same object** in memory.

### 🔸 Shallow Copy Methods

```python
original = [1, 2, 3]

# Method 1: .copy()
copy1 = original.copy()

# Method 2: slicing
copy2 = original[:]

# Method 3: list() constructor
copy3 = list(original)
```

Now modifying the copy doesn't affect the original:

```python
copy1.append(4)
print(copy1)      # [1, 2, 3, 4]
print(original)   # [1, 2, 3]  ← safe!
```

### 🔸 Shallow Copy Limitation ⚠️ (Nested Lists)

```python
original = [[1, 2], [3, 4]]
copy = original.copy()   # shallow copy

copy[0][0] = 99
print(copy)       # [[99, 2], [3, 4]]
print(original)   # [[99, 2], [3, 4]]  ← inner list also changed!
```

🧠 Shallow copy copies the **outer list**, but the inner lists are still **shared references**.

### 🔸 Deep Copy (For Nested Lists)

```python
import copy

original = [[1, 2], [3, 4]]
deep = copy.deepcopy(original)

deep[0][0] = 99
print(deep)       # [[99, 2], [3, 4]]
print(original)   # [[1, 2], [3, 4]]  ← safe!
```

✔ `deepcopy()` creates completely independent copies at **all levels**.

### 🔸 Copy Summary

| Method | Shallow? | Deep? | Nested Safe? |
|--------|:---:|:---:|:---:|
| `=` assignment | ❌ Not a copy | ❌ | ❌ |
| `.copy()` | ✅ | ❌ | ❌ |
| `[:]` slicing | ✅ | ❌ | ❌ |
| `list()` | ✅ | ❌ | ❌ |
| `copy.deepcopy()` | ✅ | ✅ | ✅ |

---

## 🔹 Iterating Through Lists

### 🔸 Basic — Using while loop

```python
fruits = ["apple", "banana", "cherry"]
i = 0

while i < len(fruits):
    print(fruits[i])
    i = i + 1
```

### 🔸 Using for loop

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

### 🔸 With Index — Using enumerate()

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

Output:
```
0: apple
1: banana
2: cherry
```

### 🔸 Loop Over Two Lists — Using zip()

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

for name, age in zip(names, ages):
    print(f"{name} is {age}")
```

---

## 🔹 List Comprehensions (VERY IMPORTANT 🔥)

A one-line way to create lists from loops.

### 🔸 Basic Comprehension

```python
# Normal way
squares = []
for i in range(5):
    squares.append(i * i)

# Comprehension
squares = [i * i for i in range(5)]
print(squares)   # [0, 1, 4, 9, 16]
```

### 🔸 With Condition (Filter)

```python
# Normal way
evens = []
for i in range(10):
    if i % 2 == 0:
        evens.append(i)

# Comprehension
evens = [i for i in range(10) if i % 2 == 0]
print(evens)   # [0, 2, 4, 6, 8]
```

### 🔸 With if-else (Transform)

```python
labels = ["Even" if i % 2 == 0 else "Odd" for i in range(5)]
print(labels)   # ['Even', 'Odd', 'Even', 'Odd', 'Even']
```

⚠️ `if-else` goes **before** `for`. Plain `if` (filter) goes **after** `for`.

### 🔸 Nested Comprehension

```python
# Flatten a 2D list
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

flat = [num for row in matrix for num in row]
print(flat)   # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 🔸 When NOT to Use Comprehensions

```python
# ❌ Too complex — use a regular loop
result = [func(x) for x in data if x > 0 and x < 100 and x not in excluded]

# ✅ Better as a loop
result = []
for x in data:
    if x > 0 and x < 100 and x not in excluded:
        result.append(func(x))
```

---

## 🔹 Nested Lists (2D Lists / Matrices)

### 🔸 Creating a 2D List

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

### 🔸 Accessing Items

```python
print(matrix[0])      # [1, 2, 3]   (first row)
print(matrix[0][0])   # 1           (row 0, column 0)
print(matrix[1][2])   # 6           (row 1, column 2)
print(matrix[-1][-1]) # 9           (last row, last column)
```

### 🔸 Iterating a 2D List

#### Using while loop (basic way):

```python
i = 0
while i < len(matrix):
    j = 0
    while j < len(matrix[i]):
        print(matrix[i][j], end=" ")
        j = j + 1
    print()
    i = i + 1
```

#### Using for loop:

```python
for row in matrix:
    for item in row:
        print(item, end=" ")
    print()
```

Output:
```
1 2 3
4 5 6
7 8 9
```

### 🔸 Modifying Items

```python
matrix[1][1] = 99
print(matrix[1])   # [4, 99, 6]
```

### 🔸 Creating a Matrix Safely

```python
# ❌ Wrong — all rows are the SAME object
matrix = [[0] * 3] * 3
matrix[0][0] = 1
print(matrix)   # [[1, 0, 0], [1, 0, 0], [1, 0, 0]]  ← all changed!

# ✅ Correct — each row is independent
matrix = [[0] * 3 for i in range(3)]
matrix[0][0] = 1
print(matrix)   # [[1, 0, 0], [0, 0, 0], [0, 0, 0]]  ← only first changed
```

---

## 🔹 Useful Built-in Functions for Lists

```python
nums = [3, 1, 4, 1, 5, 9, 2, 6]

print(len(nums))     # 8
print(sum(nums))     # 31
print(min(nums))     # 1
print(max(nums))     # 9
print(sorted(nums))  # [1, 1, 2, 3, 4, 5, 6, 9]
```

### 🔸 any() and all()

```python
nums = [0, 1, 2, 3]

print(any(nums))   # True   (at least one truthy value)
print(all(nums))   # False  (0 is falsy)

nums2 = [1, 2, 3]
print(all(nums2))  # True   (all truthy)
```

### 🔸 map() with Lists

```python
nums = [1, 2, 3, 4, 5]

# Double each number
doubled = list(map(lambda x: x * 2, nums))
print(doubled)   # [2, 4, 6, 8, 10]

# Convert to strings
str_nums = list(map(str, nums))
print(str_nums)   # ['1', '2', '3', '4', '5']
```

### 🔸 filter() with Lists

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)   # [2, 4, 6, 8, 10]
```

---

## 🔹 Lists as Stacks and Queues

### 🔸 Stack (LIFO — Last In, First Out)

```python
stack = []

# Push
stack.append("a")
stack.append("b")
stack.append("c")
print(stack)   # ['a', 'b', 'c']

# Pop
print(stack.pop())   # c
print(stack.pop())   # b
print(stack)         # ['a']
```

### 🔸 Queue (FIFO — First In, First Out)

```python
from collections import deque

queue = deque()

# Enqueue
queue.append("a")
queue.append("b")
queue.append("c")

# Dequeue
print(queue.popleft())   # a
print(queue.popleft())   # b
print(queue)             # deque(['c'])
```

⚠️ Don't use `list.pop(0)` for queues — it's slow because it shifts all elements. Use `deque` instead.

---

## 🔹 Bridging Strings and Lists (VERY COMMON IN INTERVIEWS 🔥)

`split()` and `join()` are **string methods**, but they are essential for list manipulation. Interviews constantly require converting between strings and lists.

### 🔸 String → List: split()

```python
text = "apple banana cherry"
words = text.split(" ")
print(words)   # ['apple', 'banana', 'cherry']

# Split by comma
csv = "one,two,three"
items = csv.split(",")
print(items)   # ['one', 'two', 'three']

# Split with no argument (splits by any whitespace, removes extras)
text = "  hello   world  "
words = text.split()
print(words)   # ['hello', 'world']
```

### 🔸 List → String: join()

```python
fruits = ["apple", "banana", "cherry"]

text = ", ".join(fruits)
print(text)   # apple, banana, cherry

text = " - ".join(fruits)
print(text)   # apple - banana - cherry

text = "".join(fruits)
print(text)   # applebananacherry
```

⚠️ `join()` only works with **lists of strings**:

```python
nums = [1, 2, 3]

# ❌ Wrong — integers can't be joined
# ", ".join(nums)   # TypeError

# ✅ Convert to strings first
print(", ".join(str(n) for n in nums))   # 1, 2, 3
```

### 🔸 Common Interview Pattern: Word Reversal

```python
text = "Python is easy"

# Step 1: Split into list
words = text.split()          # ['Python', 'is', 'easy']

# Step 2: Reverse the list
words.reverse()               # ['easy', 'is', 'Python']

# Step 3: Join back into string
result = " ".join(words)
print(result)   # easy is Python
```

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Modifying List While Iterating

```python
nums = [1, 2, 3, 4, 5]

# ❌ Dangerous — skips elements
for num in nums:
    if num % 2 == 0:
        nums.remove(num)

# ✅ Safe — iterate over a copy
for num in nums[:]:
    if num % 2 == 0:
        nums.remove(num)

# ✅ Even better — create a new list
odds = [num for num in nums if num % 2 != 0]
```

### 🔸 Mistake 2: sort() Returns None

```python
nums = [3, 1, 2]

# ❌ Wrong
sorted_nums = nums.sort()
print(sorted_nums)   # None!

# ✅ Correct
sorted_nums = sorted(nums)
print(sorted_nums)   # [1, 2, 3]
```

### 🔸 Mistake 3: `=` is Not a Copy

```python
a = [1, 2, 3]
b = a          # NOT a copy!
b.append(4)
print(a)       # [1, 2, 3, 4]  ← a also changed!

# ✅ Use .copy() or [:]
b = a.copy()
```

### 🔸 Mistake 4: `[[0]] * n` Trap

```python
# ❌ All rows share the same reference
grid = [[0] * 3] * 3

# ✅ Each row is independent
grid = [[0] * 3 for i in range(3)]
```

---

## 🔹 All List Methods — Quick Reference 📌

| Method | Description | Returns |
|--------|-------------|---------|
| `append(x)` | Add item to end | None |
| `extend(iterable)` | Add all items from iterable | None |
| `insert(i, x)` | Insert item at index | None |
| `remove(x)` | Remove first occurrence of value | None |
| `pop(i)` | Remove and return item at index | Item |
| `pop()` | Remove and return last item | Item |
| `clear()` | Remove all items | None |
| `index(x)` | Find index of first occurrence | Int |
| `count(x)` | Count occurrences | Int |
| `sort()` | Sort in-place | None |
| `reverse()` | Reverse in-place | None |
| `copy()` | Shallow copy | New list |

---

## 🔹 Interview Programs 💡

### ✅ 1. Reverse a List

#### Manual way (using while loop):

```python
nums = [1, 2, 3, 4, 5]
reversed_list = []
i = len(nums) - 1

while i >= 0:
    reversed_list.append(nums[i])
    i = i - 1

print(reversed_list)   # [5, 4, 3, 2, 1]
```

#### Manual way (two-pointer swap):

```python
nums = [1, 2, 3, 4, 5]
left = 0
right = len(nums) - 1

while left < right:
    nums[left], nums[right] = nums[right], nums[left]
    left = left + 1
    right = right - 1

print(nums)   # [5, 4, 3, 2, 1]
```

#### Pythonic shortcuts:

```python
nums = [1, 2, 3, 4, 5]

print(nums[::-1])          # [5, 4, 3, 2, 1]  (new list)
nums.reverse()             # reverses in-place
print(list(reversed(nums)))  # returns iterator
```

---

### ✅ 2. Find the Largest Element

#### Manual way:

```python
nums = [3, 7, 2, 9, 4]
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

### ✅ 3. Find the Second Largest Element

```python
nums = [3, 7, 2, 9, 4, 9]
largest = nums[0]
second = float('-inf')

for num in nums:
    if num > largest:
        second = largest
        largest = num
    elif num > second and num != largest:
        second = num

print(f"Second largest: {second}")   # Second largest: 7
```

#### Pythonic shortcut:

```python
unique_sorted = sorted(set(nums), reverse=True)
print(f"Second largest: {unique_sorted[1]}")   # 7
```

---

### ✅ 4. Remove Duplicates from a List

#### Manual way (preserving order):

```python
nums = [1, 2, 2, 3, 4, 3, 5]
unique = []

for num in nums:
    if num not in unique:
        unique.append(num)

print(unique)   # [1, 2, 3, 4, 5]
```

#### Pythonic shortcut (**⚠️ order is NOT guaranteed**):

```python
unique = list(set(nums))
print(unique)   # [1, 2, 3, 4, 5]  (order may vary)
```

**Warning:** `set()` **completely destroys the original order**. In coding interviews, if the problem says "preserve order," using `set()` alone will fail the test case.

#### Pythonic shortcut (preserving order — Python 3.7+):

```python
unique = list(dict.fromkeys(nums))
print(unique)   # [1, 2, 3, 4, 5]  (order preserved)
```

---

### ✅ 5. Flatten a Nested List

#### Manual way:

```python
nested = [[1, 2], [3, 4], [5, 6]]
flat = []

for sublist in nested:
    for item in sublist:
        flat.append(item)

print(flat)   # [1, 2, 3, 4, 5, 6]
```

#### Comprehension shortcut:

```python
flat = [item for sublist in nested for item in sublist]
print(flat)   # [1, 2, 3, 4, 5, 6]
```

---

### ✅ 6. Find Common Elements in Two Lists

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

#### Pythonic shortcut (using sets):

```python
common = list(set(list1) & set(list2))
print(common)   # [4, 5]
```

---

### ✅ 7. Rotate a List by K Positions

```python
nums = [1, 2, 3, 4, 5]
k = 2

# Manual way — rotate right by k
rotated = []
n = len(nums)
i = 0
while i < n:
    new_index = (i + k) % n
    rotated.append(0)
    i = i + 1

i = 0
while i < n:
    new_index = (i + k) % n
    rotated[new_index] = nums[i]
    i = i + 1

print(rotated)   # [4, 5, 1, 2, 3]
```

#### Pythonic shortcut (slicing):

```python
nums = [1, 2, 3, 4, 5]
k = 2

rotated = nums[-k:] + nums[:-k]
print(rotated)   # [4, 5, 1, 2, 3]
```

---

### ✅ 8. Check if List is Sorted

#### Manual way:

```python
nums = [1, 2, 3, 4, 5]
is_sorted = True

i = 0
while i < len(nums) - 1:
    if nums[i] > nums[i + 1]:
        is_sorted = False
        break
    i = i + 1

print(f"Sorted: {is_sorted}")   # Sorted: True
```

#### Pythonic shortcut:

```python
print(nums == sorted(nums))   # True
```

---

### ✅ 9. Merge Two Sorted Lists

```python
list1 = [1, 3, 5, 7]
list2 = [2, 4, 6, 8]
merged = []

i = 0
j = 0

while i < len(list1) and j < len(list2):
    if list1[i] <= list2[j]:
        merged.append(list1[i])
        i = i + 1
    else:
        merged.append(list2[j])
        j = j + 1

# Add remaining items
while i < len(list1):
    merged.append(list1[i])
    i = i + 1

while j < len(list2):
    merged.append(list2[j])
    j = j + 1

print(merged)   # [1, 2, 3, 4, 5, 6, 7, 8]
```

#### Pythonic shortcut:

```python
merged = sorted(list1 + list2)
print(merged)   # [1, 2, 3, 4, 5, 6, 7, 8]
```

---

### ✅ 10. Find Missing Number (1 to N)

Given a list of numbers from 1 to N with one missing, find the missing number.

#### Manual way:

```python
nums = [1, 2, 4, 5, 6]
n = 6

expected_sum = 0
i = 1
while i <= n:
    expected_sum = expected_sum + i
    i = i + 1

actual_sum = 0
for num in nums:
    actual_sum = actual_sum + num

missing = expected_sum - actual_sum
print(f"Missing: {missing}")   # Missing: 3
```

#### Pythonic shortcut:

```python
n = 6
expected = sum(range(1, n + 1))
actual = sum(nums)
print(f"Missing: {expected - actual}")   # Missing: 3
```

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| List | Ordered, mutable, allows duplicates |
| Creating | `[]`, `list()`, `list(range())` |
| Indexing | `list[0]`, `list[-1]` |
| Slicing | `list[start:end:step]` |
| Length | `len(list)` |
| Mutable | Can change items after creation |
| `append()` | Add one item to end |
| `extend()` | Add multiple items |
| `insert()` | Add at specific position |
| `remove()` | Remove by value |
| `pop()` | Remove by index, returns item |
| `del` | Delete by index or slice |
| `clear()` | Remove all items |
| `sort()` | Sort in-place (returns None) |
| `sorted()` | Returns new sorted list |
| `reverse()` | Reverse in-place |
| `copy()` | Shallow copy |
| `deepcopy()` | Deep copy (for nested) |
| `index()` | Find position |
| `count()` | Count occurrences |
| Comprehension | `[expr for x in list if cond]` |
| Nested lists | `list[row][col]` |
| Stack | `append()` + `pop()` |
| Queue | Use `deque` from collections |

---

> 🚀 **Next:** Tuples in Python →
