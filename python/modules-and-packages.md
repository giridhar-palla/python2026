# 📦 Modules & Packages in Python - Complete Guide (Zero to Hero)

> A module is a **file** containing Python code. A package is a **folder** containing modules.

---

## 🔹 What is a Module?

A module is simply a **`.py` file** that contains functions, classes, and variables you can reuse in other files.

### 🧠 Real-World Analogy

> 👉 Think of a module like a **toolbox**:
> - A carpenter has different toolboxes (modules) — one for hammers, one for screwdrivers
> - Instead of building every tool from scratch, you just grab the right toolbox
> - `import math` = grabbing the math toolbox

---

## 🔹 Why Use Modules?

| Without Modules | With Modules |
|----------------|-------------|
| All code in one giant file | Code split into organized files |
| Duplicate code everywhere | Write once, import anywhere |
| Hard to maintain | Easy to maintain |
| No code sharing | Share across projects |

---

## 🔹 Types of Modules

| Type | Description | Example |
|------|-------------|---------|
| **Built-in** | Come with Python | `math`, `os`, `sys`, `json` |
| **Third-party** | Installed via pip | `requests`, `numpy`, `flask` |
| **Custom** | Your own `.py` files | `my_utils.py` |

---

## 🔹 Importing Modules

### 🔸 1. import — Import Entire Module

```python
import math

print(math.pi)          # 3.141592653589793
print(math.sqrt(16))    # 4.0
print(math.factorial(5))  # 120
```

✔ Access everything with `module_name.function_name`.

### 🔸 2. from ... import — Import Specific Items

```python
from math import pi, sqrt, factorial

print(pi)            # 3.141592653589793
print(sqrt(16))      # 4.0
print(factorial(5))  # 120
```

✔ No need for `math.` prefix. But be careful of **name collisions**.

### 🔸 3. from ... import * — Import Everything (NOT Recommended ❌)

```python
from math import *

print(pi)       # works
print(sqrt(9))  # works
```

⚠️ **Don't use `import *`** in production code:
- You don't know what names are imported
- Can overwrite your own variables
- Makes debugging harder

```python
# ❌ Dangerous — pi could be your own variable
pi = 3.14
from math import *   # overwrites YOUR pi with math.pi!
```

### 🔸 4. import ... as — Alias

```python
import math as m

print(m.pi)        # 3.141592653589793
print(m.sqrt(16))  # 4.0
```

```python
from math import factorial as fact

print(fact(5))   # 120
```

✔ Common aliases in the real world:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

---

## 🔹 Creating Your Own Module

### 🔸 Step 1: Create a `.py` File

Create `my_utils.py`:

```python
# my_utils.py

PI = 3.14159

def greet(name):
    return f"Hello, {name}!"

def add(a, b):
    return a + b

def is_even(n):
    return n % 2 == 0

class Calculator:
    def multiply(self, a, b):
        return a * b
```

### 🔸 Step 2: Import and Use It

Create `main.py` in the **same folder**:

```python
# main.py
import my_utils

print(my_utils.greet("Giridhar"))   # Hello, Giridhar!
print(my_utils.add(3, 4))           # 7
print(my_utils.PI)                   # 3.14159

calc = my_utils.Calculator()
print(calc.multiply(5, 6))          # 30
```

Or import specific items:

```python
from my_utils import greet, add, PI

print(greet("Giridhar"))   # Hello, Giridhar!
print(add(3, 4))           # 7
```

---

## 🔹 The `__name__` Variable (VERY IMPORTANT 🔥)

Every Python file has a special variable `__name__`.

| When | `__name__` equals |
|------|------------------|
| File is **run directly** | `"__main__"` |
| File is **imported** | The module's name |

### 🔸 The Problem

```python
# my_utils.py
def greet(name):
    return f"Hello, {name}!"

# This runs when the file is imported too!
print(greet("Test"))
```

When you `import my_utils`, it prints "Hello, Test!" — which you don't want.

### 🔸 The Solution: `if __name__ == "__main__"`

```python
# my_utils.py
def greet(name):
    return f"Hello, {name}!"

# Only runs when this file is executed directly
if __name__ == "__main__":
    print(greet("Test"))
    print("Running tests...")
```

Now:
- Running `python my_utils.py` → prints "Hello, Test!" and "Running tests..."
- `import my_utils` in another file → prints **nothing** (test code is skipped)

✔ **Always use `if __name__ == "__main__"`** for test code, demo code, or scripts.

---

## 🔹 What is a Package?

A package is a **folder** containing multiple modules, organized with an `__init__.py` file.

### 🔸 Package Structure

```
my_project/
├── main.py
└── my_package/
    ├── __init__.py      ← makes it a package
    ├── math_utils.py
    ├── string_utils.py
    └── file_utils.py
```

### 🔸 `__init__.py`

This file tells Python that the folder is a **package**. It can be:
- **Empty** (just marks the folder as a package)
- **Contains initialization code** or imports

```python
# my_package/__init__.py

# You can make specific items available at the package level
from .math_utils import add, subtract
from .string_utils import capitalize_all
```

### 🔸 Importing from a Package

```python
# Method 1: Import the module
from my_package import math_utils
print(math_utils.add(3, 4))

# Method 2: Import specific function
from my_package.math_utils import add
print(add(3, 4))

# Method 3: If __init__.py exports it
from my_package import add   # works if __init__.py imports it
```

### 🔸 Sub-Packages (Nested Packages)

```
my_project/
└── my_package/
    ├── __init__.py
    ├── utils/
    │   ├── __init__.py
    │   ├── math_utils.py
    │   └── string_utils.py
    └── models/
        ├── __init__.py
        └── user.py
```

```python
from my_package.utils.math_utils import add
from my_package.models.user import User
```

---

## 🔹 Module Search Path

When you `import something`, Python searches in this order:

1. **Current directory**
2. **PYTHONPATH** environment variable
3. **Standard library** directories
4. **Site-packages** (third-party packages)

```python
import sys
print(sys.path)   # shows all search directories
```

### 🔸 Adding to the Search Path

```python
import sys
sys.path.append("/path/to/my/modules")
```

⚠️ This is a temporary fix. For permanent solutions, use proper package structure or virtual environments.

---

## 🔹 Installing Third-Party Packages — pip

### 🔸 Basic pip Commands

```bash
# Install a package
pip install requests

# Install specific version
pip install requests==2.28.0

# Upgrade a package
pip install --upgrade requests

# Uninstall
pip uninstall requests

# List installed packages
pip list

# Show package info
pip show requests

# Save all dependencies to a file
pip freeze > requirements.txt

# Install from requirements file
pip install -r requirements.txt
```

### 🔸 requirements.txt

```
requests==2.28.0
flask==2.3.0
numpy==1.24.0
```

✔ This file lists all your project's dependencies with exact versions. Essential for **reproducible environments**.

---

## 🔹 Virtual Environments (VERY IMPORTANT 🔥)

A virtual environment is an **isolated Python environment** for each project.

### 🧠 Why?

> 👉 Project A needs `requests==2.28`. Project B needs `requests==2.31`. Without virtual environments, they'd conflict. With them, each project has its own isolated packages.

### 🔸 Creating and Using a Virtual Environment

```bash
# Create
python -m venv myenv

# Activate (Windows)
myenv\Scripts\activate

# Activate (Mac/Linux)
source myenv/bin/activate

# Now pip installs go into this environment only
pip install requests

# Deactivate
deactivate
```

### 🔸 Best Practice

```bash
# 1. Create project folder
mkdir my_project
cd my_project

# 2. Create virtual environment
python -m venv venv

# 3. Activate it
venv\Scripts\activate

# 4. Install dependencies
pip install requests flask

# 5. Save dependencies
pip freeze > requirements.txt

# 6. Share with team — they run:
pip install -r requirements.txt
```

---

## 🔹 Useful Built-in Modules

### 🔸 `math` — Mathematical Functions

```python
import math

print(math.pi)            # 3.141592653589793
print(math.e)             # 2.718281828459045
print(math.sqrt(16))      # 4.0
print(math.ceil(3.2))     # 4
print(math.floor(3.8))    # 3
print(math.factorial(5))  # 120
print(math.gcd(12, 8))    # 4
print(math.log(100, 10))  # 2.0
print(math.pow(2, 10))    # 1024.0
print(math.inf)           # inf
```

### 🔸 `random` — Random Numbers

```python
import random

print(random.randint(1, 10))       # random int between 1 and 10
print(random.random())              # random float between 0 and 1
print(random.choice(["a", "b", "c"]))  # random item from list
print(random.sample(range(100), 5))    # 5 unique random numbers

nums = [1, 2, 3, 4, 5]
random.shuffle(nums)                # shuffles in-place
print(nums)
```

### 🔸 `datetime` — Dates and Times

```python
from datetime import datetime, date, timedelta

# Current date and time
now = datetime.now()
print(now)                    # 2025-04-19 14:30:00.123456

# Current date only
today = date.today()
print(today)                  # 2025-04-19

# Formatting
print(now.strftime("%Y-%m-%d"))          # 2025-04-19
print(now.strftime("%d/%m/%Y %H:%M"))    # 19/04/2025 14:30

# Parsing string to date
date_str = "2025-04-19"
parsed = datetime.strptime(date_str, "%Y-%m-%d")
print(parsed)

# Date arithmetic
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
print(tomorrow)
print(next_week)
```

### 🔸 `os` — Operating System Interaction

```python
import os

print(os.getcwd())              # current working directory
print(os.listdir("."))           # list files in current directory
print(os.path.exists("data.txt"))  # check if file exists
print(os.path.join("folder", "file.txt"))  # "folder/file.txt" or "folder\\file.txt"

os.makedirs("new_folder", exist_ok=True)   # create directory
```

### 🔸 `sys` — System-Specific Parameters

```python
import sys

print(sys.version)           # Python version
print(sys.platform)          # 'win32', 'linux', 'darwin'
print(sys.path)              # module search paths
print(sys.getsizeof([1,2]))  # memory size in bytes
# sys.exit()                 # exit the program
```

### 🔸 `string` — String Constants

```python
import string

print(string.ascii_letters)     # abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.ascii_lowercase)   # abcdefghijklmnopqrstuvwxyz
print(string.ascii_uppercase)   # ABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.digits)            # 0123456789
print(string.punctuation)       # !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

#### Practical Use: Generate Random Password

```python
import random
import string

chars = string.ascii_letters + string.digits + string.punctuation
password = ""

i = 0
while i < 12:
    password = password + random.choice(chars)
    i = i + 1

print(f"Password: {password}")

# Pythonic shortcut
password = "".join(random.choices(chars, k=12))
print(f"Password: {password}")
```

---

## 🔹 Relative vs Absolute Imports

### 🔸 Absolute Import (Recommended ✅)

```python
from my_package.utils.math_utils import add
```

### 🔸 Relative Import (Within a Package)

```python
# Inside my_package/utils/string_utils.py
from .math_utils import add          # same directory
from ..models.user import User       # parent directory
```

| Syntax | Meaning |
|--------|---------|
| `.` | Current package |
| `..` | Parent package |
| `...` | Grandparent package |

⚠️ Relative imports only work **inside packages**, not in standalone scripts.

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Naming Your File Same as a Module

```python
# ❌ If you create a file called "math.py"
import math
print(math.sqrt(16))   # ❌ AttributeError — imports YOUR math.py, not Python's!
```

✔ **Never name your files** `math.py`, `random.py`, `os.py`, `json.py`, etc.

### 🔸 Mistake 2: Circular Imports

```python
# a.py
from b import func_b

def func_a():
    return "A"

# b.py
from a import func_a   # ❌ ImportError — circular dependency!

def func_b():
    return "B"
```

✔ Fix: restructure code, use lazy imports, or move shared code to a third module.

### 🔸 Mistake 3: Using `import *`

```python
# ❌ Don't know what's imported, can overwrite variables
from math import *
from os import *   # might overwrite something from math!

# ✅ Import specific items
from math import sqrt, pi
from os import path
```

### 🔸 Mistake 4: Forgetting `__init__.py`

Without `__init__.py`, Python won't recognize the folder as a package (in Python < 3.3).

✔ In Python 3.3+, `__init__.py` is optional (namespace packages), but it's still **best practice** to include it.

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| Module | A `.py` file with reusable code |
| Package | A folder with `__init__.py` and modules |
| `import module` | Import entire module |
| `from module import x` | Import specific items |
| `import module as alias` | Import with alias |
| `from module import *` | ❌ Avoid — imports everything |
| `__name__` | `"__main__"` if run directly |
| `if __name__ == "__main__"` | Guard for test/demo code |
| `pip install` | Install third-party packages |
| `requirements.txt` | List of project dependencies |
| `venv` | Virtual environment for isolation |
| `sys.path` | Module search path |
| Relative import | `.` current, `..` parent package |
| Circular import | ❌ Avoid — restructure code |
| File naming | Never name files same as built-in modules |

---

> 🚀 **Next:** Regular Expressions →
