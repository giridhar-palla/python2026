# ➕ Operators in Python - Complete Guide (Zero to Hero)

> An operator is a **symbol** that performs an operation on one or more values (operands).

---

## 🔹 What is an Operator?

An operator takes **values** (called operands) and **does something** with them.

```python
result = 10 + 5
#        ↑  ↑ ↑
#   operand op operand
```

### 🧠 Real-World Analogy

> 👉 Think of operators like **actions**:
> - `+` is like **adding** items to a cart
> - `-` is like **removing** items
> - `*` is like **multiplying** a recipe
> - `==` is like **comparing** two prices

---

## 🔹 Types of Operators in Python

| Type | Symbols |
|------|---------|
| Arithmetic | `+`, `-`, `*`, `/`, `//`, `%`, `**` |
| Assignment | `=`, `+=`, `-=`, `*=`, etc. |
| Comparison | `==`, `!=`, `>`, `<`, `>=`, `<=` |
| Logical | `and`, `or`, `not` |
| Identity | `is`, `is not` |
| Membership | `in`, `not in` |
| Bitwise | `&`, `|`, `^`, `~`, `<<`, `>>` |
| Walrus | `:=` |

---

## 🔹 1️⃣ Arithmetic Operators

| Operator | Name | Example | Result |
|:--------:|------|---------|:------:|
| `+` | Addition | `10 + 3` | `13` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `10 * 3` | `30` |
| `/` | Division | `10 / 3` | `3.333...` |
| `//` | Floor Division | `10 // 3` | `3` |
| `%` | Modulus (Remainder) | `10 % 3` | `1` |
| `**` | Exponentiation (Power) | `2 ** 3` | `8` |

### 🔸 Division `/` — Always Returns Float

```python
print(10 / 2)    # 5.0   (not 5!)
print(10 / 3)    # 3.3333333333333335
print(7 / 2)     # 3.5
```

✔ `/` **always** returns a `float`, even if the result is a whole number.

### 🔸 Floor Division `//` — Rounds Down to Integer

```python
print(10 // 3)    # 3
print(7 // 2)     # 3
print(-7 // 2)    # -4   ← rounds DOWN, not toward zero!
```

⚠️ **Negative floor division trap (INTERVIEW 🔥):**

```python
print(7 // 2)     # 3    (rounds down from 3.5)
print(-7 // 2)    # -4   (rounds down from -3.5 → -4, NOT -3!)
```

🧠 Floor division always rounds **toward negative infinity**, not toward zero.

### 🔸 Modulus `%` — Remainder

```python
print(10 % 3)    # 1    (10 ÷ 3 = 3 remainder 1)
print(15 % 5)    # 0    (perfectly divisible)
print(7 % 2)     # 1    (odd number check!)
```

#### Common Uses:

```python
# Check even or odd
num = 7
if num % 2 == 0:
    print("Even")
else:
    print("Odd")

# Check divisibility
if num % 5 == 0:
    print("Divisible by 5")

# Get last digit
print(12345 % 10)   # 5
```

### 🔸 Exponentiation `**` — Power

```python
print(2 ** 3)     # 8     (2 × 2 × 2)
print(5 ** 2)     # 25    (5 × 5)
print(9 ** 0.5)   # 3.0   (square root!)
print(2 ** 10)    # 1024
```

#### Pythonic shortcut for power:

```python
print(pow(2, 3))      # 8
print(pow(2, 3, 5))   # 3   (2**3 % 5 = 8 % 5 = 3)
```

✔ `pow(base, exp, mod)` is useful for modular exponentiation (common in competitive programming).

### 🔸 Arithmetic with Different Types

```python
print(10 + 2.5)      # 12.5   (int + float → float)
print(True + 10)     # 11     (bool + int → int)
print(True + 1.5)    # 2.5    (bool + float → float)
```

### 🔸 Arithmetic with Strings (Special Cases)

```python
print("Hello" + " World")   # Hello World  (concatenation)
print("Ha" * 3)              # HaHaHa      (repetition)

# ❌ Cannot subtract or divide strings
# print("Hello" - "o")      # TypeError
# print("Hello" / 2)        # TypeError
```

### 🔸 Unary Operators (`+x`, `-x`)

Unary operators work on a **single** operand.

```python
x = 5

print(+x)    # 5   (positive — rarely used, doesn't change anything)
print(-x)    # -5  (negation — flips the sign)
```

```python
x = -3
print(-x)    # 3   (negating a negative gives positive)
print(+x)    # -3  (unary + doesn't change the value)
```

⚠️ Chaining unary operators:

```python
print(--5)    # 5   (not decrement! It's -(-5) = 5)
print(+-5)    # -5
print(-+5)    # -5
```

✔ Python has **no `++` or `--`** operators. `--5` is just `-(-(5))`.

### 🔸 String Formatting Operator `%` (Legacy)

The `%` operator is also used for **old-style string formatting**. You'll see this in legacy codebases.

```python
name = "Giridhar"
age = 25

print("My name is %s and I am %d years old" % (name, age))
# My name is Giridhar and I am 25 years old
```

| Placeholder | Meaning |
|:-----------:|---------|
| `%s` | String |
| `%d` | Integer |
| `%f` | Float |
| `%.2f` | Float with 2 decimals |

⚠️ This is the **old way**. Prefer **f-strings** in modern Python:

```python
print(f"My name is {name} and I am {age} years old")
```

---

### 🔸 The `@` Operator (Matrix Multiplication — Python 3.5+)

The `@` operator was introduced for **matrix multiplication**. It's used with libraries like **NumPy**.

```python
# Requires NumPy
import numpy as np

a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

result = a @ b
print(result)
```

Output:
```
[[19 22]
 [43 50]]
```

🧠 `a @ b` is the same as `np.matmul(a, b)` or `a.dot(b)`.

✔ You won't use `@` in basic Python, but it's a **valid Python operator** and may come up in interviews about Python 3 features.

### 🔸 `*` and `**` — Arithmetic vs Unpacking (Don't Confuse! ⚠️)

The symbols `*` and `**` have **two completely different meanings** depending on context:

| Context | `*` Means | `**` Means |
|---------|-----------|------------|
| **Arithmetic** | Multiplication: `3 * 4` = 12 | Power: `2 ** 3` = 8 |
| **Function definition** | Collect args: `def f(*args)` | Collect kwargs: `def f(**kwargs)` |
| **Function call** | Unpack list: `f(*[1,2,3])` | Unpack dict: `f(**{"a":1})` |
| **Assignment** | Catch extras: `a, *b = [1,2,3]` | — |

```python
# Arithmetic
print(3 * 4)       # 12
print(2 ** 3)      # 8

# Unpacking
nums = [1, 2, 3]
print(*nums)       # 1 2 3  (unpacks into print arguments)
```

✔ Context determines the meaning. Don't confuse multiplication `*` with unpacking `*`.

---

## 🔹 2️⃣ Assignment Operators

| Operator | Example | Same As |
|:--------:|---------|---------|
| `=` | `x = 5` | `x = 5` |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 3` | `x = x * 3` |
| `/=` | `x /= 3` | `x = x / 3` |
| `//=` | `x //= 3` | `x = x // 3` |
| `%=` | `x %= 3` | `x = x % 3` |
| `**=` | `x **= 3` | `x = x ** 3` |
| `&=` | `x &= 3` | `x = x & 3` |
| `|=` | `x |= 3` | `x = x | 3` |
| `^=` | `x ^= 3` | `x = x ^ 3` |
| `>>=` | `x >>= 3` | `x = x >> 3` |
| `<<=` | `x <<= 3` | `x = x << 3` |

### 🔸 Examples

```python
x = 10

x += 5    # x = 10 + 5 = 15
print(x)  # 15

x -= 3    # x = 15 - 3 = 12
print(x)  # 12

x *= 2    # x = 12 * 2 = 24
print(x)  # 24

x //= 5   # x = 24 // 5 = 4
print(x)  # 4

x **= 3   # x = 4 ** 3 = 64
print(x)  # 64
```

⚠️ **Python does NOT have `++` or `--` operators!**

```python
x = 10

# ❌ These don't work like C/Java
# x++    # SyntaxError
# x--    # SyntaxError

# ✅ Use this instead
x += 1   # increment
x -= 1   # decrement
```

---

## 🔹 3️⃣ Comparison Operators

Return `True` or `False`.

| Operator | Meaning | Example | Result |
|:--------:|---------|---------|:------:|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater or equal | `5 >= 5` | `True` |
| `<=` | Less or equal | `5 <= 3` | `False` |

### 🔸 Comparing Different Types

```python
print(10 == 10.0)    # True   (int and float with same value)
print(True == 1)     # True   (bool is subclass of int)
print(False == 0)    # True
print("10" == 10)    # False  (string vs int — different types)
```

### 🔸 Chained Comparisons (Python Special ✨)

```python
x = 15

# Normal way
if x >= 10 and x <= 20:
    print("In range")

# Python way — chained
if 10 <= x <= 20:
    print("In range")

print(1 < 5 < 10)      # True
print(1 < 5 > 3)       # True  (1 < 5 AND 5 > 3)
```

### 🔸 `=` vs `==` (COMMON MISTAKE ⚠️)

```python
x = 10     # Assignment — puts 10 into x
x == 10    # Comparison — checks if x equals 10, returns True/False
```

---

## 🔹 4️⃣ Logical Operators

| Operator | Meaning | Example | Result |
|:--------:|---------|---------|:------:|
| `and` | Both True | `True and False` | `False` |
| `or` | At least one True | `True or False` | `True` |
| `not` | Reverse | `not True` | `False` |

### 🔸 Truth Tables

#### `and`
| A | B | A and B |
|:---:|:---:|:---:|
| True | True | **True** |
| True | False | False |
| False | True | False |
| False | False | False |

#### `or`
| A | B | A or B |
|:---:|:---:|:---:|
| True | True | **True** |
| True | False | **True** |
| False | True | **True** |
| False | False | False |

#### `not`
| A | not A |
|:---:|:---:|
| True | **False** |
| False | **True** |

### 🔸 Short-Circuit Evaluation (INTERVIEW FAVORITE 🔥)

Python **stops evaluating** as soon as the result is determined.

#### `and` — stops at first False

```python
print(False and print("Hello"))   # False  (print never executes!)
```

🧠 Since the first operand is `False`, `and` already knows the result is `False`. It doesn't bother checking the second operand.

#### `or` — stops at first True

```python
print(True or print("Hello"))   # True  (print never executes!)
```

### 🔸 Logical Operators Return Values (Not Just True/False!)

This is a **critical interview concept**:

```python
# 'and' returns the first falsy value, or the last value if all truthy
print(0 and 5)        # 0     (first falsy)
print(3 and 5)        # 5     (all truthy → last value)
print("" and "Hi")    # ""    (first falsy)

# 'or' returns the first truthy value, or the last value if all falsy
print(0 or 5)         # 5     (first truthy)
print(3 or 5)         # 3     (first truthy)
print("" or "Hi")     # "Hi"  (first truthy)
print(0 or "" or [])  # []    (all falsy → last value)
```

#### Practical Use: Default Values

```python
name = ""
display_name = name or "Anonymous"
print(display_name)   # Anonymous

name = "Giridhar"
display_name = name or "Anonymous"
print(display_name)   # Giridhar
```

### 🔸 Operator Precedence

```
not  →  and  →  or
```

```python
print(True or False and False)     # True
# Same as: True or (False and False) → True or False → True

print((True or False) and False)   # False
```

---

## 🔹 5️⃣ Identity Operators

Check if two variables point to the **same object in memory**.

| Operator | Meaning |
|:--------:|---------|
| `is` | Same object |
| `is not` | Different objects |

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)      # True   (same value)
print(a is b)      # False  (different objects in memory)
print(a is c)      # True   (c points to same object as a)
print(a is not b)  # True
```

### 🔸 `is` vs `==`

| Operator | Checks |
|:--------:|--------|
| `==` | Same **value** |
| `is` | Same **object in memory** |

### 🔸 When to Use `is`

```python
# ✅ Use 'is' for None checks
x = None
if x is None:
    print("No value")

# ✅ Use 'is' for singleton comparisons (True, False, None)
if x is True:
    pass

# ❌ Don't use 'is' for value comparisons
if x is 10:    # unreliable!
    pass
```

### 🔸 Small Integer Caching (INTERVIEW 🔥)

```python
a = 256
b = 256
print(a is b)   # True   (cached by Python)

a = 257
b = 257
print(a is b)   # May be False  (not cached)
```

✔ Python caches integers from **-5 to 256**. Beyond that, `is` may return `False` even for equal values.

---

## 🔹 6️⃣ Membership Operators

Check if a value **exists in** a sequence.

| Operator | Meaning |
|:--------:|---------|
| `in` | Value exists in sequence |
| `not in` | Value does NOT exist |

```python
# In a list
fruits = ["apple", "banana", "cherry"]
print("banana" in fruits)       # True
print("grape" not in fruits)    # True

# In a string
text = "Python Programming"
print("Python" in text)         # True
print("Java" in text)           # False

# In a dictionary (checks KEYS, not values)
person = {"name": "Giridhar", "age": 25}
print("name" in person)         # True
print("Giridhar" in person)     # False  (checks keys only!)
print(25 in person.values())    # True   (check values explicitly)

# In a set
numbers = {1, 2, 3, 4, 5}
print(3 in numbers)             # True
```

### 🔸 Performance of `in` (INTERVIEW 🔥)

| Data Structure | `in` Performance |
|---------------|:---:|
| `list` | O(n) — slow for large lists |
| `tuple` | O(n) — same as list |
| `set` | O(1) — very fast! |
| `dict` | O(1) — very fast! |
| `str` | O(n) — substring search |

✔ If you need frequent membership checks, use a **set** or **dict** instead of a list.

---

## 🔹 7️⃣ Bitwise Operators

Operate on numbers at the **binary (bit) level**.

| Operator | Name | Example | Result |
|:--------:|------|---------|:------:|
| `&` | AND | `5 & 3` | `1` |
| `\|` | OR | `5 \| 3` | `7` |
| `^` | XOR | `5 ^ 3` | `6` |
| `~` | NOT | `~5` | `-6` |
| `<<` | Left Shift | `5 << 1` | `10` |
| `>>` | Right Shift | `5 >> 1` | `2` |

### 🔸 Understanding with Binary

```
5 in binary = 101
3 in binary = 011
```

#### AND `&` — Both bits must be 1

```
  101  (5)
& 011  (3)
-----
  001  (1)
```

```python
print(5 & 3)   # 1
```

#### OR `|` — At least one bit must be 1

```
  101  (5)
| 011  (3)
-----
  111  (7)
```

```python
print(5 | 3)   # 7
```

#### XOR `^` — Bits must be different

```
  101  (5)
^ 011  (3)
-----
  110  (6)
```

```python
print(5 ^ 3)   # 6
```

#### NOT `~` — Flip all bits

```python
print(~5)    # -6
```

🧠 Formula: `~n = -(n + 1)`

```python
print(~0)    # -1
print(~1)    # -2
print(~(-3)) # 2
```

#### Left Shift `<<` — Multiply by 2

```python
print(5 << 1)   # 10   (5 × 2)
print(5 << 2)   # 20   (5 × 4)
print(5 << 3)   # 40   (5 × 8)
```

🧠 `n << k` = `n × 2^k`

#### Right Shift `>>` — Divide by 2 (floor)

```python
print(10 >> 1)   # 5    (10 ÷ 2)
print(10 >> 2)   # 2    (10 ÷ 4)
print(5 >> 1)    # 2    (5 ÷ 2, floored)
```

🧠 `n >> k` = `n ÷ 2^k` (floored)

### 🔸 Common Interview Uses of Bitwise

```python
# Check if number is even or odd (faster than %)
num = 7
if num & 1:
    print("Odd")
else:
    print("Even")

# Swap two numbers without temp variable
a = 5
b = 3
a = a ^ b
b = a ^ b
a = a ^ b
print(a, b)   # 3 5

# Multiply by 2
print(10 << 1)   # 20

# Divide by 2
print(10 >> 1)   # 5
```

---

## 🔹 8️⃣ Walrus Operator `:=` (Python 3.8+)

Assigns a value **and** returns it in the same expression.

### 🔸 Without Walrus (Normal Way)

```python
text = input("Enter something: ")
while text != "quit":
    print(f"You entered: {text}")
    text = input("Enter something: ")
```

### 🔸 With Walrus Operator

```python
while (text := input("Enter something: ")) != "quit":
    print(f"You entered: {text}")
```

✔ The walrus operator `:=` assigns `input()` to `text` AND checks the condition in one line.

### 🔸 In List Comprehensions

```python
# Without walrus — calls len() twice
results = []
for s in ["hello", "hi", "hey", "a"]:
    n = len(s)
    if n > 2:
        results.append(n)

# With walrus — calls len() once
results = [n for s in ["hello", "hi", "hey", "a"] if (n := len(s)) > 2]
print(results)   # [5, 3]
```

### 🔸 In if Statements

```python
import re

text = "My phone is 123-456-7890"

# Without walrus
match = re.search(r"\d{3}-\d{3}-\d{4}", text)
if match:
    print(f"Found: {match.group()}")

# With walrus
if match := re.search(r"\d{3}-\d{3}-\d{4}", text):
    print(f"Found: {match.group()}")
```

⚠️ Don't overuse the walrus operator. Use it only when it genuinely makes code cleaner.

---

## 🔹 Operator Precedence (VERY IMPORTANT 🔥)

From **highest** to **lowest** priority:

| Priority | Operator | Description |
|:--------:|----------|-------------|
| 1 | `()` | Parentheses |
| 2 | `**` | Exponentiation |
| 3 | `~`, `+x`, `-x` | Unary NOT, positive, negative |
| 4 | `*`, `/`, `//`, `%` | Multiplication, division |
| 5 | `+`, `-` | Addition, subtraction |
| 6 | `<<`, `>>` | Bitwise shifts |
| 7 | `&` | Bitwise AND |
| 8 | `^` | Bitwise XOR |
| 9 | `\|` | Bitwise OR |
| 10 | `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `in` | Comparisons |
| 11 | `not` | Logical NOT |
| 12 | `and` | Logical AND |
| 13 | `or` | Logical OR |
| 14 | `:=` | Walrus |

### 🔸 Examples

```python
# ** is right-associative
print(2 ** 3 ** 2)    # 512  (2 ** 9, NOT 8 ** 2)

# * before +
print(2 + 3 * 4)      # 14  (not 20)

# Parentheses override everything
print((2 + 3) * 4)    # 20

# not before and, and before or
print(True or False and False)    # True
print((True or False) and False)  # False
```

### 🔸 PEMDAS / BODMAS Reminder

```
P — Parentheses
E — Exponents
M/D — Multiplication / Division (left to right)
A/S — Addition / Subtraction (left to right)
```

```python
result = 2 + 3 * 4 ** 2 / 8 - 1
# Step 1: 4 ** 2 = 16
# Step 2: 3 * 16 = 48
# Step 3: 48 / 8 = 6.0
# Step 4: 2 + 6.0 = 8.0
# Step 5: 8.0 - 1 = 7.0
print(result)   # 7.0
```

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: `=` vs `==`

```python
# ❌ Assignment, not comparison
if x = 10:    # SyntaxError

# ✅ Comparison
if x == 10:
    print("Ten")
```

### 🔸 Mistake 2: Integer Division with Negatives

```python
print(7 // 2)     # 3
print(-7 // 2)    # -4   ← NOT -3!
```

### 🔸 Mistake 3: `is` vs `==` for Values

```python
a = 1000
b = 1000
print(a == b)   # True
print(a is b)   # May be False!  ← use == for values
```

### 🔸 Mistake 4: `and`/`or` Return Values, Not Just Booleans

```python
result = 0 or "default"
print(result)   # "default"  (not True!)

result = "hello" and "world"
print(result)   # "world"  (not True!)
```

### 🔸 Mistake 5: `in` with Dictionaries

```python
d = {"name": "Python"}
print("name" in d)     # True   (checks keys)
print("Python" in d)   # False  (doesn't check values!)
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Check Even/Odd Using Bitwise

```python
num = 7

# Using modulus (normal way)
if num % 2 == 0:
    print("Even")
else:
    print("Odd")

# Using bitwise AND (faster way)
if num & 1:
    print("Odd")
else:
    print("Even")
```

---

### ✅ 2. Swap Without Temp Variable

#### Using XOR:

```python
a = 10
b = 20

a = a ^ b
b = a ^ b
a = a ^ b

print(a, b)   # 20 10
```

#### Pythonic shortcut:

```python
a, b = b, a
```

---

### ✅ 3. Check if a Number is a Power of 2

```python
def is_power_of_two(n):
    if n <= 0:
        return False
    return (n & (n - 1)) == 0

print(is_power_of_two(16))   # True
print(is_power_of_two(18))   # False
```

🧠 Powers of 2 in binary have exactly one `1` bit:
```
1  = 0001
2  = 0010
4  = 0100
8  = 1000
16 = 10000
```

`n & (n-1)` removes the lowest set bit. If the result is 0, there was only one bit → power of 2.

---

### ✅ 4. Find the Odd One Out (XOR Trick)

Given a list where every number appears twice except one, find the unique number.

```python
numbers = [2, 3, 5, 3, 2]
result = 0

for num in numbers:
    result = result ^ num

print(f"Unique number: {result}")   # Unique number: 5
```

🧠 XOR properties: `a ^ a = 0` and `a ^ 0 = a`. Pairs cancel out, leaving the unique number.

---

## 🔹 Complete Summary 📌

| Operator Type | Operators | Key Point |
|--------------|-----------|-----------|
| Arithmetic | `+`, `-`, `*`, `/`, `//`, `%`, `**` | `/` always returns float |
| Assignment | `=`, `+=`, `-=`, etc. | No `++` or `--` in Python |
| Comparison | `==`, `!=`, `>`, `<`, `>=`, `<=` | Chaining: `1 < x < 10` |
| Logical | `and`, `or`, `not` | Return values, not just bool |
| Identity | `is`, `is not` | Checks memory, not value |
| Membership | `in`, `not in` | `set` is O(1), `list` is O(n) |
| Bitwise | `&`, `\|`, `^`, `~`, `<<`, `>>` | Used in optimization tricks |
| Walrus | `:=` | Assign + return in one expression |

---

> 🚀 **Next:** Lists in Python →
