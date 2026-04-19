# 🎨 Decorators & Generators in Python - Complete Guide (Zero to Hero)

> **Decorators** modify function behavior without changing the function itself.
> **Generators** produce values one at a time, saving memory.

---

# Part 1: Decorators

---

## 🔹 What is a Decorator?

A decorator is a function that **wraps another function** to add extra behavior — without modifying the original function's code.

### 🧠 Real-World Analogy

> 👉 Think of a decorator like a **phone case**:
> - The phone (original function) stays the same
> - The case (decorator) adds protection, style, grip
> - You can swap cases without changing the phone

---

## 🔹 Prerequisites: Functions Are Objects

Before understanding decorators, remember these concepts from `functions.md`:

### 🔸 Functions Can Be Assigned to Variables

```python
def greet():
    return "Hello!"

say_hello = greet   # no parentheses — assigning the function itself
print(say_hello())  # Hello!
```

### 🔸 Functions Can Be Passed as Arguments

```python
def shout(func):
    result = func()
    return result.upper()

def greet():
    return "Hello!"

print(shout(greet))   # HELLO!
```

### 🔸 Functions Can Return Functions (Closures)

```python
def create_greeter(greeting):
    def greeter(name):
        return f"{greeting}, {name}!"
    return greeter

hello = create_greeter("Hello")
print(hello("Giridhar"))   # Hello, Giridhar!
```

---

## 🔹 Building a Decorator — Step by Step

### 🔸 Step 1: A Function That Wraps Another Function

```python
def my_decorator(func):
    def wrapper():
        print("Before the function")
        func()
        print("After the function")
    return wrapper

def say_hello():
    print("Hello!")

# Manually decorating
decorated = my_decorator(say_hello)
decorated()
```

Output:
```
Before the function
Hello!
After the function
```

### 🔸 Step 2: Using `@` Syntax (Syntactic Sugar)

```python
def my_decorator(func):
    def wrapper():
        print("Before the function")
        func()
        print("After the function")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()   # same output as above
```

🧠 `@my_decorator` is the same as writing `say_hello = my_decorator(say_hello)`.

---

## 🔹 Decorator with Arguments (IMPORTANT 🔥)

The wrapped function might accept arguments. Use `*args` and `**kwargs`.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Finished {func.__name__}")
        return result
    return wrapper

@my_decorator
def add(a, b):
    return a + b

@my_decorator
def greet(name):
    return f"Hello, {name}!"

print(add(3, 4))
print(greet("Giridhar"))
```

Output:
```
Calling add
Finished add
7
Calling greet
Finished greet
Hello, Giridhar!
```

---

## 🔹 Preserving Function Metadata — `functools.wraps`

Without `wraps`, the decorated function loses its original name and docstring.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def greet():
    """This function greets"""
    return "Hello!"

print(greet.__name__)   # wrapper  ← wrong! should be "greet"
print(greet.__doc__)    # None     ← lost the docstring!
```

### 🔸 Fix with `functools.wraps`

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def greet():
    """This function greets"""
    return "Hello!"

print(greet.__name__)   # greet  ✅
print(greet.__doc__)    # This function greets  ✅
```

✔ **Always use `@wraps(func)`** in your decorators. It's a best practice.

---

## 🔹 Practical Decorator Examples

### 🔸 1. Timer Decorator

```python
import time
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    return "Done!"

print(slow_function())
```

Output:
```
slow_function took 1.0012 seconds
Done!
```

### 🔸 2. Logger Decorator

```python
from functools import wraps

def logger(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@logger
def add(a, b):
    return a + b

add(3, 4)
```

Output:
```
Calling add with args=(3, 4), kwargs={}
add returned 7
```

### 🔸 3. Retry Decorator

```python
import time
from functools import wraps

def retry(max_attempts=3, delay=1):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            attempts = 0
            while attempts < max_attempts:
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    attempts = attempts + 1
                    print(f"Attempt {attempts} failed: {e}")
                    if attempts < max_attempts:
                        time.sleep(delay)
            raise Exception(f"All {max_attempts} attempts failed")
        return wrapper
    return decorator

@retry(max_attempts=3, delay=0.5)
def unstable_function():
    import random
    if random.random() < 0.7:
        raise ValueError("Random failure!")
    return "Success!"
```

### 🔸 4. Authorization Decorator

```python
from functools import wraps

def require_auth(func):
    @wraps(func)
    def wrapper(user, *args, **kwargs):
        if not user.get("is_authenticated", False):
            raise PermissionError("User is not authenticated!")
        return func(user, *args, **kwargs)
    return wrapper

@require_auth
def view_dashboard(user):
    return f"Welcome to dashboard, {user['name']}!"

# ✅ Authenticated user
user1 = {"name": "Giridhar", "is_authenticated": True}
print(view_dashboard(user1))   # Welcome to dashboard, Giridhar!

# ❌ Unauthenticated user
user2 = {"name": "Guest", "is_authenticated": False}
try:
    print(view_dashboard(user2))
except PermissionError as e:
    print(f"Error: {e}")   # Error: User is not authenticated!
```

---

## 🔹 Stacking Multiple Decorators

```python
def bold(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return f"<b>{func(*args, **kwargs)}</b>"
    return wrapper

def italic(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return f"<i>{func(*args, **kwargs)}</i>"
    return wrapper

@bold
@italic
def greet(name):
    return f"Hello, {name}"

print(greet("Giridhar"))   # <b><i>Hello, Giridhar</i></b>
```

🧠 Decorators are applied **bottom to top**:
1. `@italic` wraps `greet` first
2. `@bold` wraps the result of `@italic`

---

## 🔹 Class-Based Decorators

Instead of a function, you can use a **class** as a decorator using `__call__`.

```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0

    def __call__(self, *args, **kwargs):
        self.count = self.count + 1
        print(f"{self.func.__name__} called {self.count} times")
        return self.func(*args, **kwargs)

@CountCalls
def say_hello():
    print("Hello!")

say_hello()   # say_hello called 1 times \n Hello!
say_hello()   # say_hello called 2 times \n Hello!
say_hello()   # say_hello called 3 times \n Hello!
```

---

## 🔹 Built-in Decorators

| Decorator | Purpose | Covered In |
|-----------|---------|-----------|
| `@property` | Getter/setter as attribute | OOP Basics |
| `@classmethod` | Method bound to class | OOP Basics |
| `@staticmethod` | Utility method in class | OOP Basics |
| `@abstractmethod` | Force child implementation | OOP Basics |
| `@dataclass` | Auto-generate class methods | OOP Advanced |
| `@functools.wraps` | Preserve function metadata | This file |
| `@functools.lru_cache` | Cache function results | Below |

### 🔸 `@lru_cache` — Memoization (IMPORTANT 🔥)

Caches function results to avoid recomputation.

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(50))   # 12586269025  (instant! without cache it would take forever)
```

✔ Without `@lru_cache`, `fibonacci(50)` would make billions of recursive calls. With it, each unique input is computed **only once**.

---

# Part 2: Generators

---

## 🔹 What is a Generator?

A generator is a function that **produces values one at a time** using `yield` instead of `return`.

### 🧠 Real-World Analogy

> 👉 Think of a generator like a **vending machine**:
> - It doesn't dump all items at once
> - You press a button → get one item
> - Press again → get the next item
> - It remembers where it left off

---

## 🔹 Regular Function vs Generator

### 🔸 Regular Function — Returns All at Once

```python
def get_numbers():
    result = []
    i = 0
    while i < 5:
        result.append(i)
        i = i + 1
    return result

nums = get_numbers()
print(nums)   # [0, 1, 2, 3, 4]  ← entire list in memory
```

### 🔸 Generator Function — Yields One at a Time

```python
def get_numbers():
    i = 0
    while i < 5:
        yield i
        i = i + 1

nums = get_numbers()
print(nums)        # <generator object get_numbers at 0x...>
print(type(nums))  # <class 'generator'>

# Get values one at a time
print(next(nums))   # 0
print(next(nums))   # 1
print(next(nums))   # 2
print(next(nums))   # 3
print(next(nums))   # 4
print(next(nums))   # ❌ StopIteration
```

### 🔸 Key Differences

| | Regular Function | Generator Function |
|---|---|---|
| Keyword | `return` | `yield` |
| Returns | All values at once | One value at a time |
| Memory | Stores everything | Stores only current value |
| Reusable | ✅ Call again | ❌ Exhausted after one pass |
| Type | Returns value | Returns generator object |

---

## 🔹 How `yield` Works — Step by Step

```python
def countdown(n):
    print("Starting countdown")
    while n > 0:
        print(f"About to yield {n}")
        yield n
        print(f"Resumed after yielding {n}")
        n = n - 1
    print("Countdown finished")

gen = countdown(3)

print("--- First next() ---")
print(next(gen))

print("--- Second next() ---")
print(next(gen))

print("--- Third next() ---")
print(next(gen))
```

Output:
```
--- First next() ---
Starting countdown
About to yield 3
3
--- Second next() ---
Resumed after yielding 3
About to yield 2
2
--- Third next() ---
Resumed after yielding 2
About to yield 1
1
```

🧠 Key insight: `yield` **pauses** the function. `next()` **resumes** it from where it left off.

---

## 🔹 Iterating Over a Generator

```python
def squares(n):
    i = 0
    while i < n:
        yield i * i
        i = i + 1

# Using for loop (most common way)
for num in squares(5):
    print(num, end=" ")
```

Output:
```
0 1 4 9 16
```

✔ `for` loop automatically calls `next()` and handles `StopIteration`.

---

## 🔹 Generator Expressions (One-Liner Generators)

Like list comprehensions, but with **parentheses** instead of brackets.

```python
# List comprehension — creates entire list in memory
squares_list = [i * i for i in range(1000000)]

# Generator expression — creates values on demand
squares_gen = (i * i for i in range(1000000))

print(type(squares_list))   # <class 'list'>
print(type(squares_gen))    # <class 'generator'>
```

### 🔸 Memory Comparison

```python
import sys

list_comp = [i for i in range(1000000)]
gen_exp = (i for i in range(1000000))

print(f"List: {sys.getsizeof(list_comp)} bytes")   # ~8 MB
print(f"Generator: {sys.getsizeof(gen_exp)} bytes") # ~200 bytes!
```

✔ Generators use **almost no memory** regardless of how many items they produce.

### 🔸 Using Generator Expressions with Functions

```python
# Sum of squares — no intermediate list needed
total = sum(i * i for i in range(1000000))
print(total)

# Any / All with generators
has_even = any(i % 2 == 0 for i in [1, 3, 5, 4, 7])
print(has_even)   # True

all_positive = all(i > 0 for i in [1, 2, 3, 4])
print(all_positive)   # True
```

---

## 🔹 `yield from` — Delegating to Sub-Generators

```python
def inner():
    yield 1
    yield 2
    yield 3

def outer():
    yield "start"
    yield from inner()   # delegates to inner generator
    yield "end"

for item in outer():
    print(item)
```

Output:
```
start
1
2
3
end
```

### 🔸 Flattening Nested Lists with `yield from`

```python
def flatten(nested):
    for item in nested:
        if isinstance(item, list):
            yield from flatten(item)   # recursive delegation
        else:
            yield item

data = [1, [2, 3], [4, [5, 6]], 7]
print(list(flatten(data)))   # [1, 2, 3, 4, 5, 6, 7]
```

---

## 🔹 Generators Are Single-Use ⚠️

```python
gen = (i for i in range(3))

# First pass — works
for num in gen:
    print(num, end=" ")   # 0 1 2

print()

# Second pass — empty!
for num in gen:
    print(num, end=" ")   # (nothing printed)
```

✔ Once a generator is **exhausted**, you must create a **new one**.

---

## 🔹 Infinite Generators

Generators can produce values **forever** — useful for streams, IDs, etc.

```python
def infinite_counter(start=0):
    n = start
    while True:
        yield n
        n = n + 1

counter = infinite_counter(1)
print(next(counter))   # 1
print(next(counter))   # 2
print(next(counter))   # 3
# ... can go on forever
```

### 🔸 Fibonacci Generator

```python
def fibonacci():
    a = 0
    b = 1
    while True:
        yield a
        a, b = b, a + b

fib = fibonacci()
for i in range(10):
    print(next(fib), end=" ")
```

Output:
```
0 1 1 2 3 5 8 13 21 34
```

---

## 🔹 Iterators vs Generators

| | Iterator | Generator |
|---|---|---|
| Created by | Class with `__iter__` + `__next__` | Function with `yield` |
| Code | More boilerplate | Concise |
| State | Manual (`self.current`) | Automatic (Python handles it) |
| Memory | Depends | Always lazy |

### 🔸 Same Logic — Iterator vs Generator

#### Iterator (manual way):

```python
class Squares:
    def __init__(self, n):
        self.n = n
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current >= self.n:
            raise StopIteration
        result = self.current * self.current
        self.current = self.current + 1
        return result

for num in Squares(5):
    print(num, end=" ")   # 0 1 4 9 16
```

#### Generator (Pythonic way):

```python
def squares(n):
    i = 0
    while i < n:
        yield i * i
        i = i + 1

for num in squares(5):
    print(num, end=" ")   # 0 1 4 9 16
```

✔ Generators are **simpler** and **preferred** for most use cases.

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Forgetting `@wraps` in Decorators

```python
# ❌ Loses function name and docstring
def my_decorator(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

# ✅ Preserves metadata
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

### 🔸 Mistake 2: Reusing an Exhausted Generator

```python
gen = (i for i in range(3))
print(list(gen))   # [0, 1, 2]
print(list(gen))   # []  ← empty! generator is exhausted

# ✅ Create a new generator
gen = (i for i in range(3))
print(list(gen))   # [0, 1, 2]
```

### 🔸 Mistake 3: Confusing `return` and `yield`

```python
# return — function ends, returns one value
def get_nums():
    return [1, 2, 3]

# yield — function pauses, produces values one at a time
def get_nums():
    yield 1
    yield 2
    yield 3
```

---

## 🔹 Complete Summary 📌

### Decorators

| Concept | Description |
|---------|-------------|
| Decorator | Function that wraps another function |
| `@decorator` | Syntactic sugar for `func = decorator(func)` |
| `*args, **kwargs` | Accept any arguments in wrapper |
| `@wraps(func)` | Preserve original function metadata |
| Stacking | `@a @b` → b applied first, then a |
| Class decorator | Uses `__call__` method |
| `@lru_cache` | Cache function results (memoization) |

### Generators

| Concept | Description |
|---------|-------------|
| Generator | Function with `yield` |
| `yield` | Pauses function, produces one value |
| `next()` | Resumes generator, gets next value |
| `StopIteration` | Raised when generator is exhausted |
| Generator expression | `(x for x in ...)` |
| `yield from` | Delegate to sub-generator |
| Single-use | Cannot iterate twice |
| Memory efficient | Produces values on demand |
| Infinite | `while True: yield ...` |

---

> 🚀 **What's Next?**
> 👉 Modules & Packages
> 👉 Regular Expressions
> 👉 DSA with Python
