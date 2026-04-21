# ⚠️ Exception Handling in Python - Complete Guide (Zero to Hero)

> Exception handling lets you **gracefully deal with errors** instead of crashing your program.

---

## 🔹 What is an Exception?

An exception is an **error that occurs during program execution**. When Python encounters an error, it **stops** the program and shows an error message.

### 🧠 Real-World Analogy

> 👉 Think of exceptions like **road hazards**:
> - You're driving (running code)
> - You hit a pothole (error occurs)
> - Without handling: your car breaks down (program crashes)
> - With handling: you swerve around it and keep driving (program continues)

---

## 🔹 Error vs Exception

| Term | Meaning | Example |
|------|---------|---------|
| **Syntax Error** | Code is written wrong — Python can't even run it | `if True print("Hi")` |
| **Exception** | Code is valid but fails during execution | `10 / 0` |

```python
# Syntax Error — caught BEFORE running
if True
    print("Hello")   # SyntaxError: expected ':'

# Exception — caught DURING running
print(10 / 0)   # ZeroDivisionError: division by zero
```

✔ You can **handle exceptions**. You **cannot handle syntax errors** (fix the code instead).

---

## 🔹 Common Built-in Exceptions

| Exception | When It Happens | Example |
|-----------|----------------|---------|
| `ZeroDivisionError` | Dividing by zero | `10 / 0` |
| `TypeError` | Wrong type operation | `"hello" + 5` |
| `ValueError` | Right type, wrong value | `int("hello")` |
| `IndexError` | Index out of range | `[1,2,3][10]` |
| `KeyError` | Dict key not found | `{"a":1}["b"]` |
| `NameError` | Variable not defined | `print(xyz)` |
| `AttributeError` | Object has no attribute | `"hello".push()` |
| `FileNotFoundError` | File doesn't exist | `open("xyz.txt")` |
| `ImportError` | Module not found | `import xyz` |
| `StopIteration` | Iterator exhausted | `next()` on empty |
| `OverflowError` | Number too large | `math.exp(1000)` |
| `RecursionError` | Too many recursive calls | Infinite recursion |
| `PermissionError` | No file permission | Writing to read-only |
| `IndentationError` | Wrong indentation | Missing/extra spaces |

---

## 🔹 The `try-except` Block

### Syntax:

```python
try:
    # code that might cause an error
except ExceptionType:
    # code to handle the error
```

### 🔸 Basic Example

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")

print("Program continues...")
```

Output:
```
Cannot divide by zero!
Program continues...
```

✔ Without `try-except`, the program would **crash** at `10 / 0`. With it, the error is **caught** and the program continues.

### 🔸 Step-by-Step Execution

1. Python enters the `try` block
2. `10 / 0` raises `ZeroDivisionError`
3. Python **jumps** to the matching `except` block
4. Prints "Cannot divide by zero!"
5. Program continues after the try-except block

### 🔸 When No Error Occurs

```python
try:
    result = 10 / 2
    print(f"Result: {result}")
except ZeroDivisionError:
    print("Cannot divide by zero!")
```

Output:
```
Result: 5.0
```

✔ If no error occurs, the `except` block is **skipped entirely**.

---

## 🔹 Catching Specific Exceptions

### 🔸 Multiple except Blocks

```python
try:
    num = int(input("Enter a number: "))
    result = 100 / num
    print(f"Result: {result}")
except ValueError:
    print("That's not a valid number!")
except ZeroDivisionError:
    print("Cannot divide by zero!")
```

✔ Python checks each `except` block **top to bottom** and runs the **first matching one**.

### 🔸 Catching Multiple Exceptions in One Block

```python
try:
    num = int(input("Enter a number: "))
    result = 100 / num
except (ValueError, ZeroDivisionError):
    print("Invalid input or division by zero!")
```

### 🔸 Catching ALL Exceptions (Use Carefully!)

```python
try:
    result = 10 / 0
except Exception:
    print("Something went wrong!")
```

⚠️ **Avoid bare `except:` or `except Exception:`** in production code — it hides bugs. Always catch **specific** exceptions when possible.

```python
# ❌ Bad — hides all errors
try:
    do_something()
except:
    pass

# ✅ Good — catch specific errors
try:
    do_something()
except ValueError:
    print("Invalid value")
except FileNotFoundError:
    print("File not found")
```

---

## 🔹 Getting the Error Message

### 🔸 Using `as` to Capture the Exception Object

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
    print(f"Type: {type(e)}")
```

Output:
```
Error: division by zero
Type: <class 'ZeroDivisionError'>
```

### 🔸 Practical Example

```python
try:
    num = int("hello")
except ValueError as e:
    print(f"Conversion failed: {e}")
```

Output:
```
Conversion failed: invalid literal for int() with base 10: 'hello'
```

---

## 🔹 The `else` Block

Runs **only if NO exception occurred** in the `try` block.

```python
try:
    num = int(input("Enter a number: "))
    result = 100 / num
except ValueError:
    print("Not a valid number!")
except ZeroDivisionError:
    print("Cannot divide by zero!")
else:
    print(f"Result: {result}")   # only runs if no error
```

### 🔸 Why Use `else`?

```python
# ❌ Without else — hard to tell what might fail
try:
    num = int(input("Enter: "))
    result = 100 / num
    print(f"Result: {result}")   # is this line protected or not?
except ValueError:
    print("Error")

# ✅ With else — clear separation
try:
    num = int(input("Enter: "))
    result = 100 / num
except ValueError:
    print("Error")
else:
    print(f"Result: {result}")   # clearly runs only on success
```

---

## 🔹 The `finally` Block (VERY IMPORTANT 🔥)

Runs **ALWAYS** — whether an exception occurred or not. Used for **cleanup**.

```python
try:
    f = open("data.txt", "r")
    content = f.read()
except FileNotFoundError:
    print("File not found!")
finally:
    print("This always runs!")
```

### 🔸 finally Runs Even After return

```python
def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"
    finally:
        print("Finally block executed!")

result = divide(10, 2)
print(result)
```

Output:
```
Finally block executed!
5.0
```

✔ `finally` runs **even if** the function returns from inside `try` or `except`.

### 🔸 Common Use: Closing Resources

```python
f = None
try:
    f = open("data.txt", "r")
    content = f.read()
except FileNotFoundError:
    print("File not found!")
finally:
    if f is not None:
        f.close()
        print("File closed")
```

✔ Better approach — use `with` statement (covered in File Handling).

---

## 🔹 Complete try-except-else-finally Flow

```python
try:
    # code that might fail
except SomeError:
    # handle the error
else:
    # runs ONLY if no error
finally:
    # ALWAYS runs (cleanup)
```

### 🔸 Flow Diagram

```
try block
    ├── Error occurs → except block → finally block
    └── No error → else block → finally block
```

### 🔸 Full Example

```python
def safe_divide(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        print("Error: Division by zero!")
        return None
    except TypeError:
        print("Error: Invalid types!")
        return None
    else:
        print(f"Success: {a} / {b} = {result}")
        return result
    finally:
        print("Operation complete.\n")

safe_divide(10, 2)
safe_divide(10, 0)
safe_divide("10", 2)
```

Output:
```
Success: 10 / 2 = 5.0
Operation complete.

Error: Division by zero!
Operation complete.

Error: Invalid types!
Operation complete.
```

---

## 🔹 Raising Exceptions — `raise` (IMPORTANT 🔥)

You can **manually raise** exceptions using `raise`.

### 🔸 Basic raise

```python
age = -5

if age < 0:
    raise ValueError("Age cannot be negative!")
```

Output:
```
ValueError: Age cannot be negative!
```

### 🔸 raise in a Function

```python
def set_age(age):
    if not isinstance(age, int):
        raise TypeError("Age must be an integer")
    if age < 0:
        raise ValueError("Age cannot be negative")
    if age > 150:
        raise ValueError("Age cannot be more than 150")
    return age

try:
    set_age(-5)
except ValueError as e:
    print(f"Error: {e}")   # Error: Age cannot be negative
```

### 🔸 Re-raising an Exception

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Logging the error...")
    raise   # re-raise the same exception
```

✔ `raise` without arguments re-raises the **current exception**. Useful for logging before letting the error propagate.

---

## 🔹 Custom Exceptions (INTERVIEW FAVORITE 🔥)

You can create your own exception classes by inheriting from `Exception`.

### 🔸 Basic Custom Exception

```python
class InsufficientFundsError(Exception):
    pass

def withdraw(balance, amount):
    if amount > balance:
        raise InsufficientFundsError(f"Cannot withdraw {amount}. Balance: {balance}")
    return balance - amount

try:
    new_balance = withdraw(100, 200)
except InsufficientFundsError as e:
    print(f"Error: {e}")
```

Output:
```
Error: Cannot withdraw 200. Balance: 100
```

### 🔸 Custom Exception with Extra Attributes

```python
class ValidationError(Exception):
    def __init__(self, field, message):
        self.field = field
        self.message = message
        super().__init__(f"{field}: {message}")

def validate_email(email):
    if "@" not in email:
        raise ValidationError("email", "Must contain @")
    if "." not in email.split("@")[1]:
        raise ValidationError("email", "Invalid domain")

try:
    validate_email("invalid-email")
except ValidationError as e:
    print(f"Validation failed — {e.field}: {e.message}")
```

### 🔸 Exception Hierarchy for a Project

```python
class AppError(Exception):
    """Base exception for our application"""
    pass

class DatabaseError(AppError):
    pass

class ConnectionError(DatabaseError):
    pass

class QueryError(DatabaseError):
    pass

class AuthError(AppError):
    pass

class LoginError(AuthError):
    pass

class PermissionError(AuthError):
    pass

# Now you can catch broadly or specifically
try:
    raise LoginError("Invalid credentials")
except AuthError as e:
    print(f"Auth issue: {e}")   # catches LoginError AND PermissionError
except AppError as e:
    print(f"App issue: {e}")    # catches everything else
```

---

## 🔹 Exception Chaining — `raise from`

```python
try:
    num = int("hello")
except ValueError as original:
    raise RuntimeError("Failed to process input") from original
```

Output:
```
ValueError: invalid literal for int() with base 10: 'hello'

The above exception was the direct cause of the following exception:

RuntimeError: Failed to process input
```

✔ `raise ... from ...` links the new exception to the original cause. Useful for debugging.

---

## 🔹 LBYL vs EAFP (INTERVIEW 🔥)

Two coding styles for handling potential errors:

### 🔸 LBYL — Look Before You Leap

Check **before** doing something.

```python
# Check first, then act
if "key" in my_dict:
    value = my_dict["key"]
else:
    value = "default"
```

### 🔸 EAFP — Easier to Ask Forgiveness than Permission

Just **do it** and handle the error if it happens.

```python
# Just try it, handle error if needed
try:
    value = my_dict["key"]
except KeyError:
    value = "default"
```

### 🔸 Which is Pythonic?

✔ **EAFP is the Pythonic way.** Python is optimized for the `try-except` pattern.

| Style | Approach | Pythonic? |
|-------|----------|:---------:|
| LBYL | Check first | ❌ (other languages) |
| EAFP | Try and handle | ✅ (Python way) |

---

## 🔹 The Exception Hierarchy

All exceptions inherit from `BaseException`:

```
BaseException
├── SystemExit
├── KeyboardInterrupt
├── GeneratorExit
└── Exception
    ├── ValueError
    ├── TypeError
    ├── KeyError
    ├── IndexError
    ├── FileNotFoundError
    ├── ZeroDivisionError
    ├── AttributeError
    ├── ImportError
    ├── OSError
    ├── RuntimeError
    ├── StopIteration
    └── ... (many more)
```

⚠️ **Always catch `Exception`, not `BaseException`:**

```python
# ❌ Bad — catches KeyboardInterrupt and SystemExit too!
try:
    do_something()
except BaseException:
    pass

# ✅ Good — lets Ctrl+C and sys.exit() work normally
try:
    do_something()
except Exception:
    pass
```

---

## 🔹 Assertions — `assert` (For Debugging)

`assert` checks a condition. If `False`, raises `AssertionError`.

```python
age = 25
assert age >= 0, "Age cannot be negative"   # passes silently

age = -5
assert age >= 0, "Age cannot be negative"   # ❌ AssertionError: Age cannot be negative
```

### 🔸 When to Use assert

```python
# ✅ Use for debugging and development checks
def calculate_average(numbers):
    assert len(numbers) > 0, "List cannot be empty"
    return sum(numbers) / len(numbers)

# ❌ Don't use for user input validation (can be disabled with -O flag)
# assert user_input > 0   # BAD — use raise ValueError instead
```

⚠️ Assertions can be **disabled** by running Python with `-O` (optimize) flag. Never use them for production validation.

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Bare except (Catches Everything)

```python
# ❌ Bad — hides all errors including typos
try:
    pritn("Hello")   # typo!
except:
    pass   # silently swallows the NameError

# ✅ Good — catch specific exceptions
try:
    print("Hello")
except NameError as e:
    print(f"Error: {e}")
```

### 🔸 Mistake 2: Too Much Code in try Block

```python
# ❌ Bad — hard to know which line caused the error
try:
    data = read_file()
    parsed = parse_data(data)
    result = process(parsed)
    save(result)
except Exception:
    print("Something failed")

# ✅ Good — narrow try blocks
try:
    data = read_file()
except FileNotFoundError:
    print("File not found")
else:
    parsed = parse_data(data)
    result = process(parsed)
    save(result)
```

### 🔸 Mistake 3: Using Exceptions for Flow Control

```python
# ❌ Bad — exceptions are for errors, not normal logic
try:
    value = my_list[index]
except IndexError:
    value = None

# ✅ Better — check first for expected conditions
if index < len(my_list):
    value = my_list[index]
else:
    value = None
```

⚠️ This contradicts EAFP slightly. The rule: use EAFP when the **error is unlikely**. Use LBYL when the **error is expected/common**.

### 🔸 Mistake 4: Catching and Ignoring

```python
# ❌ Worst practice — silently swallowing errors
try:
    important_operation()
except Exception:
    pass   # error disappears, good luck debugging!

# ✅ At minimum, log the error
import logging

try:
    important_operation()
except Exception as e:
    logging.error(f"Operation failed: {e}")

# ✅ Even better — logging.exception() captures the full stack trace automatically
try:
    important_operation()
except Exception:
    logging.exception("Operation failed")
    # This prints the error message AND the full traceback
    # without needing to import the traceback module
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Safe Division Function

```python
def safe_divide(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"
    except TypeError:
        return "Invalid types"
    else:
        return result

print(safe_divide(10, 2))      # 5.0
print(safe_divide(10, 0))      # Cannot divide by zero
print(safe_divide("10", 2))    # Invalid types
```

---

### ✅ 2. Safe Integer Input

```python
def get_integer(prompt):
    while True:
        try:
            return int(input(prompt))
        except ValueError:
            print("Please enter a valid integer!")

num = get_integer("Enter a number: ")
print(f"You entered: {num}")
```

---

### ✅ 3. File Reader with Error Handling

```python
def read_file(filename):
    try:
        f = open(filename, "r")
        content = f.read()
        return content
    except FileNotFoundError:
        return f"File '{filename}' not found"
    except PermissionError:
        return f"No permission to read '{filename}'"
    finally:
        try:
            f.close()
        except NameError:
            pass   # file was never opened

print(read_file("nonexistent.txt"))
```

---

### ✅ 4. Custom Exception — Age Validator

```python
class InvalidAgeError(Exception):
    def __init__(self, age, message="Invalid age"):
        self.age = age
        self.message = message
        super().__init__(f"{message}: {age}")

def validate_age(age):
    if not isinstance(age, int):
        raise TypeError("Age must be an integer")
    if age < 0 or age > 150:
        raise InvalidAgeError(age)
    return True

try:
    validate_age(200)
except InvalidAgeError as e:
    print(f"Error: {e}")          # Error: Invalid age: 200
    print(f"Age was: {e.age}")    # Age was: 200
except TypeError as e:
    print(f"Type error: {e}")
```

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| `try` | Code that might fail |
| `except` | Handle specific errors |
| `else` | Runs only if no error |
| `finally` | Always runs (cleanup) |
| `raise` | Manually raise an exception |
| `raise from` | Chain exceptions |
| `as e` | Capture exception object |
| Custom exceptions | Inherit from `Exception` |
| `assert` | Debug-time checks (can be disabled) |
| EAFP | Try first, handle error (Pythonic) |
| LBYL | Check first, then act |
| Exception hierarchy | `BaseException` → `Exception` → specific |
| Bare except | ❌ Avoid — hides bugs |
| `finally` + return | `finally` runs even after return |

---

> 🚀 **Next:** File Handling →
