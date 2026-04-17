# 🐍 Python - Complete Interview Preparation (Zero to Hero)

## 🔹 What is Python?

Python is a **high-level, interpreted, general-purpose programming language**.

Created by **Guido van Rossum** in **1991**.

### 🧠 Real-World Analogy
> Think of Python as **English among programming languages** — easy to read, easy to write, and understood by almost everyone.

---

## 🔹 Why Python?

| Feature | Meaning |
|---------|---------|
| Easy to learn | Simple syntax, like writing English |
| Interpreted | No need to compile, runs line by line |
| Dynamically typed | No need to declare variable types |
| Huge community | Tons of libraries and support |
| Cross-platform | Works on Windows, Mac, Linux |
| Free & Open Source | No cost, anyone can use |

---

## 🔹 Where is Python Used?

| Area | Example |
|------|---------|
| Web Development | Django, Flask |
| Data Science | Pandas, NumPy |
| Machine Learning | TensorFlow, Scikit-learn |
| Automation | Scripting, Web Scraping |
| Desktop Apps | Tkinter, PyQt |
| Game Development | Pygame |
| API Development | FastAPI, Flask |

---

## 🔹 Installing Python

1. Go to [python.org](https://www.python.org/)
2. Download the latest version
3. During installation ✅ **Check "Add Python to PATH"**
4. Verify installation:

```python
python --version
```

Output:
```
Python 3.x.x
```

---

## 🔹 Your First Python Program

```python
print("Hello, World!")
```

Output:
```
Hello, World!
```

### 🧠 What happened?
- `print()` is a **built-in function**
- It displays whatever is inside the parentheses
- `"Hello, World!"` is a **string** (text inside quotes)

---

## 🔹 Python Syntax Rules

### ✅ No semicolons needed
```python
print("Hello")
print("World")
```

### ✅ Indentation matters (VERY IMPORTANT 🔥)
```python
# ✅ Correct
if True:
    print("Hello")

# ❌ Wrong - will give error
if True:
print("Hello")
```

### ✅ Comments

```python
# This is a single-line comment

"""
This is a
multi-line comment
"""
```

---

## 🔹 Python Keywords

Keywords are **reserved words** that Python uses internally. You **cannot** use them as variable names.

```python
import keyword
print(keyword.kwlist)
```

Common keywords:
```
if, else, elif, for, while, break, continue, return,
def, class, import, from, True, False, None, and, or,
not, in, is, try, except, finally, raise, with, as,
pass, lambda, global, nonlocal, yield, del, assert
```

---

## 🔹 Python Indentation

Python uses **indentation (spaces/tabs)** to define blocks of code.

Other languages use `{}` curly braces, but Python uses **4 spaces**.

```python
# ✅ Correct
if 5 > 2:
    print("Five is greater")

# ❌ Wrong
if 5 > 2:
print("Five is greater")   # IndentationError
```

---

## 🔹 Taking Input from User

```python
name = input("Enter your name: ")
print("Hello", name)
```

⚠️ **Important:** `input()` always returns a **string**

```python
age = input("Enter age: ")
print(type(age))   # <class 'str'>
```

To get a number:
```python
age = int(input("Enter age: "))
print(type(age))   # <class 'int'>
```

---

## 🔹 Print Function in Detail

### Basic print
```python
print("Hello")
```

### Print multiple values
```python
print("Name:", "Python", "Age:", 30)
```
Output: `Name: Python Age: 30`

### sep parameter (separator)
```python
print("A", "B", "C", sep="-")
```
Output: `A-B-C`

### end parameter
```python
print("Hello", end=" ")
print("World")
```
Output: `Hello World`

(Without `end`, each print goes to a new line)

---

## 🔹 Summary 📌

| Concept | Description |
|---------|-------------|
| Python | High-level, interpreted language |
| print() | Display output |
| input() | Take user input |
| Comments | # for single, """ for multi-line |
| Indentation | 4 spaces, defines code blocks |
| Keywords | Reserved words |

---

> 🚀 **Next:** Variables and Data Types →
