# 🔀 Conditional Statements in Python - Complete Guide (Zero to Hero)

> Conditional statements let your program **make decisions** — do different things based on different conditions.

---

## 🔹 What are Conditional Statements?

They allow your program to **choose** which code to run based on whether a condition is `True` or `False`.

### 🧠 Real-World Analogy

> 👉 Think of it like a **traffic signal**:
> - If the light is **green** → Go
> - If the light is **yellow** → Slow down
> - If the light is **red** → Stop
>
> Your program does the same — checks a condition and acts accordingly.

---

## 🔹 The `if` Statement

The simplest conditional. Runs the code block **only if** the condition is `True`.

### Syntax:

```python
if condition:
    # code to run if condition is True
```

### Example:

```python
age = 20

if age >= 18:
    print("You are eligible to vote")
```

Output:
```
You are eligible to vote
```

### 🔸 What Happens Step by Step?

1. Python evaluates `age >= 18` → `20 >= 18` → `True`
2. Since the condition is `True`, the indented code runs
3. If the condition were `False`, the indented code would be **skipped entirely**

### 🔸 When Condition is False — Nothing Happens

```python
age = 15

if age >= 18:
    print("You are eligible to vote")

print("Program continues...")
```

Output:
```
Program continues...
```

✔ The `if` block was skipped because `15 >= 18` is `False`.

---

## 🔹 Indentation is CRITICAL ⚠️

Python uses **indentation** (4 spaces) to define what's inside the `if` block.

```python
age = 20

# ✅ Correct — indented code is inside the if block
if age >= 18:
    print("You can vote")
    print("You are an adult")

# ❌ Wrong — no indentation
if age >= 18:
print("You can vote")   # IndentationError!
```

### 🔸 What's Inside vs Outside the if Block

```python
age = 15

if age >= 18:
    print("Inside if — only runs if True")
    print("Also inside if")

print("Outside if — always runs")
```

Output:
```
Outside if — always runs
```

✔ Only the **indented lines** are part of the `if` block. The non-indented line runs **regardless**.

---

## 🔹 The `if-else` Statement

Provides an **alternative** when the condition is `False`.

### Syntax:

```python
if condition:
    # runs if condition is True
else:
    # runs if condition is False
```

### Example:

```python
age = 15

if age >= 18:
    print("You can vote")
else:
    print("You cannot vote yet")
```

Output:
```
You cannot vote yet
```

### 🔸 Only ONE Block Runs

```python
num = 10

if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

Output:
```
Even
```

✔ Either the `if` block runs OR the `else` block runs — **never both**.

---

## 🔹 The `if-elif-else` Statement

When you have **multiple conditions** to check.

### Syntax:

```python
if condition1:
    # runs if condition1 is True
elif condition2:
    # runs if condition2 is True
elif condition3:
    # runs if condition3 is True
else:
    # runs if ALL conditions are False
```

### Example:

```python
marks = 75

if marks >= 90:
    print("Grade: A")
elif marks >= 80:
    print("Grade: B")
elif marks >= 70:
    print("Grade: C")
elif marks >= 60:
    print("Grade: D")
else:
    print("Grade: F")
```

Output:
```
Grade: C
```

### 🔸 How Python Evaluates This — Step by Step

1. `marks >= 90` → `75 >= 90` → `False` → skip
2. `marks >= 80` → `75 >= 80` → `False` → skip
3. `marks >= 70` → `75 >= 70` → `True` → **runs this block**
4. Remaining `elif` and `else` are **skipped entirely**

✔ Python checks conditions **top to bottom** and runs the **first True** block only.

### 🔸 You Can Have Multiple elif

```python
day = "Wednesday"

if day == "Monday":
    print("Start of work week")
elif day == "Wednesday":
    print("Midweek")
elif day == "Friday":
    print("Almost weekend!")
elif day == "Saturday" or day == "Sunday":
    print("Weekend!")
else:
    print("Regular day")
```

### 🔸 else is Optional

```python
temperature = 30

if temperature > 35:
    print("Very hot")
elif temperature > 25:
    print("Warm")
```

✔ No `else` needed if you don't want a default action.

---

## 🔹 Nested if Statements

An `if` inside another `if`.

```python
age = 25
has_id = True

if age >= 18:
    if has_id:
        print("You can enter the club")
    else:
        print("You need an ID")
else:
    print("You are underage")
```

Output:
```
You can enter the club
```

### 🔸 Multiple Levels of Nesting

```python
num = 15

if num > 0:
    print("Positive")
    if num % 2 == 0:
        print("Even")
    else:
        print("Odd")
    if num > 10:
        print("Greater than 10")
else:
    print("Not positive")
```

Output:
```
Positive
Odd
Greater than 10
```

⚠️ **Avoid deep nesting** (more than 2-3 levels). It makes code hard to read. Use logical operators instead.

---

## 🔹 Logical Operators in Conditions (VERY IMPORTANT 🔥)

### 🔸 `and` — Both Conditions Must Be True

```python
age = 25
has_id = True

if age >= 18 and has_id:
    print("You can enter")
```

| Condition 1 | Condition 2 | Result |
|:---:|:---:|:---:|
| True | True | **True** |
| True | False | False |
| False | True | False |
| False | False | False |

### 🔸 `or` — At Least One Must Be True

```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("It's the weekend!")
```

| Condition 1 | Condition 2 | Result |
|:---:|:---:|:---:|
| True | True | **True** |
| True | False | **True** |
| False | True | **True** |
| False | False | False |

### 🔸 `not` — Reverses the Result

```python
is_raining = False

if not is_raining:
    print("No need for umbrella")
```

| Condition | Result |
|:---:|:---:|
| True | **False** |
| False | **True** |

### 🔸 Combining Logical Operators

```python
age = 25
income = 50000
has_good_credit = True

if (age >= 21 and income >= 30000) or has_good_credit:
    print("Loan approved")
```

✔ Use **parentheses** to make complex conditions clear.

### 🔸 Operator Precedence

```
not  →  and  →  or
```

`not` is evaluated first, then `and`, then `or`.

```python
# Without parentheses
print(True or False and False)    # True  (and is evaluated first)

# Same as:
print(True or (False and False))  # True

# With parentheses to change order
print((True or False) and False)  # False
```

---

## 🔹 Comparison Operators (Recap)

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater than or equal | `5 >= 5` | `True` |
| `<=` | Less than or equal | `5 <= 3` | `False` |

### 🔸 Chained Comparisons (Python Special ✨)

```python
age = 25

# Normal way
if age >= 18 and age <= 65:
    print("Working age")

# Python way — chained comparison
if 18 <= age <= 65:
    print("Working age")
```

✔ Python allows **chaining** comparisons. Much cleaner!

```python
x = 5
print(1 < x < 10)     # True
print(1 < x < 3)      # False
print(10 > x > 1)     # True
```

---

## 🔹 Float Comparison Trap ⚠️ (VERY IMPORTANT 🔥)

Remember from the data types chapter: `0.1 + 0.2` is NOT exactly `0.3` due to binary precision.

```python
# ❌ This will NOT work as expected!
if 0.1 + 0.2 == 0.3:
    print("Equal")
else:
    print("Not equal")
```

Output:
```
Not equal
```

🧠 Because `0.1 + 0.2` = `0.30000000000000004`, not `0.3`.

### 🔸 Solution: Use `math.isclose()`

```python
import math

if math.isclose(0.1 + 0.2, 0.3):
    print("Equal")
else:
    print("Not equal")
```

Output:
```
Equal
```

✔ `math.isclose()` checks if two floats are **approximately equal** (within a tiny tolerance).

### 🔸 Custom Tolerance

```python
import math

a = 1.0000001
b = 1.0000002

print(math.isclose(a, b))                          # True  (default tolerance)
print(math.isclose(a, b, rel_tol=1e-10))           # False (stricter tolerance)
```

### 🔸 Manual Approach (Without math module)

```python
a = 0.1 + 0.2
b = 0.3

if abs(a - b) < 0.0001:
    print("Approximately equal")
```

✔ `abs(a - b)` gives the **absolute difference**. If it's tiny enough, they're "equal".

---

## 🔹 Membership Operators in Conditions

### 🔸 `in` — Check if Value Exists

```python
fruits = ["apple", "banana", "cherry"]

if "banana" in fruits:
    print("Yes, banana is in the list")
```

### 🔸 `not in` — Check if Value Does NOT Exist

```python
text = "Python Programming"

if "Java" not in text:
    print("Java is not mentioned")
```

---

## 🔹 Identity Operators in Conditions

### 🔸 `is` — Same Object in Memory

```python
x = None

if x is None:
    print("x has no value")
```

### 🔸 `is not` — Different Objects

```python
x = 10

if x is not None:
    print("x has a value")
```

✔ Always use `is None` / `is not None` instead of `== None` / `!= None`.

---

## 🔹 Multi-Condition Checks — all() and any() (IMPORTANT 🔥)

When you have **many conditions** to check, chaining `and` / `or` gets messy. Python provides `all()` and `any()`.

### 🔸 all() — ALL Conditions Must Be True (like `and`)

```python
age = 25
has_id = True
has_ticket = True

# ❌ Long chain of and
if age >= 18 and has_id and has_ticket:
    print("Entry allowed")

# ✅ Cleaner with all()
conditions = [age >= 18, has_id, has_ticket]

if all(conditions):
    print("Entry allowed")
```

🧠 `all()` returns `True` only if **every item** in the list is `True`.

```python
print(all([True, True, True]))    # True
print(all([True, False, True]))   # False
print(all([]))                    # True  (empty = vacuously true)
```

### 🔸 any() — At Least ONE Must Be True (like `or`)

```python
has_cash = False
has_card = False
has_upi = True

# ❌ Long chain of or
if has_cash or has_card or has_upi:
    print("Payment possible")

# ✅ Cleaner with any()
payment_methods = [has_cash, has_card, has_upi]

if any(payment_methods):
    print("Payment possible")
```

🧠 `any()` returns `True` if **at least one item** is `True`.

```python
print(any([False, False, True]))   # True
print(any([False, False, False]))  # False
print(any([]))                     # False  (empty = nothing is true)
```

### 🔸 Real-World Example: Form Validation

```python
username = "giridhar"
email = "giri@email.com"
password = "secret123"

# Check all fields are filled
fields = [username, email, password]

if all(fields):
    print("All fields filled — form valid")
else:
    print("Some fields are empty!")
```

✔ This works because empty strings `""` are **falsy** — `all()` will catch them.

### 🔸 Summary

| Function | Meaning | Like |
|----------|---------|------|
| `all(list)` | Every item is True | `and` |
| `any(list)` | At least one is True | `or` |

---

## 🔹 Truthy and Falsy in Conditions (INTERVIEW FAVORITE 🔥)

You don't always need explicit comparisons. Python evaluates **truthiness** directly.

### 🔸 Instead of Comparing to Empty/Zero

```python
name = "Giridhar"

# ❌ Verbose way
if name != "":
    print("Name is not empty")

# ✅ Pythonic way
if name:
    print("Name is not empty")
```

```python
numbers = []

# ❌ Verbose
if len(numbers) == 0:
    print("List is empty")

# ✅ Pythonic
if not numbers:
    print("List is empty")
```

### 🔸 Common Patterns

```python
# Check if list has items
items = [1, 2, 3]
if items:
    print("List has items")

# Check if string is not empty
text = "Hello"
if text:
    print("String is not empty")

# Check if variable has a value
result = None
if result is None:
    print("No result yet")
```

---

## 🔹 Conditional Expression (Ternary Operator)

A **one-line** if-else.

### Syntax:

```python
value_if_true if condition else value_if_false
```

### Example:

```python
age = 20

# Normal if-else
if age >= 18:
    status = "Adult"
else:
    status = "Minor"

# Same thing in one line (ternary)
status = "Adult" if age >= 18 else "Minor"
print(status)   # Adult
```

### More Examples:

```python
num = 7
result = "Even" if num % 2 == 0 else "Odd"
print(result)   # Odd

x = 10
y = 20
bigger = x if x > y else y
print(bigger)   # 20
```

### 🔸 Nested Ternary (Use Carefully!)

```python
marks = 75
grade = "A" if marks >= 90 else "B" if marks >= 80 else "C" if marks >= 70 else "F"
print(grade)   # C
```

⚠️ Nested ternary is **hard to read**. Use regular `if-elif-else` for complex conditions.

---

## 🔹 The `pass` Statement

A **placeholder** that does nothing. Used when a block is required but you don't want to write code yet.

```python
age = 20

if age >= 18:
    pass   # TODO: implement later
else:
    print("Minor")
```

✔ Without `pass`, an empty `if` block would cause a `SyntaxError`.

```python
# ❌ Error
if True:
    # nothing here → SyntaxError

# ✅ Works
if True:
    pass
```

---

## 🔹 match-case Statement (Python 3.10+)

Python's version of **switch-case** from other languages.

### Syntax:

```python
match variable:
    case value1:
        # code
    case value2:
        # code
    case _:
        # default (like else)
```

### Example:

```python
day = "Monday"

match day:
    case "Monday":
        print("Start of the week")
    case "Friday":
        print("Almost weekend!")
    case "Saturday" | "Sunday":
        print("Weekend!")
    case _:
        print("Regular day")
```

Output:
```
Start of the week
```

### 🔸 match-case with Numbers

```python
status_code = 404

match status_code:
    case 200:
        print("OK")
    case 404:
        print("Not Found")
    case 500:
        print("Server Error")
    case _:
        print("Unknown status")
```

### 🔸 match-case with Multiple Values (Using `|`)

```python
command = "quit"

match command:
    case "quit" | "exit" | "q":
        print("Goodbye!")
    case "help" | "h":
        print("Showing help...")
    case _:
        print(f"Unknown command: {command}")
```

⚠️ `match-case` is only available in **Python 3.10 and above**.

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Using `=` Instead of `==`

```python
x = 10

# ❌ Wrong — this is assignment, not comparison
if x = 10:    # SyntaxError!
    print("Ten")

# ✅ Correct — double equals for comparison
if x == 10:
    print("Ten")
```

### 🔸 Mistake 2: Forgetting the Colon `:`

```python
# ❌ Wrong
if x == 10
    print("Ten")   # SyntaxError: expected ':'

# ✅ Correct
if x == 10:
    print("Ten")
```

### 🔸 Mistake 3: Wrong Indentation

```python
# ❌ Wrong — inconsistent indentation
if True:
    print("Hello")
      print("World")   # IndentationError

# ✅ Correct — same indentation
if True:
    print("Hello")
    print("World")
```

### 🔸 Mistake 4: Comparing Different Types

```python
age = input("Enter age: ")   # returns string "25"

# ❌ Wrong — comparing string with int
if age > 18:    # TypeError!
    print("Adult")

# ✅ Correct — convert first
if int(age) > 18:
    print("Adult")
```

### 🔸 Mistake 5: Using `or` Wrong

```python
day = "Monday"

# ❌ Wrong — this doesn't do what you think
if day == "Saturday" or "Sunday":
    print("Weekend")   # This ALWAYS prints!

# 🧠 Why? Python reads it as:
# if (day == "Saturday") or ("Sunday")
# "Sunday" is a non-empty string → always True!

# ✅ Correct
if day == "Saturday" or day == "Sunday":
    print("Weekend")

# ✅ Even better
if day in ("Saturday", "Sunday"):
    print("Weekend")
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Check Even or Odd

```python
num = int(input("Enter a number: "))

if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

---

### ✅ 2. Find the Largest of Three Numbers

#### Understanding the logic (manual way):

```python
a = 10
b = 25
c = 15

if a >= b and a >= c:
    print(f"Largest: {a}")
elif b >= a and b >= c:
    print(f"Largest: {b}")
else:
    print(f"Largest: {c}")
```

#### Pythonic shortcut — using max():

```python
a = 10
b = 25
c = 15

print(f"Largest: {max(a, b, c)}")   # Largest: 25
```

✔ `max()` is a built-in function that returns the **largest** value. Similarly, `min()` returns the smallest.

```python
print(max(10, 25, 15))   # 25
print(min(10, 25, 15))   # 10
```

🧠 **Rule:** Always understand the manual logic first, then use the Pythonic shortcut in real code.

---

### ✅ 3. Check Positive, Negative, or Zero

```python
num = int(input("Enter a number: "))

if num > 0:
    print("Positive")
elif num < 0:
    print("Negative")
else:
    print("Zero")
```

---

### ✅ 4. Check Leap Year

```python
year = int(input("Enter year: "))

if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print(f"{year} is a Leap Year")
else:
    print(f"{year} is NOT a Leap Year")
```

🧠 Leap year rules:
- Divisible by 4 → leap year
- BUT divisible by 100 → NOT a leap year
- BUT divisible by 400 → IS a leap year

---

### ✅ 5. Simple Calculator

```python
num1 = float(input("Enter first number: "))
operator = input("Enter operator (+, -, *, /): ")
num2 = float(input("Enter second number: "))

if operator == "+":
    print(f"Result: {num1 + num2}")
elif operator == "-":
    print(f"Result: {num1 - num2}")
elif operator == "*":
    print(f"Result: {num1 * num2}")
elif operator == "/":
    if num2 != 0:
        print(f"Result: {num1 / num2}")
    else:
        print("Error: Cannot divide by zero!")
else:
    print("Invalid operator")
```

---

### ✅ 6. Check Vowel or Consonant

```python
char = input("Enter a character: ").lower()

if char in "aeiou":
    print(f"'{char}' is a Vowel")
elif char.isalpha():
    print(f"'{char}' is a Consonant")
else:
    print("Not a letter")
```

---

### ✅ 7. Check if a Number is in a Range

```python
num = int(input("Enter a number: "))

if 1 <= num <= 100:
    print("In range (1-100)")
else:
    print("Out of range")
```

---

### ✅ 8. FizzBuzz (Classic Interview Question 🔥)

```python
num = int(input("Enter a number: "))

if num % 3 == 0 and num % 5 == 0:
    print("FizzBuzz")
elif num % 3 == 0:
    print("Fizz")
elif num % 5 == 0:
    print("Buzz")
else:
    print(num)
```

⚠️ **Order matters!** Check `num % 3 == 0 and num % 5 == 0` **first**, otherwise it will match the individual checks before reaching the combined one.

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| `if` | Runs code if condition is True |
| `else` | Runs code if condition is False |
| `elif` | Check additional conditions |
| Indentation | 4 spaces define the code block |
| `and` | Both conditions must be True |
| `or` | At least one must be True |
| `not` | Reverses True/False |
| Chained comparison | `1 < x < 10` |
| Ternary | `"Yes" if True else "No"` |
| `pass` | Placeholder, does nothing |
| `match-case` | Switch-case (Python 3.10+) |
| Truthy/Falsy | Empty values are False |
| `in` / `not in` | Membership check |
| `is` / `is not` | Identity check |

---

> 🚀 **Next:** Loops in Python →
