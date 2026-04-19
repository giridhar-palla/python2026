# 🏗️ OOP in Python — Advanced (Zero to Hero)

> Building on the basics: Composition, Dunder Methods, Dataclasses, `__slots__`, Design Patterns, and Interview Programs.

---

## 🔹 Composition vs Inheritance (VERY IMPORTANT 🔥)

### 🔸 Inheritance = "IS-A" Relationship

```python
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):   # Dog IS-A Animal
    def bark(self):
        print("Woof!")
```

### 🔸 Composition = "HAS-A" Relationship

Instead of inheriting, a class **contains** another class as an attribute.

```python
class Engine:
    def __init__(self, horsepower):
        self.horsepower = horsepower

    def start(self):
        print(f"Engine with {self.horsepower}HP started")

class Car:
    def __init__(self, brand, horsepower):
        self.brand = brand
        self.engine = Engine(horsepower)   # Car HAS-A Engine

    def drive(self):
        self.engine.start()
        print(f"{self.brand} is driving")

car = Car("Toyota", 150)
car.drive()
```

Output:
```
Engine with 150HP started
Toyota is driving
```

🧠 `Car` doesn't inherit from `Engine`. It **contains** an `Engine` object. This is composition.

### 🔸 When to Use Which?

| | Inheritance (IS-A) | Composition (HAS-A) |
|---|---|---|
| Relationship | Dog IS-A Animal | Car HAS-A Engine |
| Coupling | Tight (child depends on parent) | Loose (objects are independent) |
| Flexibility | Less flexible | More flexible |
| Code reuse | Through parent class | Through contained objects |
| When to use | True "is-a" relationship | Most other cases |

✔ **Prefer composition over inheritance** in most cases. This is a common interview answer.

### 🔸 Real-World Example: Employee System

```python
class Address:
    def __init__(self, street, city, state):
        self.street = street
        self.city = city
        self.state = state

    def __str__(self):
        return f"{self.street}, {self.city}, {self.state}"

class Department:
    def __init__(self, name, floor):
        self.name = name
        self.floor = floor

    def __str__(self):
        return f"{self.name} (Floor {self.floor})"

class Employee:
    def __init__(self, name, salary, address, department):
        self.name = name
        self.salary = salary
        self.address = address         # HAS-A Address
        self.department = department   # HAS-A Department

    def __str__(self):
        return f"{self.name} | {self.department} | {self.address}"

addr = Address("123 Main St", "Hyderabad", "Telangana")
dept = Department("Engineering", 3)
emp = Employee("Giridhar", 50000, addr, dept)

print(emp)
# Giridhar | Engineering (Floor 3) | 123 Main St, Hyderabad, Telangana
```

---

## 🔹 More Dunder (Magic) Methods

### 🔸 `__getitem__` and `__setitem__` — Make Object Subscriptable

```python
class Playlist:
    def __init__(self):
        self.songs = []

    def add(self, song):
        self.songs.append(song)

    def __getitem__(self, index):
        return self.songs[index]

    def __setitem__(self, index, value):
        self.songs[index] = value

    def __len__(self):
        # __len__ must return an integer
        return len(self.songs)

    def __str__(self):
        return str(self.songs)

playlist = Playlist()
playlist.add("Song A")
playlist.add("Song B")
playlist.add("Song C")

print(playlist[0])      # Song A  (uses __getitem__)
playlist[1] = "Song X"  # uses __setitem__
print(playlist)          # ['Song A', 'Song X', 'Song C']
print(len(playlist))     # 3
```

### 🔸 `__contains__` — Support `in` Operator

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __contains__(self, song):
        return song in self.songs

playlist = Playlist(["Song A", "Song B", "Song C"])

print("Song A" in playlist)   # True
print("Song Z" in playlist)   # False
```

### 🔸 `__iter__` and `__next__` — Make Object Iterable

```python
class Countdown:
    def __init__(self, start):
        self.start = start

    def __iter__(self):
        self.current = self.start
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        value = self.current
        self.current = self.current - 1
        return value

for num in Countdown(5):
    print(num, end=" ")
```

Output:
```
5 4 3 2 1
```

### 🔸 `__call__` — Make Object Callable Like a Function

```python
class Multiplier:
    def __init__(self, factor):
        self.factor = factor

    def __call__(self, value):
        return value * self.factor

double = Multiplier(2)
triple = Multiplier(3)

print(double(5))    # 10  (calling object like a function!)
print(triple(5))    # 15
print(callable(double))  # True
```

### 🔸 `__hash__` and `__eq__` — For Sets and Dict Keys

For an object to be used in a `set` or as a `dict` key, it needs both `__hash__` and `__eq__`.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    def __hash__(self):
        return hash((self.x, self.y))

    def __repr__(self):
        return f"Point({self.x}, {self.y})"

# Now Points can be in sets
points = {Point(1, 2), Point(3, 4), Point(1, 2)}
print(points)   # {Point(1, 2), Point(3, 4)}  ← duplicate removed!

# And as dict keys
distances = {Point(0, 0): "origin", Point(1, 1): "diagonal"}
print(distances[Point(0, 0)])   # origin
```

### 🔸 `__new__` vs `__init__` — Object Creation (SENIOR INTERVIEW 🔥)

Most developers only know `__init__`. But `__new__` is what **actually creates** the object.

| Method | Purpose | Called |
|--------|---------|-------|
| `__new__` | **Creates** the object (allocates memory) | First |
| `__init__` | **Initializes** the object (sets attributes) | Second |

```python
class MyClass:
    def __new__(cls, *args, **kwargs):
        print("1. __new__ called — creating object")
        instance = super().__new__(cls)
        return instance   # MUST return the instance

    def __init__(self, name):
        print("2. __init__ called — initializing object")
        self.name = name

obj = MyClass("Python")
```

Output:
```
1. __new__ called — creating object
2. __init__ called — initializing object
```

#### Singleton Pattern Using `__new__`

A **Singleton** ensures only **one instance** of a class ever exists.

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            print("Creating the one and only instance")
            cls._instance = super().__new__(cls)
        return cls._instance

s1 = Singleton()   # Creating the one and only instance
s2 = Singleton()   # (no print — reuses existing instance)

print(s1 is s2)   # True  ← same object!
```

🧠 `__new__` checks if an instance already exists. If yes, it returns the existing one instead of creating a new one.

✔ You rarely need to override `__new__` in everyday code. It's mainly used for **Singletons**, **immutable types**, and **metaclasses**.

### 🔸 Context Manager: `__enter__` and `__exit__`

Used with the `with` statement for automatic cleanup.

```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()
        print("File closed automatically")

with FileManager("test.txt", "w") as f:
    f.write("Hello, World!")
# File closed automatically  ← __exit__ called automatically
```

### 🔸 All Common Dunder Methods — Reference Table

| Method | Triggered By | Purpose |
|--------|-------------|---------|
| `__init__` | `obj = Class()` | Constructor |
| `__del__` | `del obj` / garbage collection | Destructor |
| `__str__` | `print(obj)`, `str(obj)` | Human-readable string |
| `__repr__` | `repr(obj)`, interactive shell | Developer-readable string |
| `__len__` | `len(obj)` | Length (must return int) |
| `__getitem__` | `obj[key]` | Get item by index/key |
| `__setitem__` | `obj[key] = val` | Set item by index/key |
| `__delitem__` | `del obj[key]` | Delete item |
| `__contains__` | `x in obj` | Membership test |
| `__iter__` | `for x in obj` | Make iterable |
| `__next__` | `next(obj)` | Get next item |
| `__call__` | `obj()` | Make callable |
| `__eq__` | `obj == other` | Equality |
| `__ne__` | `obj != other` | Not equal |
| `__lt__` | `obj < other` | Less than |
| `__gt__` | `obj > other` | Greater than |
| `__le__` | `obj <= other` | Less or equal |
| `__ge__` | `obj >= other` | Greater or equal |
| `__add__` | `obj + other` | Addition |
| `__sub__` | `obj - other` | Subtraction |
| `__mul__` | `obj * other` | Multiplication |
| `__hash__` | `hash(obj)` | Hash value |
| `__bool__` | `bool(obj)`, `if obj:` | Truthiness |
| `__enter__` | `with obj:` | Context manager enter |
| `__exit__` | End of `with` block | Context manager exit |

---

## 🔹 Dataclasses (Python 3.7+) — IMPORTANT 🔥

Dataclasses **automatically generate** `__init__`, `__repr__`, `__eq__`, and more.

### 🔸 The Problem: Boilerplate Code

```python
# Without dataclass — lots of repetitive code
class Person:
    def __init__(self, name, age, city):
        self.name = name
        self.age = age
        self.city = city

    def __repr__(self):
        return f"Person(name='{self.name}', age={self.age}, city='{self.city}')"

    def __eq__(self, other):
        return self.name == other.name and self.age == other.age and self.city == other.city
```

### 🔸 The Solution: `@dataclass`

```python
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int
    city: str

p1 = Person("Giridhar", 25, "Hyderabad")
p2 = Person("Giridhar", 25, "Hyderabad")

print(p1)          # Person(name='Giridhar', age=25, city='Hyderabad')  ← auto __repr__
print(p1 == p2)    # True  ← auto __eq__
print(p1.name)     # Giridhar
```

✔ `@dataclass` auto-generates `__init__`, `__repr__`, and `__eq__` from the field definitions.

### 🔸 Default Values

```python
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int
    city: str = "Unknown"   # default value

p = Person("Giridhar", 25)
print(p)   # Person(name='Giridhar', age=25, city='Unknown')
```

⚠️ Fields with defaults must come **after** fields without defaults (same rule as function parameters).

### 🔸 Frozen Dataclass (Immutable)

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class Point:
    x: float
    y: float

p = Point(1.0, 2.0)
p.x = 3.0   # ❌ FrozenInstanceError: cannot assign to field 'x'
```

✔ `frozen=True` makes the dataclass **immutable** — like a tuple but with named fields.

### 🔸 Ordering with Dataclasses

```python
from dataclasses import dataclass

@dataclass(order=True)
class Student:
    grade: float
    name: str

students = [
    Student(3.5, "Alice"),
    Student(3.8, "Bob"),
    Student(3.2, "Charlie")
]

students.sort()
for s in students:
    print(s)
```

Output:
```
Student(grade=3.2, name='Charlie')
Student(grade=3.5, name='Alice')
Student(grade=3.8, name='Bob')
```

✔ `order=True` auto-generates `__lt__`, `__le__`, `__gt__`, `__ge__` based on field order.

### 🔸 field() for Advanced Configuration

```python
from dataclasses import dataclass, field

@dataclass
class Student:
    name: str
    grades: list = field(default_factory=list)   # safe mutable default!

s1 = Student("Alice")
s2 = Student("Bob")

s1.grades.append(90)
print(s1.grades)   # [90]
print(s2.grades)   # []  ← independent! (no shared reference bug)
```

✔ `field(default_factory=list)` creates a **new list for each instance** — avoids the mutable default trap.

### 🔸 Post-Init Processing

```python
from dataclasses import dataclass

@dataclass
class Rectangle:
    width: float
    height: float
    area: float = 0

    def __post_init__(self):
        self.area = self.width * self.height

r = Rectangle(5, 3)
print(r)   # Rectangle(width=5, height=3, area=15)
```

### 🔸 Dataclass vs Regular Class vs NamedTuple

| Feature | Regular Class | `@dataclass` | `NamedTuple` |
|---------|:---:|:---:|:---:|
| Auto `__init__` | ❌ | ✅ | ✅ |
| Auto `__repr__` | ❌ | ✅ | ✅ |
| Auto `__eq__` | ❌ | ✅ | ✅ |
| Mutable | ✅ | ✅ (default) | ❌ |
| Can add methods | ✅ | ✅ | ✅ |
| Inheritance | ✅ | ✅ | Limited |
| Default values | ✅ | ✅ | ✅ |
| Type hints | Optional | Required | Required |

---

## 🔹 `__slots__` — Memory Optimization

By default, Python stores instance attributes in a `__dict__` dictionary. `__slots__` replaces this with a fixed structure.

### 🔸 Without `__slots__` (Default)

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

p = Point(1, 2)
print(p.__dict__)   # {'x': 1, 'y': 2}

# Can add new attributes dynamically
p.z = 3   # ✅ works
```

### 🔸 With `__slots__`

```python
class Point:
    __slots__ = ('x', 'y')

    def __init__(self, x, y):
        self.x = x
        self.y = y

p = Point(1, 2)
# print(p.__dict__)   # ❌ AttributeError: 'Point' has no attribute '__dict__'

# Cannot add new attributes
p.z = 3   # ❌ AttributeError: 'Point' object has no attribute 'z'
```

### 🔸 Why Use `__slots__`?

```python
import sys

class PointDict:
    def __init__(self, x, y):
        self.x = x
        self.y = y

class PointSlots:
    __slots__ = ('x', 'y')
    def __init__(self, x, y):
        self.x = x
        self.y = y

p1 = PointDict(1, 2)
p2 = PointSlots(1, 2)

print(sys.getsizeof(p1.__dict__) + sys.getsizeof(p1))  # ~200 bytes
print(sys.getsizeof(p2))                                 # ~56 bytes
```

| | Without `__slots__` | With `__slots__` |
|---|---|---|
| Memory | More (has `__dict__`) | Less (no `__dict__`) |
| Dynamic attributes | ✅ Can add any | ❌ Only declared ones |
| Speed | Slightly slower | Slightly faster |
| Use when | Flexibility needed | Many instances, memory matters |

---

## 🔹 Mixins — Reusable Behavior Without Full Inheritance

A mixin is a small class that provides **specific behavior** to be mixed into other classes.

```python
class JsonMixin:
    def to_json(self):
        import json
        return json.dumps(self.__dict__)

class LogMixin:
    def log(self, message):
        print(f"[{self.__class__.__name__}] {message}")

class User(JsonMixin, LogMixin):
    def __init__(self, name, email):
        self.name = name
        self.email = email

user = User("Giridhar", "giri@email.com")
print(user.to_json())   # {"name": "Giridhar", "email": "giri@email.com"}
user.log("User created")  # [User] User created
```

✔ Mixins add **specific capabilities** without creating deep inheritance hierarchies.

---

## 🔹 Common Mistakes ⚠️

### 🔸 Mistake 1: Mutable Class Variable Shared Across Instances

```python
class Student:
    grades = []   # ❌ shared by ALL instances!

    def add_grade(self, grade):
        self.grades.append(grade)

s1 = Student()
s2 = Student()

s1.add_grade(90)
print(s2.grades)   # [90]  ← s2 also affected!

# ✅ Fix: use instance variable
class Student:
    def __init__(self):
        self.grades = []   # unique per instance
```

### 🔸 Mistake 2: Forgetting `super().__init__()`

```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        # ❌ Forgot super().__init__()
        self.breed = breed

dog = Dog("Buddy", "Labrador")
print(dog.name)   # ❌ AttributeError: 'Dog' has no attribute 'name'

# ✅ Fix
class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```

### 🔸 Mistake 3: Confusing `__str__` and `__repr__`

```python
class Person:
    def __init__(self, name):
        self.name = name

p = Person("Giridhar")
print(p)   # <__main__.Person object at 0x...>  ← ugly!

# ✅ Define __repr__ at minimum
class Person:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"Person('{self.name}')"
```

### 🔸 Mistake 4: Using `isinstance()` Instead of Duck Typing

```python
# ❌ Over-checking types (not Pythonic)
def process(obj):
    if isinstance(obj, Dog):
        obj.bark()
    elif isinstance(obj, Cat):
        obj.meow()

# ✅ Pythonic — duck typing
def process(obj):
    obj.speak()   # just call the method, trust the object
```

---

## 🔹 Interview Programs 💡

### ✅ 1. Bank Account System

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance   # private

    @property
    def balance(self):
        return self.__balance

    def deposit(self, amount):
        if amount <= 0:
            print("Deposit amount must be positive")
            return
        self.__balance = self.__balance + amount
        print(f"Deposited {amount}. Balance: {self.__balance}")

    def withdraw(self, amount):
        if amount <= 0:
            print("Withdrawal amount must be positive")
            return
        if amount > self.__balance:
            print("Insufficient funds!")
            return
        self.__balance = self.__balance - amount
        print(f"Withdrew {amount}. Balance: {self.__balance}")

    def __str__(self):
        return f"Account({self.owner}, Balance: {self.__balance})"

acc = BankAccount("Giridhar", 1000)
acc.deposit(500)      # Deposited 500. Balance: 1500
acc.withdraw(200)     # Withdrew 200. Balance: 1300
acc.withdraw(2000)    # Insufficient funds!
print(acc)            # Account(Giridhar, Balance: 1300)
```

---

### ✅ 2. Shape Hierarchy (Inheritance + Abstraction)

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

    def __str__(self):
        return f"{self.__class__.__name__}: Area={self.area():.2f}, Perimeter={self.perimeter():.2f}"

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

    def perimeter(self):
        return 2 * 3.14159 * self.radius

class Triangle(Shape):
    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c

    def area(self):
        s = (self.a + self.b + self.c) / 2
        return (s * (s - self.a) * (s - self.b) * (s - self.c)) ** 0.5

    def perimeter(self):
        return self.a + self.b + self.c

shapes = [Rectangle(5, 3), Circle(7), Triangle(3, 4, 5)]

for shape in shapes:
    print(shape)
```

Output:
```
Rectangle: Area=15.00, Perimeter=16.00
Circle: Area=153.94, Perimeter=43.98
Triangle: Area=6.00, Perimeter=12.00
```

---

### ✅ 3. Employee Management (Composition)

```python
class Department:
    def __init__(self, name):
        self.name = name
        self.employees = []

    def add_employee(self, employee):
        self.employees.append(employee)

    def total_salary(self):
        total = 0
        for emp in self.employees:
            total = total + emp.salary
        return total

    def __str__(self):
        return f"Department({self.name}, {len(self.employees)} employees)"

class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def __repr__(self):
        return f"Employee('{self.name}', {self.salary})"

dept = Department("Engineering")
dept.add_employee(Employee("Alice", 60000))
dept.add_employee(Employee("Bob", 55000))
dept.add_employee(Employee("Charlie", 70000))

print(dept)                    # Department(Engineering, 3 employees)
print(f"Total: {dept.total_salary()}")  # Total: 185000
print(dept.employees)          # [Employee('Alice', 60000), ...]
```

---

### ✅ 4. Custom Stack (Dunder Methods)

```python
class Stack:
    def __init__(self):
        self.__items = []

    def push(self, item):
        self.__items.append(item)

    def pop(self):
        if len(self.__items) == 0:
            raise IndexError("Stack is empty")
        return self.__items.pop()

    def peek(self):
        if len(self.__items) == 0:
            raise IndexError("Stack is empty")
        return self.__items[-1]

    def __len__(self):
        return len(self.__items)

    def __bool__(self):
        return len(self.__items) > 0

    def __str__(self):
        return f"Stack({self.__items})"

    def __repr__(self):
        return f"Stack({self.__items})"

    def __contains__(self, item):
        return item in self.__items

stack = Stack()
stack.push(10)
stack.push(20)
stack.push(30)

print(stack)           # Stack([10, 20, 30])
print(len(stack))      # 3
print(20 in stack)     # True
print(stack.peek())    # 30
print(stack.pop())     # 30
print(stack)           # Stack([10, 20])

if stack:
    print("Stack is not empty")
```

---

### ✅ 5. Linked List Node (Classic Interview)

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

    def __repr__(self):
        return f"Node({self.data})"

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            return
        current = self.head
        while current.next is not None:
            current = current.next
        current.next = new_node

    def display(self):
        current = self.head
        items = []
        while current is not None:
            items.append(str(current.data))
            current = current.next
        print(" -> ".join(items) + " -> None")

    def __len__(self):
        count = 0
        current = self.head
        while current is not None:
            count = count + 1
            current = current.next
        return count

    def __contains__(self, data):
        current = self.head
        while current is not None:
            if current.data == data:
                return True
            current = current.next
        return False

ll = LinkedList()
ll.append(10)
ll.append(20)
ll.append(30)

ll.display()          # 10 -> 20 -> 30 -> None
print(len(ll))        # 3
print(20 in ll)       # True
print(99 in ll)       # False
```

---

## 🔹 Interview Questions — Conceptual 💡

### Q1: What are the 4 pillars of OOP?
**Answer:** Encapsulation, Inheritance, Polymorphism, Abstraction.

### Q2: What is the difference between a class and an object?
**Answer:** A class is a blueprint/template. An object is an actual instance created from that class.

### Q3: What is the difference between `__str__` and `__repr__`?
**Answer:** `__str__` is for human-readable output (`print()`). `__repr__` is for developer-readable output (`repr()`). If only one is defined, define `__repr__`.

### Q4: Does Python support method overloading?
**Answer:** No. Python doesn't support traditional method overloading. The last definition overwrites previous ones. Use default parameters or `*args` as workarounds.

### Q5: What is the Diamond Problem?
**Answer:** When a class inherits from two classes that share a common parent, there's ambiguity about which parent's method to use. Python solves this with MRO (C3 Linearization).

### Q6: What is duck typing?
**Answer:** Python doesn't check the type of an object — it checks if the object has the required method. "If it walks like a duck and quacks like a duck, it's a duck."

### Q7: What is the difference between composition and inheritance?
**Answer:** Inheritance = "is-a" (Dog is-a Animal). Composition = "has-a" (Car has-a Engine). Prefer composition for flexibility.

### Q8: What is `@property` used for?
**Answer:** It lets you define getter/setter methods that look like attribute access. Provides validation while keeping clean syntax.

### Q9: What is `__slots__`?
**Answer:** Replaces the instance `__dict__` with a fixed structure. Saves memory and prevents dynamic attribute creation.

### Q10: What is an abstract class?
**Answer:** A class that cannot be instantiated and forces child classes to implement specific methods. Created using `ABC` and `@abstractmethod`.

### Q11: Can you have a mutable object inside an immutable tuple?
**Answer:** Yes. The tuple holds a reference to the object. The reference can't change, but the object itself can be modified if it's mutable (e.g., a list inside a tuple).

### Q12: What is a mixin?
**Answer:** A small class that provides specific reusable behavior. It's mixed into other classes via multiple inheritance without being a standalone base class.

---

## 🔹 Complete OOP Summary 📌

| Concept | Description |
|---------|-------------|
| Class | Blueprint for objects |
| Object | Instance of a class |
| `__init__` | Constructor |
| `self` | Reference to current object |
| Instance variable | Unique per object (`self.x`) |
| Class variable | Shared by all objects |
| Instance method | Uses `self`, accesses instance data |
| `@classmethod` | Uses `cls`, factory methods |
| `@staticmethod` | No `self`/`cls`, utility functions |
| Encapsulation | `_protected`, `__private`, `@property` |
| Inheritance | `class Child(Parent)`, `super()` |
| Method Overriding | Child redefines parent's method |
| Method Overloading | Not supported — use defaults / `*args` |
| Operator Overloading | `__add__`, `__eq__`, `__lt__`, etc. |
| Polymorphism | Same method, different behavior |
| Duck Typing | Check behavior, not type |
| Abstraction | `ABC`, `@abstractmethod` |
| MRO | Diamond Problem resolution order |
| Composition | "Has-a" — prefer over inheritance |
| Dataclasses | Auto `__init__`, `__repr__`, `__eq__` |
| `__slots__` | Memory optimization, no `__dict__` |
| Mixins | Reusable behavior via multiple inheritance |
| Dunder methods | `__str__`, `__repr__`, `__len__`, `__getitem__`, etc. |

---

> 🚀 **What's Next?**
> 👉 Exception Handling
> 👉 File Handling
> 👉 Decorators & Generators
