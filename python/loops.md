# 🔁 Loops in Python - Complete Guide (Zero to Hero)

> Loops let you **repeat** a block of code multiple times without writing it again and again.

---

## 🔹 What is a Loop?

A loop executes a block of code **repeatedly** until a condition is met.

### 🧠 Real-World Analogy

> 👉 Think of a loop like a **washing machine cycle**:
> - It keeps spinning (repeating) until the timer runs out
> - Each spin is one **iteration**
> - When the condition is met (timer = 0), it stops

---

## 🔹 Types of Loops in Python

| Loop | When to Use |
|------|------------|
| `while` | When you **don't know** how many times to repeat |
| `for` | When you **know** how many times to repeat, or iterating over a sequence |

---

## 🔹 The `while` Loop

Repeats **as long as** the condition is `True`.

### Syntax:

```python
while condition:
    # code to repeat
```

### 🔸 Basic Example

```python
count = 1

while count <= 5:
    print(count)
    count = count + 1
```

Output:
```
1
2
3
4
5
```

### 🔸 Step-by-Step Execution

| Iteration | count | count <= 5? | Action |
|:---------:|:-----:|:-----------:|--------|
| 1 | 1 | True | Print 1, count becomes 2 |
| 2 | 2 | True | Print 2, count becomes 3 |
| 3 | 3 | True | Print 3, count becomes 4 |
| 4 | 4 | True | Print 4, count becomes 5 |
| 5 | 5 | True | Print 5, count becomes 6 |
| 6 | 6 | False | **Loop stops** |

### 🔸 Counting Backwards

```python
count = 5

while count >= 1:
    print(count)
    count = count - 1
```

Output:
```
5
4
3
2
1
```

### 🔸 Infinite Loop ⚠️ (VERY IMPORTANT)

If the condition **never becomes False**, the loop runs forever.

```python
# ❌ INFINITE LOOP — never stops!
count = 1

while count <= 5:
    print(count)
    # forgot to increment count!
```

✔ Always make sure the condition will **eventually become False**.

### 🔸 Intentional Infinite Loop (with break)

```python
while True:
    user_input = input("Type 'quit' to exit: ")
    if user_input == "quit":
        print("Goodbye!")
        break
```

✔ `while True` creates an intentional infinite loop. Use `break` to exit.

### 🔸 while Loop with User Input

```python
total = 0

while True:
    num = input("Enter a number (or 'done' to finish): ")
    if num == "done":
        break
    total = total + int(num)

print(f"Total: {total}")
```

---

## 🔹 The `for` Loop

Iterates over a **sequence** (list, string, range, tuple, etc.).

### Syntax:

```python
for variable in sequence:
    # code to repeat
```

### 🔸 Looping Through a List

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

Output:
```
apple
banana
cherry
```

### 🔸 Looping Through a String

```python
text = "Python"

for char in text:
    print(char)
```

Output:
```
P
y
t
h
o
n
```

### 🔸 Looping Through a Tuple

```python
colors = ("red", "green", "blue")

for color in colors:
    print(color)
```

### 🔸 Looping Through a Dictionary

```python
person = {"name": "Giridhar", "age": 25, "city": "Hyderabad"}

# Loop through keys (default)
for key in person:
    print(key)

# Loop through values
for value in person.values():
    print(value)

# Loop through key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")
```

Output of last one:
```
name: Giridhar
age: 25
city: Hyderabad
```

---

## 🔹 The `range()` Function (VERY IMPORTANT 🔥)

`range()` generates a sequence of numbers. Used heavily with `for` loops.

### 🔸 range(stop) — From 0 to stop-1

```python
for i in range(5):
    print(i)
```

Output:
```
0
1
2
3
4
```

✔ `range(5)` generates: 0, 1, 2, 3, 4 (does NOT include 5).

### 🔸 range(start, stop) — From start to stop-1

```python
for i in range(1, 6):
    print(i)
```

Output:
```
1
2
3
4
5
```

### 🔸 range(start, stop, step) — With Step

```python
# Count by 2
for i in range(0, 10, 2):
    print(i)
```

Output:
```
0
2
4
6
8
```

### 🔸 Counting Backwards with range()

```python
for i in range(5, 0, -1):
    print(i)
```

Output:
```
5
4
3
2
1
```

### 🔸 range() Returns a Range Object (Not a List)

```python
r = range(5)
print(r)          # range(0, 5)
print(type(r))    # <class 'range'>
print(list(r))    # [0, 1, 2, 3, 4]
```

✔ `range()` is **memory efficient** — it doesn't create all numbers at once. It generates them **one at a time**.

---

## 🔹 for Loop with Index — enumerate() (IMPORTANT 🔥)

When you need both the **index** and the **value**.

### 🔸 Without enumerate (manual way):

```python
fruits = ["apple", "banana", "cherry"]
i = 0

while i < len(fruits):
    print(f"Index {i}: {fruits[i]}")
    i = i + 1
```

### 🔸 Using range (another way):

```python
fruits = ["apple", "banana", "cherry"]

for i in range(len(fruits)):
    print(f"Index {i}: {fruits[i]}")
```

### 🔸 Using enumerate (Pythonic way ✅):

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"Index {index}: {fruit}")
```

Output:
```
Index 0: apple
Index 1: banana
Index 2: cherry
```

### ⚠️ COMMON TRAP: enumerate() Variable Order (IMPORTANT 🔥)

`enumerate()` yields `(index, value)` — in **that specific order**. Beginners constantly flip them.

```python
fruits = ["apple", "banana", "cherry"]

# ❌ Wrong — flipped order!
for fruit, index in enumerate(fruits):
    print(f"{index}. {fruit}")
```

Output (WRONG):
```
0. apple
1. banana
2. cherry
```

🧠 Wait, it "works" but `fruit` is actually the **index** (0, 1, 2) and `index` is the **value** ("apple", "banana", "cherry"). The variable names are misleading!

```python
# ✅ Correct — index first, value second
for index, fruit in enumerate(fruits):
    print(f"{index}. {fruit}")
```

✔ **Rule:** `enumerate()` always gives `(index, value)`. Name your variables accordingly.

### 🔸 enumerate with Custom Start Index

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")
```

Output:
```
1. apple
2. banana
3. cherry
```

---

## 🔹 Loop Control Statements

### 🔸 `break` — Exit the Loop Immediately

```python
for i in range(1, 11):
    if i == 5:
        print("Found 5! Stopping.")
        break
    print(i)
```

Output:
```
1
2
3
4
Found 5! Stopping.
```

✔ When `break` is hit, the loop **stops completely**. No more iterations.

### 🔸 `continue` — Skip Current Iteration

```python
for i in range(1, 11):
    if i == 5:
        continue   # skip 5
    print(i)
```

Output:
```
1
2
3
4
6
7
8
9
10
```

✔ When `continue` is hit, the **current iteration is skipped** and the loop moves to the next one.

### 🔸 `pass` — Do Nothing (Placeholder)

```python
for i in range(5):
    if i == 3:
        pass   # TODO: handle this later
    print(i)
```

Output:
```
0
1
2
3
4
```

✔ `pass` does nothing. The loop continues normally. Used as a placeholder.

### 🔸 break vs continue vs pass — Comparison

```python
# break — stops the entire loop
for i in range(5):
    if i == 3:
        break
    print(i)
# Output: 0 1 2

# continue — skips one iteration
for i in range(5):
    if i == 3:
        continue
    print(i)
# Output: 0 1 2 4

# pass — does nothing
for i in range(5):
    if i == 3:
        pass
    print(i)
# Output: 0 1 2 3 4
```

| Statement | What It Does |
|-----------|-------------|
| `break` | Exits the loop completely |
| `continue` | Skips to the next iteration |
| `pass` | Does nothing, loop continues |

---

## 🔹 The `else` Clause with Loops (INTERVIEW FAVORITE 🔥)

Python has a unique feature: `else` with loops. The `else` block runs **only if the loop completes without hitting `break`**.

### 🔸 for-else

```python
for i in range(5):
    print(i)
else:
    print("Loop completed without break")
```

Output:
```
0
1
2
3
4
Loop completed without break
```

### 🔸 for-else with break

```python
for i in range(5):
    if i == 3:
        print("Found 3! Breaking.")
        break
    print(i)
else:
    print("Loop completed without break")
```

Output:
```
0
1
2
Found 3! Breaking.
```

✔ The `else` block did **NOT** run because `break` was triggered.

### 🔸 while-else

```python
count = 0

while count < 3:
    print(count)
    count = count + 1
else:
    print("While loop completed")
```

Output:
```
0
1
2
While loop completed
```

### 🔸 Real-World Use: Search and Report

```python
numbers = [1, 3, 5, 7, 9]
target = 4

for num in numbers:
    if num == target:
        print(f"Found {target}!")
        break
else:
    print(f"{target} not found in the list")
```

Output:
```
4 not found in the list
```

✔ This is cleaner than using a separate `found` flag variable.

---

## 🔹 Nested Loops

A loop inside another loop.

### 🔸 Basic Nested Loop

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(f"i={i}, j={j}")
```

Output:
```
i=1, j=1
i=1, j=2
i=1, j=3
i=2, j=1
i=2, j=2
i=2, j=3
i=3, j=1
i=3, j=2
i=3, j=3
```

🧠 For each iteration of the **outer loop**, the **inner loop runs completely**.

### 🔸 Multiplication Table

```python
for i in range(1, 6):
    for j in range(1, 11):
        print(f"{i} x {j} = {i*j}")
    print("---")
```

### 🔸 Star Pattern — Right Triangle

```python
for i in range(1, 6):
    j = 0
    while j < i:
        print("*", end="")
        j = j + 1
    print()
```

Output:
```
*
**
***
****
*****
```

#### Pythonic shortcut:

```python
for i in range(1, 6):
    print("*" * i)
```

✔ Same output, much cleaner. Understand the manual logic first, then use the shortcut.

### 🔸 break in Nested Loops

`break` only exits the **innermost** loop.

```python
for i in range(3):
    for j in range(3):
        if j == 1:
            break
        print(f"i={i}, j={j}")
```

Output:
```
i=0, j=0
i=1, j=0
i=2, j=0
```

✔ `break` stopped the inner loop at `j=1`, but the outer loop continued.

---

## 🔹 Looping Techniques (Pythonic Ways 🔥)

### 🔸 zip() — Loop Over Multiple Sequences Together

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

# Without zip (manual way)
i = 0
while i < len(names):
    print(f"{names[i]} is {ages[i]} years old")
    i = i + 1

# With zip (Pythonic way ✅)
for name, age in zip(names, ages):
    print(f"{name} is {age} years old")
```

Output:
```
Alice is 25 years old
Bob is 30 years old
Charlie is 35 years old
```

⚠️ `zip()` stops at the **shortest** sequence:

```python
a = [1, 2, 3]
b = [10, 20]

for x, y in zip(a, b):
    print(x, y)
```

Output:
```
1 10
2 20
```

✔ The third element of `a` is ignored because `b` ran out.

### 🔸 reversed() — Loop in Reverse

```python
fruits = ["apple", "banana", "cherry"]

# Without reversed (manual way)
i = len(fruits) - 1
while i >= 0:
    print(fruits[i])
    i = i - 1

# With reversed (Pythonic way ✅)
for fruit in reversed(fruits):
    print(fruit)
```

Output:
```
cherry
banana
apple
```

### 🔸 sorted() — Loop in Sorted Order

```python
numbers = [3, 1, 4, 1, 5, 9]

for num in sorted(numbers):
    print(num)
```

Output:
```
1
1
3
4
5
9
```

#### Reverse sorted:

```python
for num in sorted(numbers, reverse=True):
    print(num)
```

Output:
```
9
5
4
3
1
1
```

---

## 🔹 while vs for — When to Use Which?

| Use `for` When | Use `while` When |
|---------------|-----------------|
| Iterating over a sequence | Don't know how many iterations |
| You know the count | Waiting for a condition |
| Looping through list/string/dict | User input loops |
| Using range() | Game loops |
| Most common choice | Infinite loops with break |

```python
# for — known iterations
for i in range(10):
    print(i)

# while — unknown iterations
password = ""
while password != "secret":
    password = input("Enter password: ")
```

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Forgetting to Update the Counter

```python
# ❌ Infinite loop!
i = 0
while i < 5:
    print(i)
    # forgot: i = i + 1
```

### 🔸 Mistake 2: Off-by-One Error

```python
# ❌ Prints 0-4 (not 1-5)
for i in range(5):
    print(i)

# ✅ Prints 1-5
for i in range(1, 6):
    print(i)
```

### 🔸 Mistake 3: Modifying a List While Looping

```python
numbers = [1, 2, 3, 4, 5]

# ❌ Dangerous — skips elements!
for num in numbers:
    if num % 2 == 0:
        numbers.remove(num)

print(numbers)   # [1, 3, 5]  ← might work, but unreliable!

# ✅ Safe — loop over a copy
for num in numbers[:]:   # [:] creates a copy
    if num % 2 == 0:
        numbers.remove(num)

# ✅ Even better — create a new list
odd_numbers = []
for num in numbers:
    if num % 2 != 0:
        odd_numbers.append(num)
```

### 🔸 Mistake 4: Using range() with Floats

```python
# ❌ range() doesn't support floats
for i in range(0.0, 1.0, 0.1):   # TypeError!
    print(i)

# ✅ Workaround
i = 0.0
while i < 1.0:
    print(round(i, 1))
    i = i + 0.1
```

---

## 🔹 Performance: while vs for (INTERVIEW 🔥)

`for` loops with `range()` are generally **faster** than equivalent `while` loops because:
- `range()` is implemented in C internally
- `while` has to evaluate the condition each time in Python

```python
# Slower
i = 0
while i < 1000000:
    i = i + 1

# Faster
for i in range(1000000):
    pass
```

✔ Prefer `for` loops when possible.

---

## 🔹 Interview Programs 💡

### ✅ 1. Print Numbers 1 to N

#### Using while:

```python
n = 10
i = 1

while i <= n:
    print(i)
    i = i + 1
```

#### Using for:

```python
n = 10

for i in range(1, n + 1):
    print(i)
```

---

### ✅ 2. Sum of Numbers 1 to N

#### Using while:

```python
n = 100
total = 0
i = 1

while i <= n:
    total = total + i
    i = i + 1

print(f"Sum: {total}")   # Sum: 5050
```

#### Using for:

```python
n = 100
total = 0

for i in range(1, n + 1):
    total = total + i

print(f"Sum: {total}")   # Sum: 5050
```

#### Pythonic shortcut:

```python
n = 100
print(f"Sum: {sum(range(1, n + 1))}")   # Sum: 5050
```

✔ `sum()` adds all items in an iterable. Understand the manual logic first.

---

### ✅ 3. Factorial of a Number

#### Using while:

```python
n = 5
factorial = 1
i = 1

while i <= n:
    factorial = factorial * i
    i = i + 1

print(f"{n}! = {factorial}")   # 5! = 120
```

#### Using for:

```python
n = 5
factorial = 1

for i in range(1, n + 1):
    factorial = factorial * i

print(f"{n}! = {factorial}")   # 5! = 120
```

#### Pythonic shortcut:

```python
import math
print(f"5! = {math.factorial(5)}")   # 5! = 120
```

---

### ✅ 4. Reverse a Number

```python
num = 12345
reversed_num = 0

while num > 0:
    digit = num % 10
    reversed_num = reversed_num * 10 + digit
    num = num // 10

print(f"Reversed: {reversed_num}")   # Reversed: 54321
```

🧠 Step by step:
| num | digit (num % 10) | reversed_num |
|:---:|:---:|:---:|
| 12345 | 5 | 5 |
| 1234 | 4 | 54 |
| 123 | 3 | 543 |
| 12 | 2 | 5432 |
| 1 | 1 | 54321 |

#### Pythonic shortcut (using string):

```python
num = 12345
print(int(str(num)[::-1]))   # 54321
```

---

### ✅ 5. Check Prime Number

```python
num = 29
is_prime = True

if num <= 1:
    is_prime = False
else:
    i = 2
    while i * i <= num:
        if num % i == 0:
            is_prime = False
            break
        i = i + 1

if is_prime:
    print(f"{num} is Prime")
else:
    print(f"{num} is NOT Prime")
```

🧠 Why `i * i <= num`?
- If `num` has a factor, at least one factor must be ≤ √num
- So we only need to check up to √num
- `i * i <= num` is the same as `i <= √num` but avoids using `math.sqrt()`

---

### ✅ 6. Print Fibonacci Series

```python
n = 10
a = 0
b = 1
count = 0

while count < n:
    print(a, end=" ")
    temp = a + b
    a = b
    b = temp
    count = count + 1
```

Output:
```
0 1 1 2 3 5 8 13 21 34
```

#### Without temp variable (Python swap):

```python
n = 10
a = 0
b = 1

for i in range(n):
    print(a, end=" ")
    a, b = b, a + b
```

---

### ✅ 7. FizzBuzz (1 to N)

```python
n = 20

for i in range(1, n + 1):
    if i % 3 == 0 and i % 5 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

---

### ✅ 8. Count Digits in a Number

#### Using while:

```python
num = 123456
count = 0

while num > 0:
    num = num // 10
    count = count + 1

print(f"Digits: {count}")   # Digits: 6
```

#### Pythonic shortcut:

```python
num = 123456
print(f"Digits: {len(str(num))}")   # Digits: 6
```

---

### ✅ 9. Print All Prime Numbers Up to N

```python
n = 50

for num in range(2, n + 1):
    is_prime = True
    i = 2
    while i * i <= num:
        if num % i == 0:
            is_prime = False
            break
        i = i + 1
    if is_prime:
        print(num, end=" ")
```

Output:
```
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47
```

---

### ✅ 10. Number Guessing Game

```python
import random

secret = random.randint(1, 100)
attempts = 0

while True:
    guess = int(input("Guess the number (1-100): "))
    attempts = attempts + 1

    if guess < secret:
        print("Too low!")
    elif guess > secret:
        print("Too high!")
    else:
        print(f"Correct! You got it in {attempts} attempts!")
        break
```

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| `while` | Repeats while condition is True |
| `for` | Iterates over a sequence |
| `range()` | Generates number sequence |
| `break` | Exit loop immediately |
| `continue` | Skip current iteration |
| `pass` | Do nothing (placeholder) |
| `else` with loop | Runs if loop completes without break |
| `enumerate()` | Index + value together |
| `zip()` | Loop multiple sequences together |
| `reversed()` | Loop in reverse |
| `sorted()` | Loop in sorted order |
| Nested loops | Loop inside a loop |
| Infinite loop | `while True` with `break` |
| Off-by-one | `range(5)` = 0-4, not 1-5 |
| Performance | `for` with `range()` is faster than `while` |

---

> 🚀 **Next:** Functions in Python →
