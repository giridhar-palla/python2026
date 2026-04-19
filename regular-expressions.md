# 🔍 Regular Expressions in Python - Complete Guide (Zero to Hero)

> Regular expressions (regex) let you **search, match, and manipulate text** using patterns.

---

## 🔹 What is a Regular Expression?

A regular expression (regex) is a **pattern** that describes a set of strings. It's like a search query on steroids.

### 🧠 Real-World Analogy

> 👉 Think of regex like a **metal detector on a beach**:
> - You define what you're looking for (the pattern)
> - You sweep across the sand (the text)
> - It beeps when it finds a match
>
> `\d{3}-\d{3}-\d{4}` = "find anything that looks like a phone number"

---

## 🔹 Why Learn Regex?

| Use Case | Example |
|----------|---------|
| Validate email | `user@domain.com` |
| Validate phone number | `123-456-7890` |
| Extract data from text | Find all URLs in a webpage |
| Search and replace | Replace all dates in a document |
| Parse log files | Extract timestamps and error codes |
| Clean user input | Remove special characters |

---

## 🔹 The `re` Module

Python's regex functionality lives in the built-in `re` module.

```python
import re
```

---

## 🔹 Basic Functions

### 🔸 re.search() — Find First Match Anywhere

```python
import re

text = "My phone is 123-456-7890"
match = re.search(r"\d{3}-\d{3}-\d{4}", text)

if match:
    print(f"Found: {match.group()}")   # Found: 123-456-7890
    print(f"Position: {match.start()}-{match.end()}")   # Position: 13-25
```

### 🔸 re.match() — Match at the BEGINNING Only

```python
import re

text = "Hello World"

match = re.match(r"Hello", text)
print(match.group() if match else "No match")   # Hello

match = re.match(r"World", text)
print(match.group() if match else "No match")   # No match  ← not at beginning!
```

### 🔸 re.fullmatch() — Match the ENTIRE String

```python
import re

print(re.fullmatch(r"\d+", "12345"))    # Match  (entire string is digits)
print(re.fullmatch(r"\d+", "123abc"))   # None   (not entirely digits)
```

### 🔸 re.findall() — Find ALL Matches (Returns List)

```python
import re

text = "Call 123-456-7890 or 987-654-3210"
matches = re.findall(r"\d{3}-\d{3}-\d{4}", text)
print(matches)   # ['123-456-7890', '987-654-3210']
```

### 🔸 re.finditer() — Find ALL Matches (Returns Iterator with Details)

```python
import re

text = "Call 123-456-7890 or 987-654-3210"

for match in re.finditer(r"\d{3}-\d{3}-\d{4}", text):
    print(f"Found: {match.group()} at position {match.start()}-{match.end()}")
```

### 🔸 re.sub() — Search and Replace

```python
import re

text = "I love Java and Java is great"
result = re.sub(r"Java", "Python", text)
print(result)   # I love Python and Python is great

# Replace only first occurrence
result = re.sub(r"Java", "Python", text, count=1)
print(result)   # I love Python and Java is great
```

### 🔸 re.split() — Split by Pattern

```python
import re

text = "apple, banana;  cherry:date"
result = re.split(r"[,;\s:]+", text)
print(result)   # ['apple', 'banana', 'cherry', 'date']
```

✔ Much more powerful than `str.split()` — can split by **multiple delimiters** at once.

### 🔸 Functions Summary

| Function | Purpose | Returns |
|----------|---------|---------|
| `re.search(pattern, text)` | Find first match anywhere | Match object or None |
| `re.match(pattern, text)` | Match at beginning only | Match object or None |
| `re.fullmatch(pattern, text)` | Match entire string | Match object or None |
| `re.findall(pattern, text)` | Find all matches | List of strings |
| `re.finditer(pattern, text)` | Find all matches with details | Iterator of Match objects |
| `re.sub(pattern, repl, text)` | Search and replace | New string |
| `re.split(pattern, text)` | Split by pattern | List of strings |

---

## 🔹 Regex Patterns — The Language

### 🔸 Literal Characters

```python
import re

# Matches the exact text
print(re.findall(r"cat", "the cat sat on the mat"))   # ['cat']
```

### 🔸 Metacharacters (Special Characters)

| Character | Meaning | Example | Matches |
|:---------:|---------|---------|---------|
| `.` | Any character (except newline) | `c.t` | cat, cot, cut |
| `^` | Start of string | `^Hello` | "Hello world" ✅ |
| `$` | End of string | `world$` | "Hello world" ✅ |
| `\` | Escape special character | `\.` | literal dot |
| `\|` | OR | `cat\|dog` | cat or dog |

```python
import re

# . matches any character
print(re.findall(r"c.t", "cat cot cut cit c9t"))
# ['cat', 'cot', 'cut', 'cit', 'c9t']

# ^ and $
print(re.search(r"^Hello", "Hello World"))   # Match
print(re.search(r"^World", "Hello World"))   # None

print(re.search(r"World$", "Hello World"))   # Match
print(re.search(r"Hello$", "Hello World"))   # None
```

---

### 🔸 Character Classes `[]`

| Pattern | Meaning | Example |
|---------|---------|---------|
| `[abc]` | a, b, or c | `[aeiou]` matches vowels |
| `[a-z]` | Any lowercase letter | `[a-z]+` matches words |
| `[A-Z]` | Any uppercase letter | |
| `[0-9]` | Any digit | Same as `\d` |
| `[a-zA-Z]` | Any letter | |
| `[^abc]` | NOT a, b, or c | `[^0-9]` matches non-digits |

```python
import re

text = "Hello World 123"

print(re.findall(r"[aeiou]", text.lower()))   # ['e', 'o', 'o']
print(re.findall(r"[0-9]", text))              # ['1', '2', '3']
print(re.findall(r"[^a-zA-Z ]", text))         # ['1', '2', '3']
```

---

### 🔸 Shorthand Character Classes

| Shorthand | Meaning | Equivalent |
|:---------:|---------|-----------|
| `\d` | Any digit | `[0-9]` |
| `\D` | Any non-digit | `[^0-9]` |
| `\w` | Any word character | `[a-zA-Z0-9_]` |
| `\W` | Any non-word character | `[^a-zA-Z0-9_]` |
| `\s` | Any whitespace | `[ \t\n\r\f\v]` |
| `\S` | Any non-whitespace | `[^ \t\n\r\f\v]` |

```python
import re

text = "Hello World 123!"

print(re.findall(r"\d", text))    # ['1', '2', '3']
print(re.findall(r"\w+", text))   # ['Hello', 'World', '123']
print(re.findall(r"\s", text))    # [' ', ' ']
```

---

### 🔸 Quantifiers — How Many Times?

| Quantifier | Meaning | Example | Matches |
|:----------:|---------|---------|---------|
| `*` | 0 or more | `ab*c` | ac, abc, abbc |
| `+` | 1 or more | `ab+c` | abc, abbc (NOT ac) |
| `?` | 0 or 1 | `colou?r` | color, colour |
| `{n}` | Exactly n | `\d{3}` | 123 |
| `{n,}` | n or more | `\d{2,}` | 12, 123, 1234 |
| `{n,m}` | Between n and m | `\d{2,4}` | 12, 123, 1234 |

```python
import re

# * — zero or more
print(re.findall(r"go*d", "gd god good goood"))
# ['gd', 'god', 'good', 'goood']

# + — one or more
print(re.findall(r"go+d", "gd god good goood"))
# ['god', 'good', 'goood']  (NOT 'gd')

# ? — zero or one
print(re.findall(r"colou?r", "color colour"))
# ['color', 'colour']

# {n} — exactly n
print(re.findall(r"\d{3}", "12 123 1234 12345"))
# ['123', '123', '123']
```

---

### 🔸 Greedy vs Lazy (IMPORTANT 🔥)

By default, quantifiers are **greedy** — they match as much as possible.

```python
import re

text = "<b>Hello</b> and <b>World</b>"

# Greedy (default) — matches as MUCH as possible
print(re.findall(r"<b>.*</b>", text))
# ['<b>Hello</b> and <b>World</b>']  ← grabbed everything!

# Lazy (add ?) — matches as LITTLE as possible
print(re.findall(r"<b>.*?</b>", text))
# ['<b>Hello</b>', '<b>World</b>']  ← two separate matches
```

| Greedy | Lazy | Meaning |
|:------:|:----:|---------|
| `*` | `*?` | 0 or more (minimal) |
| `+` | `+?` | 1 or more (minimal) |
| `?` | `??` | 0 or 1 (minimal) |
| `{n,m}` | `{n,m}?` | Between n and m (minimal) |

---

### 🔸 Groups `()` — Capture Parts of a Match

```python
import re

text = "John is 25 years old. Jane is 30 years old."

matches = re.findall(r"(\w+) is (\d+) years old", text)
print(matches)   # [('John', '25'), ('Jane', '30')]
```

🧠 Parentheses `()` create **capture groups**. `findall()` returns the groups as tuples.

### 🔸 Named Groups

```python
import re

text = "2025-04-19"
match = re.search(r"(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})", text)

if match:
    print(match.group("year"))    # 2025
    print(match.group("month"))   # 04
    print(match.group("day"))     # 19
```

### 🔸 Non-Capturing Groups `(?:...)`

```python
import re

# Capturing group — included in findall results
print(re.findall(r"(cat|dog)", "I have a cat and a dog"))
# ['cat', 'dog']

# Non-capturing group — NOT included in results
print(re.findall(r"(?:cat|dog) food", "cat food and dog food"))
# ['cat food', 'dog food']
```

---

### 🔸 Anchors and Boundaries

| Pattern | Meaning |
|---------|---------|
| `^` | Start of string |
| `$` | End of string |
| `\b` | Word boundary |
| `\B` | Not a word boundary |

```python
import re

# Word boundary — matches whole words only
text = "cat concatenate category"

print(re.findall(r"cat", text))      # ['cat', 'cat', 'cat']  ← finds partial matches
print(re.findall(r"\bcat\b", text))  # ['cat']  ← only the standalone word
```

---

### 🔸 Lookahead and Lookbehind (ADVANCED)

| Pattern | Name | Meaning |
|---------|------|---------|
| `(?=...)` | Positive lookahead | Followed by ... |
| `(?!...)` | Negative lookahead | NOT followed by ... |
| `(?<=...)` | Positive lookbehind | Preceded by ... |
| `(?<!...)` | Negative lookbehind | NOT preceded by ... |

```python
import re

# Positive lookahead — find digits followed by "px"
text = "12px 14em 16px 18pt"
print(re.findall(r"\d+(?=px)", text))   # ['12', '16']

# Negative lookahead — find digits NOT followed by "px"
print(re.findall(r"\d+(?!px)", text))   # ['1', '14', '1', '18']

# Positive lookbehind — find digits preceded by "$"
text = "Price: $100 and $200"
print(re.findall(r"(?<=\$)\d+", text))  # ['100', '200']
```

---

## 🔹 Flags (Modifiers)

| Flag | Meaning |
|------|---------|
| `re.IGNORECASE` or `re.I` | Case-insensitive matching |
| `re.MULTILINE` or `re.M` | `^` and `$` match each line |
| `re.DOTALL` or `re.S` | `.` matches newline too |
| `re.VERBOSE` or `re.X` | Allow comments in pattern |

```python
import re

# Case-insensitive
print(re.findall(r"python", "Python PYTHON python", re.IGNORECASE))
# ['Python', 'PYTHON', 'python']

# Verbose — readable patterns with comments
pattern = re.compile(r"""
    \d{3}       # area code
    [-.]         # separator
    \d{3}       # first 3 digits
    [-.]         # separator
    \d{4}       # last 4 digits
""", re.VERBOSE)

print(pattern.findall("Call 123-456-7890 or 987.654.3210"))
# ['123-456-7890', '987.654.3210']
```

---

## 🔹 Compiling Patterns — re.compile()

If you use the same pattern multiple times, **compile it** for better readability.

```python
import re

# Without compile — pattern string repeated
result1 = re.findall(r"\d+", "abc 123 def 456")
result2 = re.search(r"\d+", "abc 123 def 456")

# With compile — pattern object reused
pattern = re.compile(r"\d+")
result1 = pattern.findall("abc 123 def 456")
result2 = pattern.search("abc 123 def 456")
```

---

## 🔹 Raw Strings `r""` — Why We Use Them

```python
# Without raw string — backslash issues
print(re.findall("\d+", "abc 123"))    # works but risky
print(re.findall("\\d+", "abc 123"))   # escaped backslash — ugly

# With raw string — clean and safe
print(re.findall(r"\d+", "abc 123"))   # ✅ always use r"" for regex
```

✔ **Always use raw strings `r"..."`** for regex patterns. It prevents Python from interpreting `\d`, `\b`, `\n` as escape characters.

---

## 🔹 Manual vs Regex — Comparison

### 🔸 Extract All Numbers from Text

#### Manual way:

```python
text = "I have 2 cats and 3 dogs and 10 fish"
numbers = []
current = ""

for char in text:
    if char.isdigit():
        current = current + char
    else:
        if current != "":
            numbers.append(int(current))
            current = ""

if current != "":
    numbers.append(int(current))

print(numbers)   # [2, 3, 10]
```

#### Regex way:

```python
import re

text = "I have 2 cats and 3 dogs and 10 fish"
numbers = [int(n) for n in re.findall(r"\d+", text)]
print(numbers)   # [2, 3, 10]
```

### 🔸 Validate Email Format

#### Manual way:

```python
def is_valid_email(email):
    if "@" not in email:
        return False
    parts = email.split("@")
    if len(parts) != 2:
        return False
    local, domain = parts
    if len(local) == 0 or len(domain) == 0:
        return False
    if "." not in domain:
        return False
    return True

print(is_valid_email("user@example.com"))   # True
print(is_valid_email("invalid-email"))       # False
```

#### Regex way:

```python
import re

def is_valid_email(email):
    pattern = r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
    return re.fullmatch(pattern, email) is not None

print(is_valid_email("user@example.com"))   # True
print(is_valid_email("invalid-email"))       # False
```

---

## 🔹 Common Regex Patterns (Cheat Sheet 🔥)

| Pattern | Matches | Example |
|---------|---------|---------|
| `\d+` | One or more digits | `123` |
| `\w+` | One or more word chars | `hello_123` |
| `[a-zA-Z]+` | One or more letters | `Hello` |
| `\d{3}-\d{3}-\d{4}` | US phone number | `123-456-7890` |
| `\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}` | IP address (basic) | `192.168.1.1` |
| `\d{4}-\d{2}-\d{2}` | Date (YYYY-MM-DD) | `2025-04-19` |
| `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$` | Email (basic) | `user@example.com` |
| `https?://\S+` | URL | `https://example.com` |
| `\b\w+\b` | Whole words | Each word separately |
| `^\s+\|\s+$` | Leading/trailing whitespace | For trimming |

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Forgetting Raw Strings

```python
# ❌ \b is interpreted as backspace by Python
re.findall("\bcat\b", "the cat sat")   # []  ← no match!

# ✅ Use raw string
re.findall(r"\bcat\b", "the cat sat")  # ['cat']
```

### 🔸 Mistake 2: Greedy Matching

```python
# ❌ Greedy — grabs too much
re.findall(r"<.*>", "<b>Hello</b>")   # ['<b>Hello</b>']

# ✅ Lazy — grabs minimum
re.findall(r"<.*?>", "<b>Hello</b>")  # ['<b>', '</b>']
```

### 🔸 Mistake 3: match() vs search()

```python
import re

text = "Hello World"

# match() only checks the BEGINNING
print(re.match(r"World", text))    # None!

# search() checks ANYWHERE
print(re.search(r"World", text))   # Match!
```

### 🔸 Mistake 4: Not Checking for None

```python
import re

match = re.search(r"\d+", "no numbers here")

# ❌ Crashes if no match
# print(match.group())   # AttributeError: 'NoneType' has no attribute 'group'

# ✅ Always check first
if match:
    print(match.group())
else:
    print("No match found")
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Extract All Email Addresses from Text

```python
import re

text = "Contact us at support@example.com or sales@company.org for help"
emails = re.findall(r"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}", text)
print(emails)   # ['support@example.com', 'sales@company.org']
```

---

### ✅ 2. Validate a Phone Number

```python
import re

def is_valid_phone(phone):
    pattern = r"^\d{3}-\d{3}-\d{4}$"
    return re.fullmatch(pattern, phone) is not None

print(is_valid_phone("123-456-7890"))   # True
print(is_valid_phone("12-456-7890"))    # False
print(is_valid_phone("1234567890"))     # False
```

---

### ✅ 3. Remove All HTML Tags

#### Manual way:

```python
text = "<p>Hello <b>World</b></p>"
result = ""
inside_tag = False

for char in text:
    if char == "<":
        inside_tag = True
    elif char == ">":
        inside_tag = False
    elif not inside_tag:
        result = result + char

print(result)   # Hello World
```

#### Regex way:

```python
import re

text = "<p>Hello <b>World</b></p>"
result = re.sub(r"<[^>]+>", "", text)
print(result)   # Hello World
```

---

### ✅ 4. Find All Words Starting with a Capital Letter

```python
import re

text = "Alice went to Paris with Bob"
words = re.findall(r"\b[A-Z][a-z]*\b", text)
print(words)   # ['Alice', 'Paris', 'Bob']
```

---

### ✅ 5. Replace Multiple Spaces with Single Space

#### Manual way:

```python
text = "Hello    World   Python"
result = ""
prev_space = False

for char in text:
    if char == " ":
        if not prev_space:
            result = result + char
        prev_space = True
    else:
        result = result + char
        prev_space = False

print(result)   # "Hello World Python"
```

#### Regex way:

```python
import re

text = "Hello    World   Python"
result = re.sub(r"\s+", " ", text)
print(result)   # "Hello World Python"
```

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| `re.search()` | Find first match anywhere |
| `re.match()` | Match at beginning only |
| `re.fullmatch()` | Match entire string |
| `re.findall()` | Find all matches (list) |
| `re.finditer()` | Find all matches (iterator) |
| `re.sub()` | Search and replace |
| `re.split()` | Split by pattern |
| `re.compile()` | Pre-compile pattern |
| `.` | Any character |
| `\d`, `\w`, `\s` | Digit, word char, whitespace |
| `[]` | Character class |
| `*`, `+`, `?` | Quantifiers (0+, 1+, 0/1) |
| `{n}`, `{n,m}` | Exact/range quantifiers |
| `*?`, `+?` | Lazy (minimal) matching |
| `()` | Capture group |
| `(?P<name>)` | Named group |
| `(?:...)` | Non-capturing group |
| `^`, `$` | Start/end anchors |
| `\b` | Word boundary |
| `(?=)`, `(?<=)` | Lookahead/lookbehind |
| `re.I` | Case-insensitive flag |
| `re.VERBOSE` | Allow comments in pattern |
| `r""` | Raw string (always use for regex) |

---

> 🚀 This completes the Python Foundations series!
