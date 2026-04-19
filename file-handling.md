# 📁 File Handling in Python - Complete Guide (Zero to Hero)

> File handling lets you **read from** and **write to** files on your computer.

---

## 🔹 What is File Handling?

File handling is the ability to **create, read, update, and delete** files using Python.

### 🧠 Real-World Analogy

> 👉 Think of a file like a **notebook**:
> - **Open** the notebook
> - **Read** what's written
> - **Write** new content
> - **Close** the notebook when done

---

## 🔹 Opening a File — `open()`

### Syntax:

```python
file = open(filename, mode)
```

### 🔸 File Modes

| Mode | Meaning | File Exists? | File Doesn't Exist? |
|:----:|---------|:---:|:---:|
| `"r"` | Read (default) | Opens file | ❌ FileNotFoundError |
| `"w"` | Write | Overwrites content | Creates new file |
| `"a"` | Append | Adds to end | Creates new file |
| `"x"` | Exclusive create | ❌ FileExistsError | Creates new file |
| `"r+"` | Read + Write | Opens file | ❌ FileNotFoundError |
| `"w+"` | Write + Read | Overwrites content | Creates new file |
| `"a+"` | Append + Read | Adds to end | Creates new file |

### 🔸 Text vs Binary Mode

| Suffix | Meaning | Example |
|:------:|---------|---------|
| `"t"` | Text mode (default) | `"rt"`, `"wt"` |
| `"b"` | Binary mode | `"rb"`, `"wb"` |

```python
# Text mode (default) — for .txt, .csv, .json
f = open("data.txt", "r")

# Binary mode — for images, PDFs, audio
f = open("image.png", "rb")
```

### 🔸 File Encoding (VERY IMPORTANT on Windows ⚠️)

Python's default encoding depends on your **Operating System**:
- **Windows** defaults to `cp1252`
- **Mac/Linux** defaults to `utf-8`

If your file contains special characters, emojis, or accented letters, the default Windows encoding will **crash** with `UnicodeDecodeError`.

```python
# ❌ May crash on Windows with special characters
f = open("data.txt", "r")

# ✅ Always specify encoding — works everywhere
f = open("data.txt", "r", encoding="utf-8")
```

✔ **Best practice:** Always pass `encoding="utf-8"` when opening text files. UTF-8 handles every character in every language.

```python
# Reading
with open("data.txt", "r", encoding="utf-8") as f:
    content = f.read()

# Writing
with open("output.txt", "w", encoding="utf-8") as f:
    f.write("Hello 🌍 Héllo Wörld")
```

⚠️ Binary mode (`"rb"`, `"wb"`) does **not** use encoding — it reads/writes raw bytes.

---

## 🔹 Reading Files

### 🔸 read() — Read Entire File

```python
f = open("data.txt", "r")
content = f.read()
print(content)
f.close()
```

### 🔸 read(n) — Read First n Characters

```python
f = open("data.txt", "r")
first_10 = f.read(10)
print(first_10)
f.close()
```

### 🔸 readline() — Read One Line

```python
f = open("data.txt", "r")
line1 = f.readline()
line2 = f.readline()
print(line1)
print(line2)
f.close()
```

### 🔸 readlines() — Read All Lines into a List

```python
f = open("data.txt", "r")
lines = f.readlines()
print(lines)   # ['line1\n', 'line2\n', 'line3\n']
f.close()
```

### 🔸 Iterating Line by Line (Best Way ✅)

```python
f = open("data.txt", "r")

for line in f:
    print(line.strip())   # strip() removes \n

f.close()
```

✔ This is **memory efficient** — reads one line at a time instead of loading the entire file.

---

## 🔹 Writing to Files

### 🔸 write() — Write a String

```python
f = open("output.txt", "w")
f.write("Hello, World!\n")
f.write("Python is great!\n")
f.close()
```

⚠️ `"w"` mode **overwrites** the entire file! Previous content is lost.

### 🔸 writelines() — Write a List of Strings

```python
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]

f = open("output.txt", "w")
f.writelines(lines)
f.close()
```

⚠️ `writelines()` does **NOT** add newlines automatically. You must include `\n` yourself.

### 🔸 Appending to a File

```python
f = open("output.txt", "a")
f.write("This is appended!\n")
f.close()
```

✔ `"a"` mode adds to the **end** of the file without erasing existing content.

---

## 🔹 The `with` Statement (VERY IMPORTANT 🔥)

The `with` statement **automatically closes** the file when done — even if an error occurs.

### 🔸 Without `with` (Manual Way)

```python
f = open("data.txt", "r")
try:
    content = f.read()
    print(content)
finally:
    f.close()
```

### 🔸 With `with` (Pythonic Way ✅)

```python
with open("data.txt", "r") as f:
    content = f.read()
    print(content)

# File is automatically closed here — no need for f.close()
```

### 🔸 Why `with` is Better

| | Manual `open/close` | `with` Statement |
|---|---|---|
| Auto-close | ❌ Must call `f.close()` | ✅ Automatic |
| Error-safe | ❌ File stays open on error | ✅ Closes even on error |
| Clean code | ❌ More lines | ✅ Cleaner |

✔ **Always use `with` for file operations.** This is the standard in professional Python code.

### 🔸 Multiple Files with `with`

```python
with open("input.txt", "r") as infile, open("output.txt", "w") as outfile:
    content = infile.read()
    outfile.write(content.upper())
```

---

## 🔹 File Pointer / Cursor

When you read a file, Python maintains a **cursor position**.

```python
with open("data.txt", "r") as f:
    print(f.read())     # reads entire file
    print(f.read())     # prints nothing! cursor is at the end

    f.seek(0)           # move cursor back to beginning
    print(f.read())     # reads entire file again
```

### 🔸 seek() and tell()

```python
with open("data.txt", "r") as f:
    print(f.tell())     # 0  (cursor at beginning)

    f.read(5)
    print(f.tell())     # 5  (cursor moved 5 characters)

    f.seek(0)           # move cursor to beginning
    print(f.tell())     # 0
```

---

## 🔹 Checking if File Exists

```python
import os

if os.path.exists("data.txt"):
    print("File exists")
else:
    print("File does not exist")

# Check if it's a file (not a directory)
print(os.path.isfile("data.txt"))    # True/False
print(os.path.isdir("my_folder"))    # True/False
```

### 🔸 Using pathlib (Modern Way ✅)

```python
from pathlib import Path

path = Path("data.txt")

print(path.exists())     # True/False
print(path.is_file())    # True/False
print(path.is_dir())     # True/False
```

---

## 🔹 Deleting and Renaming Files

```python
import os

# Rename
os.rename("old_name.txt", "new_name.txt")

# Delete
os.remove("file_to_delete.txt")

# Delete directory
os.rmdir("empty_folder")
```

---

## 🔹 Working with CSV Files

### 🔸 Reading CSV

```python
import csv

with open("data.csv", "r") as f:
    reader = csv.reader(f)

    for row in reader:
        print(row)   # each row is a list
```

### 🔸 Writing CSV

```python
import csv

data = [
    ["Name", "Age", "City"],
    ["Giridhar", 25, "Hyderabad"],
    ["Ravi", 30, "Mumbai"]
]

with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(data)
```

### 🔸 CSV with DictReader / DictWriter

```python
import csv

# Reading as dictionaries
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["Name"], row["Age"])

# Writing from dictionaries
data = [
    {"Name": "Giridhar", "Age": 25},
    {"Name": "Ravi", "Age": 30}
]

with open("output.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=["Name", "Age"])
    writer.writeheader()
    writer.writerows(data)
```

---

## 🔹 Working with JSON Files (VERY IMPORTANT 🔥)

### 🔸 Reading JSON

```python
import json

with open("data.json", "r") as f:
    data = json.load(f)

print(data)          # Python dict/list
print(type(data))    # <class 'dict'> or <class 'list'>
```

### 🔸 Writing JSON

```python
import json

data = {
    "name": "Giridhar",
    "age": 25,
    "skills": ["Python", "JavaScript"]
}

with open("output.json", "w") as f:
    json.dump(data, f, indent=4)
```

### 🔸 JSON String ↔ Python Object

```python
import json

# Python dict → JSON string
data = {"name": "Giridhar", "age": 25}
json_string = json.dumps(data, indent=2)
print(json_string)

# JSON string → Python dict
json_string = '{"name": "Giridhar", "age": 25}'
data = json.loads(json_string)
print(data["name"])   # Giridhar
```

### 🔸 JSON Functions Summary

| Function | Direction | Input | Output |
|----------|-----------|-------|--------|
| `json.dump()` | Python → JSON file | dict/list + file | Writes to file |
| `json.dumps()` | Python → JSON string | dict/list | Returns string |
| `json.load()` | JSON file → Python | file | Returns dict/list |
| `json.loads()` | JSON string → Python | string | Returns dict/list |

🧠 **Memory trick:** Functions with `s` work with **s**trings. Without `s` work with files.

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Forgetting to Close the File

```python
# ❌ File stays open
f = open("data.txt", "r")
content = f.read()
# forgot f.close()!

# ✅ Use with statement
with open("data.txt", "r") as f:
    content = f.read()
```

### 🔸 Mistake 2: Writing Without Newlines

```python
# ❌ All text on one line
with open("output.txt", "w") as f:
    f.write("Line 1")
    f.write("Line 2")
# File contains: Line 1Line 2

# ✅ Add \n
with open("output.txt", "w") as f:
    f.write("Line 1\n")
    f.write("Line 2\n")
```

### 🔸 Mistake 3: Using "w" When You Mean "a"

```python
# ❌ Overwrites entire file!
with open("log.txt", "w") as f:
    f.write("New log entry\n")

# ✅ Append to existing content
with open("log.txt", "a") as f:
    f.write("New log entry\n")
```

### 🔸 Mistake 4: Reading After Writing Without seek()

```python
with open("data.txt", "w+") as f:
    f.write("Hello")
    content = f.read()   # returns "" — cursor is at the end!

    f.seek(0)            # ✅ move cursor back
    content = f.read()   # "Hello"
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Count Lines, Words, Characters in a File

```python
with open("data.txt", "r") as f:
    lines = f.readlines()

line_count = len(lines)
word_count = 0
char_count = 0

for line in lines:
    words = line.split()
    word_count = word_count + len(words)
    char_count = char_count + len(line)

print(f"Lines: {line_count}")
print(f"Words: {word_count}")
print(f"Characters: {char_count}")
```

---

### ✅ 2. Copy File Contents

```python
with open("source.txt", "r") as src, open("dest.txt", "w") as dst:
    for line in src:
        dst.write(line)

print("File copied!")
```

---

### ✅ 3. Find and Replace in a File

```python
with open("data.txt", "r") as f:
    content = f.read()

new_content = content.replace("old_word", "new_word")

with open("data.txt", "w") as f:
    f.write(new_content)

print("Replaced!")
```

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| `open()` | Open a file |
| Modes | `r`, `w`, `a`, `x`, `r+`, `w+`, `a+` |
| `read()` | Read entire file |
| `readline()` | Read one line |
| `readlines()` | Read all lines into list |
| `write()` | Write string to file |
| `writelines()` | Write list of strings |
| `with` | Auto-close file (always use this!) |
| `seek()` / `tell()` | Move / check cursor position |
| `csv` module | Read/write CSV files |
| `json` module | Read/write JSON files |
| `json.dump/load` | File operations |
| `json.dumps/loads` | String operations |
| `os.path.exists()` | Check if file exists |
| `pathlib.Path` | Modern file path handling |

---

> 🚀 **Next:** Decorators & Generators →
