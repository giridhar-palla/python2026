# 🔤 Strings in Python - Complete Guide (Zero to Hero)

> A string is a **sequence of characters** (letters, numbers, symbols) enclosed inside quotes.

---

## 🔹 What is a String in Python?

A string is a **sequence of characters** enclosed inside:

- Single quotes `' '`
- Double quotes `" "`
- Triple quotes `''' '''` or `""" """`

### 🧠 Real-World Analogy

> 👉 A string is like a **sentence written on paper**. Each letter sits in a specific position, and you can read it from left to right.

---

## 🔹 Creating Strings

```python
# Using single quotes
name = 'Python'

# Using double quotes
language = "Programming"

# Using triple quotes (for multi-line strings)
sentence = """Python is
easy to learn"""

# Using triple single quotes
paragraph = '''This is
also a multi-line
string'''
```

✔ All four are valid strings.

### 🔸 When to Use Which?

| Quote Type | When to Use |
|-----------|-------------|
| `' '` Single | Simple strings without apostrophes |
| `" "` Double | Strings with apostrophes like `"It's Python"` |
| `''' '''` or `""" """` Triple | Multi-line strings or docstrings |

### 🔸 Quotes Inside Strings

```python
# Apostrophe inside double quotes
text1 = "It's a beautiful day"
print(text1)   # It's a beautiful day

# Double quote inside single quotes
text2 = 'He said "Hello"'
print(text2)   # He said "Hello"

# Using escape character
text3 = 'It\'s a beautiful day'
print(text3)   # It's a beautiful day
```

---

## 🔹 Checking the Type

```python
name = "Python"
print(type(name))
```

Output:
```
<class 'str'>
```

✔ `str` is the data type for strings in Python.

---

## 🔹 Empty String

```python
empty = ""
print(empty)        # (nothing printed)
print(len(empty))   # 0
print(type(empty))  # <class 'str'>
```

✔ An empty string is still a valid string, it just has **zero characters**.

⚠️ In boolean context:
```python
print(bool(""))     # False  (empty string is Falsy)
print(bool("Hi"))   # True   (non-empty string is Truthy)
```

---

## 🔹 String with Numbers

```python
num_str = "12345"
print(type(num_str))   # <class 'str'>
```

⚠️ **Important:** Even though it looks like a number, it's a **string** because it's inside quotes.

```python
print("10" + "20")   # 1020  (concatenation, NOT addition)
print(10 + 20)       # 30    (actual addition)
```

---

## 🔹 Escape Characters (IMPORTANT 🔥)

Escape characters start with `\` (backslash).

| Escape | Meaning | Example |
|--------|---------|---------|
| `\n` | New line | `"Hello\nWorld"` |
| `\t` | Tab space | `"Hello\tWorld"` |
| `\\` | Backslash | `"C:\\Users"` |
| `\'` | Single quote | `'It\'s Python'` |
| `\"` | Double quote | `"He said \"Hi\""` |
| `\0` | Null character | `"Hello\0World"` |

### Examples:

```python
# New line
print("Hello\nWorld")
```
Output:
```
Hello
World
```

```python
# Tab
print("Name\tAge")
print("Ram\t25")
```
Output:
```
Name    Age
Ram     25
```

```python
# Backslash
print("C:\\Users\\Desktop")
```
Output:
```
C:\Users\Desktop
```

### 🔸 Raw Strings (Ignore Escape Characters)

```python
# Normal string
print("C:\new\folder")    # \n creates new line ❌

# Raw string (prefix with r)
print(r"C:\new\folder")   # C:\new\folder ✅
```

✔ Raw strings treat `\` as a normal character. Very useful for **file paths** and **regex patterns**.

---

## 🔹 Accessing Characters (Indexing)

Each character in a string has a **position (index)** starting from **0**.

```python
text = "Python"
```

| Index | 0 | 1 | 2 | 3 | 4 | 5 |
|-------|---|---|---|---|---|---|
| Char  | P | y | t | h | o | n |

### 🔸 Positive Indexing (Left to Right → starts from 0)

```python
text = "Python"

print(text[0])   # P
print(text[1])   # y
print(text[2])   # t
print(text[3])   # h
print(text[4])   # o
print(text[5])   # n
```

### 🔸 Negative Indexing (Right to Left → starts from -1)

| Index | -6 | -5 | -4 | -3 | -2 | -1 |
|-------|----|----|----|----|----|----|
| Char  | P  | y  | t  | h  | o  | n  |

```python
text = "Python"

print(text[-1])   # n  (last character)
print(text[-2])   # o
print(text[-3])   # h
print(text[-6])   # P  (first character)
```

### 🔸 Index Out of Range ⚠️

```python
text = "Python"
print(text[10])   # ❌ IndexError: string index out of range
```

✔ Always make sure the index is within the string length.

---

## 🔹 String Slicing (Substrings)

Slicing lets you extract a **part of the string**.

### Syntax:
```
string[start : end]
```

- `start` → where to begin (included ✅)
- `end` → where to stop (excluded ❌)

```python
text = "Python Programming"

print(text[0:6])     # Python
print(text[7:18])    # Programming
print(text[:6])      # Python       (start defaults to 0)
print(text[7:])      # Programming  (end defaults to last)
print(text[:])       # Python Programming  (full copy)
```

### 🔸 Slicing with Step

```
string[start : end : step]
```

```python
text = "Python Programming"

print(text[0:6:1])    # Python      (step 1 = normal)
print(text[0:6:2])    # Pto         (every 2nd character)
print(text[::2])      # Pto rgamn   (every 2nd from full string)
```

### 🔸 Reverse a String Using Slicing

```python
text = "Python"
print(text[::-1])   # nohtyP
```

🧠 How it works:
- `start` = not given (defaults to end)
- `end` = not given (defaults to beginning)
- `step` = -1 (go backwards)

### 🔸 Negative Index Slicing

```python
text = "Python Programming"

print(text[-11:])      # Programming
print(text[-11:-4])    # Program
print(text[:-12])      # Python
```

---

## 🔹 String Length

```python
text = "Python"
print(len(text))   # 6
```

✔ `len()` counts **all characters** including spaces and special characters.

```python
text = "Hello World"
print(len(text))   # 11  (space is also counted)

text2 = "Hi\n"
print(len(text2))  # 3   (\n counts as 1 character)
```

---

## 🔹 String Immutability (VERY IMPORTANT 🔥)

> 👉 Strings **cannot be changed** after creation. This is called **immutability**.

```python
text = "Python"
text[0] = "J"   # ❌ TypeError: 'str' object does not support item assignment
```

### ✔ Instead, Create a New String:

```python
text = "Python"
new_text = "J" + text[1:]
print(new_text)   # Jython
print(text)       # Python  (original unchanged)
```

### 🧠 Why Immutable?

- **Memory efficiency** — Python can reuse same string objects
- **Thread safety** — safe to use in multi-threaded programs
- **Hashable** — strings can be used as dictionary keys

### 🔸 Proof of Immutability with id()

```python
text = "Hello"
print(id(text))   # some memory address, e.g., 140234567890

text = text + " World"
print(id(text))   # different memory address!
```

✔ A **new string object** is created, the old one is not modified.

---

## 🔹 String Concatenation (Joining Strings)

### 🔸 Using `+` Operator

```python
a = "Hello"
b = "World"

result = a + " " + b
print(result)   # Hello World
```

### 🔸 Concatenating Different Types ⚠️

```python
name = "Python"
version = 3

# ❌ This will give error
# print(name + version)   # TypeError

# ✅ Convert to string first
print(name + " " + str(version))   # Python 3
```

### 🔸 Concatenation with `+=`

```python
text = "Hello"
text += " World"
print(text)   # Hello World
```

⚠️ Remember: This creates a **new string** (because strings are immutable).

---

## 🔹 String Repetition

```python
word = "Hi "
print(word * 3)   # Hi Hi Hi

line = "-" * 20
print(line)   # --------------------
```

✔ Very useful for creating separators or patterns.

---

## 🔹 Membership Operators (in / not in)

```python
text = "Python Programming"

print("Python" in text)       # True
print("Java" in text)         # False
print("Java" not in text)     # True
print("python" in text)       # False  (case-sensitive!)
```

🧠 Real-life analogy:
> 👉 Like using **Ctrl + F** to search for a word in a document.

---

## 🔹 Iterating (Looping) Through Strings

### 🔸 Basic Way — Using while loop

```python
text = "Python"
i = 0

while i < len(text):
    print(text[i])
    i = i + 1
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

### 🔸 Better Way — Using for loop

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

### 🔸 Loop with Index — Using range()

```python
text = "Python"

for i in range(len(text)):
    print(f"Index {i} = {text[i]}")
```

Output:
```
Index 0 = P
Index 1 = y
Index 2 = t
Index 3 = h
Index 4 = o
Index 5 = n
```

### 🔸 Loop with enumerate() (Index + Value Together)

```python
text = "Python"

for index, char in enumerate(text):
    print(f"Index {index} = {char}")
```

Output:
```
Index 0 = P
Index 1 = y
Index 2 = t
Index 3 = h
Index 4 = o
Index 5 = n
```

✔ `enumerate()` gives both **index** and **character** at the same time.

---

## 🔹 String Comparison

### 🔸 Using == and !=

```python
a = "Python"
b = "python"

print(a == b)   # False  (case-sensitive)
print(a != b)   # True
print(a == "Python")   # True
```

### 🔸 Using >, <, >=, <= (Lexicographic / Dictionary Order)

Python compares strings based on **ASCII/Unicode values**.

```python
print("apple" < "banana")    # True   (a comes before b)
print("abc" < "abd")         # True   (c comes before d)
print("Python" < "python")   # True   (uppercase < lowercase in ASCII)
```

### 🔸 ASCII Values

```python
print(ord("A"))   # 65
print(ord("a"))   # 97
print(ord("0"))   # 48

print(chr(65))    # A
print(chr(97))    # a
```

✔ `ord()` → character to ASCII number
✔ `chr()` → ASCII number to character

---

## 🔹 String Methods (Most Important 🔥)

Python has many **built-in methods** for strings. Methods are called using **dot notation**.

```python
text = "hello"
result = text.upper()   # calling the upper() method
print(result)           # HELLO
```

⚠️ **Remember:** String methods **do NOT change** the original string (because strings are immutable). They always **return a new string**.

---

### 🔸 Case Conversion Methods

#### upper() — Convert to UPPERCASE

```python
text = "PyThOn"
print(text.upper())   # PYTHON
print(text)           # PyThOn  (original unchanged)
```

#### lower() — Convert to lowercase

```python
text = "PyThOn"
print(text.lower())   # python
```

#### title() — First Letter of Each Word Capitalized

```python
text = "python is easy"
print(text.title())   # Python Is Easy
```

#### capitalize() — Only First Letter of String Capitalized

```python
text = "python is easy"
print(text.capitalize())   # Python is easy
```

⚠️ **Difference between title() and capitalize():**

```python
text = "hello world"
print(text.title())       # Hello World    (every word)
print(text.capitalize())  # Hello world    (only first word)
```

#### swapcase() — Swap Upper to Lower and Vice Versa

```python
text = "PyThOn"
print(text.swapcase())   # pYtHoN
```

#### casefold() — Aggressive Lowercase (for comparison)

```python
text = "PYTHON"
print(text.casefold())   # python
```

✔ `casefold()` is more aggressive than `lower()`. It handles special characters from other languages better.

```python
# German example
text = "straße"           # ß is a German character
print(text.lower())       # straße
print(text.casefold())    # strasse   (converts ß to ss)
```

---

### 🔸 Whitespace / Space Methods

#### strip() — Remove Spaces from Both Sides

```python
text = "  Python  "
print(text.strip())   # "Python"
```

#### lstrip() — Remove Spaces from Left Side Only

```python
text = "  Python  "
print(text.lstrip())   # "Python  "
```

#### rstrip() — Remove Spaces from Right Side Only

```python
text = "  Python  "
print(text.rstrip())   # "  Python"
```

#### strip() with Characters

```python
text = "***Python***"
print(text.strip("*"))   # "Python"

text2 = "xxxyyyPythonyyyxxx"
print(text2.strip("xy"))   # "Python"
```

✔ You can strip **any characters**, not just spaces.

#### removeprefix() and removesuffix() (Python 3.9+)

When you want to remove an **exact prefix or suffix** (not individual characters like `strip()`):

```python
filename = "test_file.txt"
print(filename.removesuffix(".txt"))    # test_file
print(filename.removeprefix("test_"))   # file.txt
```

⚠️ **strip() vs removesuffix() — Important Difference:**

```python
text = "mississippi"

# strip removes ANY of the given characters from both ends
print(text.strip("mips"))       # (empty string — stripped all matching chars!)

# removesuffix removes the EXACT suffix only
print(text.removesuffix("ppi"))  # mississi
```

✔ Use `removeprefix()` / `removesuffix()` when you want **exact matching**. Use `strip()` when you want to remove **any of the given characters**.

---

### 🔸 Split and Join (VERY IMPORTANT FOR INTERVIEWS 🔥)

#### split() — Break String into a List

```python
text = "Python is very easy"

words = text.split(" ")
print(words)   # ['Python', 'is', 'very', 'easy']
```

🧠 How it works:
- `split(" ")` → splits wherever there is a **space**
- Returns a **list** of substrings

#### split() with Different Separators

```python
# Split by comma
data = "apple,banana,cherry"
fruits = data.split(",")
print(fruits)   # ['apple', 'banana', 'cherry']

# Split by dash
date = "2025-04-18"
parts = date.split("-")
print(parts)   # ['2025', '04', '18']

# Split by newline
text = "line1\nline2\nline3"
lines = text.split("\n")
print(lines)   # ['line1', 'line2', 'line3']
```

#### split() with No Argument

```python
text = "  Python   is   easy  "
words = text.split()
print(words)   # ['Python', 'is', 'easy']
```

✔ Without argument, `split()` splits by **any whitespace** and removes extra spaces automatically.

#### split() with maxsplit (Limit Splits)

```python
text = "one-two-three-four"

print(text.split("-", 1))    # ['one', 'two-three-four']
print(text.split("-", 2))    # ['one', 'two', 'three-four']
```

✔ `maxsplit` controls **how many splits** to make.

#### rsplit() — Split from Right Side

```python
text = "one-two-three-four"

print(text.rsplit("-", 1))   # ['one-two-three', 'four']
print(text.split("-", 1))    # ['one', 'two-three-four']
```

✔ `rsplit()` starts splitting from the **right end**.

#### splitlines() — Split by Line Breaks

```python
text = "Hello\nWorld\nPython"
lines = text.splitlines()
print(lines)   # ['Hello', 'World', 'Python']
```

---

#### join() — Combine a List into a String

```python
words = ['Python', 'is', 'easy']

sentence = " ".join(words)
print(sentence)   # Python is easy
```

🧠 How it works:
- `" ".join(words)` → joins all items in the list with a **space** between them

#### join() with Different Separators

```python
words = ['Python', 'is', 'easy']

print("-".join(words))     # Python-is-easy
print(", ".join(words))    # Python, is, easy
print("".join(words))      # Pythoniseasy   (no separator)
print("\n".join(words))
```

Output of last one:
```
Python
is
easy
```

#### join() with Characters of a String

```python
text = "Python"
result = "-".join(text)
print(result)   # P-y-t-h-o-n
```

✔ `join()` works on **any iterable** (list, tuple, string).

---

### 🔸 Finding and Replacing in Strings (VERY IMPORTANT 🔥)

Let's use this string for all examples:

```python
message = "I love Python programming with Python"
```

🧠 Think of this as a sentence written on paper. Now we want to:
- Check if a word exists
- Find where it occurs
- Count how many times
- Replace it with another word

---

#### 1️⃣ Check if Something Exists → `in`

```python
print("Python" in message)
```

How it works:
- `"Python" in message` → asks: "Is the word Python present anywhere in the string?"

Output:
```
True
```

✔ Returns a **Boolean** (True / False)

🧠 Real-life analogy:
> 👉 Searching for a word using **Ctrl + F**

---

#### 2️⃣ Check Starting of String → `startswith()`

```python
print(message.startswith("I"))       # True
print(message.startswith("i"))       # False  (case-sensitive!)
print(message.startswith("I love"))  # True
```

✔ Checks whether the string **begins with** the given text.

---

#### 3️⃣ Check Ending of String → `endswith()`

```python
print(message.endswith("Python"))    # True
print(message.endswith("python"))    # False  (case-sensitive!)
```

📌 Common use cases:
- File validation (`.pdf`, `.csv`)
- URL checks

```python
filename = "report.pdf"
if filename.endswith(".pdf"):
    print("It's a PDF file")
```

---

#### 4️⃣ Find Position of a Substring → `find()`

```python
print(message.find("Python"))   # 7
```

What `find()` does:
- Returns the **index (position)** of the **first occurrence**

```
"I love Python programming with Python"
        ↑
        index 7
```

❗ If NOT found:
```python
print(message.find("Java"))   # -1
```

✔ `-1` means **not found**

#### rfind() — Find from Right Side

```python
print(message.rfind("Python"))   # 33
```

✔ Returns the index of the **last occurrence**.

---

#### 5️⃣ index() vs find() (INTERVIEW FAVORITE 🔥)

```python
print(message.find("Java"))    # -1   (returns -1 if not found)
print(message.index("Java"))   # ❌ ValueError: substring not found
```

| Method | Not Found Behavior |
|--------|-------------------|
| `find()` | Returns `-1` |
| `index()` | Raises `ValueError` ❌ |

✔ **Prefer `find()`** when you're unsure if the word exists.

Similarly:
- `rfind()` → safe (returns -1)
- `rindex()` → raises error

---

#### 6️⃣ Count Occurrences → `count()`

```python
print(message.count("Python"))   # 2
print(message.count("o"))        # 3
print(message.count("Java"))     # 0
```

✔ Counts **how many times** the substring appears.

Useful for:
- Frequency analysis
- Text processing
- Interview questions

---

#### 7️⃣ Replace Text → `replace()` (VERY IMPORTANT 🔥)

```python
new_message = message.replace("Python", "JavaScript")
print(new_message)
```

Output:
```
I love JavaScript programming with JavaScript
```

❗ **Important Concept: Strings Are Immutable**

Original string is **NOT changed**:
```python
print(message)
```
Output:
```
I love Python programming with Python
```

✔ `replace()` creates a **new string**.

#### Replace Only First Occurrence

```python
result = message.replace("Python", "JavaScript", 1)
print(result)
```

Output:
```
I love JavaScript programming with Python
```

✔ The third argument `1` means **replace only the first match**.

---

### 🔸 Finding & Replacing — Summary Table 📌

| Method | Purpose | Returns |
|--------|---------|---------|
| `in` | Check existence | Boolean |
| `startswith()` | Check beginning | Boolean |
| `endswith()` | Check ending | Boolean |
| `find()` | First position | Index / -1 |
| `rfind()` | Last position | Index / -1 |
| `index()` | First position | Index / Error ❌ |
| `count()` | Total occurrences | Integer |
| `replace()` | Replace text | New string |

---

### 🔸 Padding and Alignment Methods

#### center() — Center the String

```python
text = "Python"
print(text.center(20))        # "       Python       "
print(text.center(20, "*"))   # "*******Python*******"
```

#### ljust() — Left Align

```python
text = "Python"
print(text.ljust(20, "-"))   # "Python--------------"
```

#### rjust() — Right Align

```python
text = "Python"
print(text.rjust(20, "-"))   # "--------------Python"
```

#### zfill() — Pad with Zeros

```python
num = "42"
print(num.zfill(5))   # 00042

negative = "-42"
print(negative.zfill(5))   # -0042
```

✔ Very useful for formatting numbers, IDs, dates.

---

### 🔸 String Type Checking Methods

These methods return **True** or **False**.

#### isalpha() — Only Letters?

```python
print("Python".isalpha())      # True
print("Python3".isalpha())     # False  (has number)
print("Hello World".isalpha()) # False  (has space)
```

#### isdigit() — Only Digits?

```python
print("12345".isdigit())    # True
print("123.45".isdigit())   # False  (has dot)
print("12 34".isdigit())    # False  (has space)
```

#### isalnum() — Letters or Digits (No Special Characters)?

```python
print("Python3".isalnum())     # True
print("Python 3".isalnum())    # False  (has space)
print("Python@3".isalnum())    # False  (has @)
```

#### isspace() — Only Whitespace?

```python
print("   ".isspace())      # True
print(" \t\n ".isspace())   # True
print("  a  ".isspace())    # False
```

#### isupper() / islower()

```python
print("PYTHON".isupper())   # True
print("python".islower())   # True
print("Python".isupper())   # False
print("Python".islower())   # False
```

#### istitle() — Title Case?

```python
print("Python Is Easy".istitle())   # True
print("Python is easy".istitle())   # False
```

#### isnumeric() vs isdigit() vs isdecimal()

```python
# For normal digits, all three work the same
print("123".isdigit())     # True
print("123".isnumeric())   # True
print("123".isdecimal())   # True

# For special number characters (like ²)
print("²".isdigit())       # True
print("²".isnumeric())     # True
print("²".isdecimal())     # False

# For fractions (like ½)
print("½".isdigit())       # False
print("½".isnumeric())     # True
print("½".isdecimal())     # False
```

| Method | Normal Digits | Superscripts (²) | Fractions (½) |
|--------|:---:|:---:|:---:|
| `isdecimal()` | ✅ | ❌ | ❌ |
| `isdigit()` | ✅ | ✅ | ❌ |
| `isnumeric()` | ✅ | ✅ | ✅ |

---

### 🔸 Other Useful Methods

#### expandtabs() — Set Tab Size

```python
text = "Name\tAge\tCity"
print(text.expandtabs(10))
```
Output:
```
Name      Age       City
```

#### encode() — Encode String to Bytes

```python
text = "Python"
encoded = text.encode("utf-8")
print(encoded)        # b'Python'
print(type(encoded))  # <class 'bytes'>
```

#### maketrans() and translate() — Character Mapping

```python
# Replace a→1, b→2, c→3
table = str.maketrans("abc", "123")
text = "abc def"
print(text.translate(table))   # 123 def
```

#### partition() — Split into 3 Parts

```python
text = "I love Python"
result = text.partition("love")
print(result)   # ('I ', 'love', ' Python')
```

✔ Returns a **tuple** of (before, match, after).

```python
# If not found
result = text.partition("Java")
print(result)   # ('I love Python', '', '')
```

#### rpartition() — Split from Right into 3 Parts

```python
text = "I love Python and I love Java"
result = text.rpartition("love")
print(result)   # ('I love Python and I ', 'love', ' Java')
```

---

## 🔹 String Formatting (VERY IMPORTANT 🔥)

### 🔸 1️⃣ Using `+` (Old Way — Not Recommended)

```python
name = "Giridhar"
age = 25

print("My name is " + name + " and I am " + str(age) + " years old")
```

⚠️ You must convert non-string types using `str()`. Gets messy with many variables.

---

### 🔸 2️⃣ Using `%` Formatting (Old Way)

```python
name = "Giridhar"
age = 25

print("My name is %s and I am %d years old" % (name, age))
```

| Placeholder | Meaning |
|------------|---------|
| `%s` | String |
| `%d` | Integer |
| `%f` | Float |
| `%.2f` | Float with 2 decimal places |

```python
price = 99.5
print("Price is %.2f" % price)   # Price is 99.50
```

---

### 🔸 3️⃣ Using `.format()` Method

```python
name = "Giridhar"
age = 25

print("My name is {} and age is {}".format(name, age))
```

#### With Index Positions

```python
print("{0} is {1} years old. {0} loves Python".format("Giridhar", 25))
# Giridhar is 25 years old. Giridhar loves Python
```

#### With Named Placeholders

```python
print("My name is {name} and age is {age}".format(name="Giridhar", age=25))
```

---

### 🔸 4️⃣ Using f-strings (Best Way ✅) — Python 3.6+

```python
name = "Giridhar"
age = 25

print(f"My name is {name} and I am {age} years old")
```

#### Expressions Inside f-strings

```python
a = 10
b = 20

print(f"Sum = {a + b}")          # Sum = 30
print(f"Is adult = {age >= 18}") # Is adult = True
```

#### Debugging with f-strings — `f"{x=}"` (Python 3.8+)

A quick way to print both the **variable name and its value**:

```python
name = "Giridhar"
age = 25
price = 99.5

print(f"{name=}")    # name='Giridhar'
print(f"{age=}")     # age=25
print(f"{price=}")   # price=99.5

# Works with expressions too
x = 10
print(f"{x * 2=}")   # x * 2=20
```

✔ Very useful for **quick debugging** — no need to write `print(f"name = {name}")` manually.

#### Formatting Numbers in f-strings

```python
price = 99.5678

print(f"Price: {price:.2f}")     # Price: 99.57   (2 decimal places)
print(f"Price: {price:.0f}")     # Price: 100     (no decimal)

big_num = 1000000
print(f"Number: {big_num:,}")    # Number: 1,000,000  (comma separator)
```

#### Padding in f-strings

```python
name = "Python"

print(f"{name:>20}")    # "              Python"  (right align)
print(f"{name:<20}")    # "Python              "  (left align)
print(f"{name:^20}")    # "       Python       "  (center)
print(f"{name:*^20}")   # "*******Python*******"  (center with *)
```

---

### 🔸 Formatting Summary

| Method | Example | Recommended? |
|--------|---------|:---:|
| `+` concatenation | `"Hi " + name` | ❌ |
| `%` formatting | `"Hi %s" % name` | ❌ |
| `.format()` | `"Hi {}".format(name)` | ✅ OK |
| f-string | `f"Hi {name}"` | ✅ Best |

---

## 🔹 String Conversion (Type Casting)

### 🔸 Convert Other Types to String → `str()`

```python
num = 100
print(type(num))        # <class 'int'>

text = str(num)
print(text)             # "100"
print(type(text))       # <class 'str'>
```

```python
print(str(3.14))     # "3.14"
print(str(True))     # "True"
print(str([1,2,3]))  # "[1, 2, 3]"
```

### 🔸 Convert String to Other Types

```python
# String to Integer
num = int("100")
print(num)          # 100
print(type(num))    # <class 'int'>

# String to Float
price = float("99.5")
print(price)        # 99.5

# String to List
text = "Python"
chars = list(text)
print(chars)        # ['P', 'y', 't', 'h', 'o', 'n']
```

⚠️ **Cannot convert non-numeric string to int/float:**
```python
int("hello")   # ❌ ValueError
float("abc")   # ❌ ValueError
```

---

## 🔹 String Multiplication vs Repetition

```python
# Repetition
print("Ha" * 3)     # HaHaHa

# Cannot multiply two strings
# print("Ha" * "Ha")   # ❌ TypeError

# Cannot add string and number
# print("Ha" + 3)      # ❌ TypeError
```

---

## 🔹 Multi-line Strings

### 🔸 Using Triple Quotes

```python
text = """This is line 1
This is line 2
This is line 3"""

print(text)
```

Output:
```
This is line 1
This is line 2
This is line 3
```

### 🔸 Using Backslash `\` (Line Continuation)

```python
text = "This is a very long string " \
       "that continues on the next line"

print(text)   # This is a very long string that continues on the next line
```

### 🔸 Using Parentheses

```python
text = ("This is a very long string "
        "that continues on the next line")

print(text)   # This is a very long string that continues on the next line
```

---

## 🔹 String Interning (Advanced — Interview Topic 🔥)

Python **reuses** small strings to save memory. This is called **string interning**.

```python
a = "hello"
b = "hello"

print(a is b)    # True   (same object in memory)
print(a == b)    # True   (same value)
```

⚠️ **`is` vs `==`:**

| Operator | Checks |
|----------|--------|
| `==` | Same **value** |
| `is` | Same **object in memory** |

```python
a = "hello world"
b = "hello world"

print(a == b)    # True   (same value)
print(a is b)    # May be True or False (depends on Python optimization)
```

✔ Always use `==` for string comparison, not `is`.

---

## 🔹 Useful Interview Programs 💡

### ✅ 1. Reverse a String

```python
text = "Python"
print(text[::-1])   # nohtyP
```

#### Without slicing (using while loop):

```python
text = "Python"
reversed_text = ""
i = len(text) - 1

while i >= 0:
    reversed_text = reversed_text + text[i]
    i = i - 1

print(reversed_text)   # nohtyP
```

#### Using for loop:

```python
text = "Python"
reversed_text = ""

for char in text:
    reversed_text = char + reversed_text

print(reversed_text)   # nohtyP
```

---

### ✅ 2. Check Palindrome

A palindrome reads the same forwards and backwards (e.g., "madam", "racecar").

#### Manual way (two-pointer approach):

```python
text = "madam"
text = text.lower()
left = 0
right = len(text) - 1
is_palindrome = True

while left < right:
    if text[left] != text[right]:
        is_palindrome = False
        break
    left = left + 1
    right = right - 1

if is_palindrome:
    print("Palindrome")
else:
    print("Not Palindrome")
```

🧠 How it works:
- Start with two pointers: one at the **beginning**, one at the **end**
- Compare characters at both positions
- If they don't match → not a palindrome
- Move both pointers inward and repeat

```
"madam"
 ↑   ↑     m == m ✅
  ↑ ↑      a == a ✅
   ↑       left meets right → Palindrome!
```

#### Pythonic shortcut:

```python
text = "madam"

if text == text[::-1]:
    print("Palindrome")
else:
    print("Not Palindrome")
```

✔ Understand the manual two-pointer logic first, then use the shortcut in real code.

---

### ✅ 3. Count Vowels in a String

#### Using while loop (basic way):

```python
text = "Python Programming"
count = 0
i = 0

while i < len(text):
    if text[i].lower() in "aeiou":
        count = count + 1
    i = i + 1

print("Vowels:", count)   # Vowels: 4
```

#### Using for loop:

```python
text = "Python Programming"
count = 0

for char in text.lower():
    if char in "aeiou":
        count = count + 1

print("Vowels:", count)   # Vowels: 4
```

---

### ✅ 4. Count Consonants

```python
text = "Python"
count = 0

for char in text.lower():
    if char.isalpha() and char not in "aeiou":
        count = count + 1

print("Consonants:", count)   # Consonants: 4
```

---

### ✅ 5. Count Words in a String

```python
text = "Python is very easy to learn"

words = text.split()
print("Word count:", len(words))   # Word count: 6
```

---

### ✅ 6. Reverse Each Word in a String

```python
text = "Python is easy"

words = text.split()          # ['Python', 'is', 'easy']
reversed_words = []

for word in words:
    reversed_words.append(word[::-1])

result = " ".join(reversed_words)
print(result)   # nohtyP si ysae
```

---

### ✅ 7. Reverse the Order of Words

```python
text = "Python is easy"

words = text.split()          # ['Python', 'is', 'easy']
words.reverse()               # ['easy', 'is', 'Python']
result = " ".join(words)
print(result)   # easy is Python
```

#### One-liner:

```python
text = "Python is easy"
print(" ".join(text.split()[::-1]))   # easy is Python
```

---

### ✅ 8. Check if Two Strings are Anagrams

Anagram = same characters, different order (e.g., "listen" and "silent").

#### Manual way (frequency counting with dictionary):

```python
str1 = "listen"
str2 = "silent"

freq1 = {}
for char in str1:
    if char in freq1:
        freq1[char] = freq1[char] + 1
    else:
        freq1[char] = 1

freq2 = {}
for char in str2:
    if char in freq2:
        freq2[char] = freq2[char] + 1
    else:
        freq2[char] = 1

if freq1 == freq2:
    print("Anagrams")
else:
    print("Not Anagrams")
```

🧠 How it works:
- Count how many times each character appears in both strings
- If the frequency dictionaries are equal → anagrams

#### Pythonic shortcut:

```python
str1 = "listen"
str2 = "silent"

if sorted(str1) == sorted(str2):
    print("Anagrams")
else:
    print("Not Anagrams")
```

🧠 `sorted()` converts string to a sorted list of characters:
```python
print(sorted("listen"))   # ['e', 'i', 'l', 'n', 's', 't']
print(sorted("silent"))   # ['e', 'i', 'l', 'n', 's', 't']
```

✔ Understand the frequency counting logic first, then use the sorted shortcut.

---

### ✅ 9. Remove Duplicates from a String

```python
text = "programming"
result = ""

for char in text:
    if char not in result:
        result = result + char

print(result)   # progamin
```

---

### ✅ 10. Find Most Frequent Character

#### Using basic loop:

```python
text = "programming"
max_char = ""
max_count = 0

for char in text:
    current_count = text.count(char)
    if current_count > max_count:
        max_count = current_count
        max_char = char

print(f"Most frequent: '{max_char}' appears {max_count} times")
# Most frequent: 'r' appears 2 times
```

---

### ✅ 11. Check if String Contains Only Digits

```python
text = "12345"

if text.isdigit():
    print("Only digits")
else:
    print("Not only digits")
```

---

### ✅ 12. Convert String to Title Case (Without title())

```python
text = "python is easy"
words = text.split()
result = []

for word in words:
    new_word = word[0].upper() + word[1:]
    result.append(new_word)

print(" ".join(result))   # Python Is Easy
```

---

### ✅ 13. Remove All Spaces from a String

```python
text = "P y t h o n"

# Method 1: replace
print(text.replace(" ", ""))   # Python

# Method 2: split + join
print("".join(text.split()))   # Python
```

---

### ✅ 14. Check if String Starts and Ends with Same Character

```python
text = "racecar"

if text[0] == text[-1]:
    print("Same start and end")
else:
    print("Different")
```

---

### ✅ 15. Count Uppercase and Lowercase Letters

```python
text = "Hello World Python"
upper_count = 0
lower_count = 0

for char in text:
    if char.isupper():
        upper_count = upper_count + 1
    elif char.islower():
        lower_count = lower_count + 1

print(f"Uppercase: {upper_count}")   # Uppercase: 3
print(f"Lowercase: {lower_count}")   # Lowercase: 12
```

---

### ✅ 16. Replace Spaces with Hyphens (URL Slug)

```python
title = "Python Is Easy To Learn"
slug = title.lower().replace(" ", "-")
print(slug)   # python-is-easy-to-learn
```

---

### ✅ 17. Extract Numbers from a String

```python
text = "I have 2 cats and 3 dogs"
numbers = ""

for char in text:
    if char.isdigit():
        numbers = numbers + char + " "

print("Numbers:", numbers)   # Numbers: 2 3
```

---

### ✅ 18. Check if All Characters are Unique

#### Manual way:

```python
text = "Python"
is_unique = True

for char in text:
    if text.count(char) > 1:
        is_unique = False
        break

if is_unique:
    print("All unique")
else:
    print("Has duplicates")
```

#### Pythonic shortcut (using set):

```python
text = "Python"

if len(set(text)) == len(text):
    print("All unique")
else:
    print("Has duplicates")
```

🧠 `set()` removes duplicates. If the set length equals the original length, all characters were unique.

✔ Understand the manual counting logic first, then use the set shortcut.

---

## 🔹 All String Methods — Quick Reference Table 📌

| Method | Description | Returns |
|--------|-------------|---------|
| `upper()` | Convert to uppercase | New string |
| `lower()` | Convert to lowercase | New string |
| `title()` | Title case | New string |
| `capitalize()` | Capitalize first letter | New string |
| `swapcase()` | Swap case | New string |
| `casefold()` | Aggressive lowercase | New string |
| `strip()` | Remove whitespace both sides | New string |
| `lstrip()` | Remove whitespace left | New string |
| `rstrip()` | Remove whitespace right | New string |
| `split()` | Split into list | List |
| `rsplit()` | Split from right | List |
| `splitlines()` | Split by lines | List |
| `join()` | Join list into string | New string |
| `find()` | Find first index | Int / -1 |
| `rfind()` | Find last index | Int / -1 |
| `index()` | Find first index | Int / Error |
| `rindex()` | Find last index | Int / Error |
| `count()` | Count occurrences | Int |
| `replace()` | Replace substring | New string |
| `startswith()` | Check start | Bool |
| `endswith()` | Check end | Bool |
| `isalpha()` | Only letters? | Bool |
| `isdigit()` | Only digits? | Bool |
| `isalnum()` | Letters or digits? | Bool |
| `isspace()` | Only whitespace? | Bool |
| `isupper()` | All uppercase? | Bool |
| `islower()` | All lowercase? | Bool |
| `istitle()` | Title case? | Bool |
| `isnumeric()` | Numeric? | Bool |
| `isdecimal()` | Decimal? | Bool |
| `center()` | Center align | New string |
| `ljust()` | Left align | New string |
| `rjust()` | Right align | New string |
| `zfill()` | Pad with zeros | New string |
| `expandtabs()` | Set tab size | New string |
| `encode()` | Encode to bytes | Bytes |
| `maketrans()` | Create translation table | Dict |
| `translate()` | Apply translation | New string |
| `partition()` | Split into 3 parts | Tuple |
| `rpartition()` | Split from right into 3 | Tuple |
| `format()` | Format string | New string |

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| String | Sequence of characters inside quotes |
| Creating | `' '`, `" "`, `''' '''`, `""" """` |
| Indexing | Access characters by position (starts from 0) |
| Negative Indexing | Access from end (-1 is last) |
| Slicing | Extract substrings `[start:end:step]` |
| Immutability | Cannot modify directly, create new string |
| Concatenation | Join strings with `+` |
| Repetition | Repeat with `*` |
| Membership | `in` / `not in` |
| Length | `len()` |
| Escape Characters | `\n`, `\t`, `\\`, `\'`, `\"` |
| Raw Strings | `r"text"` ignores escape characters |
| Case Methods | `upper()`, `lower()`, `title()`, `swapcase()` |
| Space Methods | `strip()`, `lstrip()`, `rstrip()` |
| Split & Join | `split()`, `join()` |
| Find & Replace | `find()`, `count()`, `replace()` |
| Type Checking | `isalpha()`, `isdigit()`, `isalnum()` |
| Formatting | f-strings (best), `.format()`, `%` |
| Comparison | `==`, `!=`, `<`, `>` (lexicographic) |
| ASCII | `ord()` → number, `chr()` → character |
| Looping | `for char in text`, `while`, `enumerate()` |
| Conversion | `str()`, `int()`, `float()`, `list()` |

---

> 🚀 **What's Next?**
> 👉 Lists in Python
> 👉 Tuples in Python
> 👉 Dictionaries in Python
> 👉 Sets in Python
