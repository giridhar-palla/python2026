# 🏗️ OOP in Python — Basics (Zero to Hero)

> Object-Oriented Programming (OOP) is a way of organizing code around **objects** that combine data and behavior.

---

## 🔹 What is OOP?

OOP is a programming paradigm where you model real-world things as **objects** that have:
- **Attributes** (data / properties) — what the object **has**
- **Methods** (functions) — what the object **does**

### 🧠 Real-World Analogy

> 👉 Think of a **Car**:
> - **Attributes:** color, brand, speed, fuel level
> - **Methods:** start(), accelerate(), brake(), honk()
>
> Every car has the same **blueprint** (class), but each car is a **different object** (instance) with its own color, speed, etc.

---

## 🔹 Class vs Object

| Concept | Meaning | Analogy |
|---------|---------|---------|
| **Class** | A blueprint / template | House blueprint |
| **Object** | An actual instance created from the class | The actual house |

- You write the class **once**
- You create **many objects** from it

---

## 🔹 Creating a Class

### Syntax:

```python
class ClassName:
    # attributes and methods
    pass
```

### 🔸 Simplest Class

```python
class Car:
    pass

# Creating objects (instances)
car1 = Car()
car2 = Car()

print(type(car1))   # <class '__main__.Car'>
print(car1)          # <__main__.Car object at 0x...>

# They are different objects
print(car1 is car2)  # False
```

---

## 🔹 The `__init__()` Method (Constructor)

The **constructor** is a special method that runs **automatically** when you create an object. It initializes the object's attributes.

```python
class Car:
    def __init__(self, brand, color, speed):
        self.brand = brand
        self.color = color
        self.speed = speed

# Creating objects
car1 = Car("Toyota", "Red", 120)
car2 = Car("Honda", "Blue", 100)

print(car1.brand)   # Toyota
print(car2.color)   # Blue
```

### 🔸 What Happens Step by Step?

1. `Car("Toyota", "Red", 120)` is called
2. Python creates a **new empty object**
3. Python calls `__init__(self, "Toyota", "Red", 120)`
4. `self` refers to the **new object being created**
5. `self.brand = "Toyota"` stores "Toyota" in the object
6. The object is returned and assigned to `car1`

---

## 🔹 The `self` Keyword (VERY IMPORTANT 🔥)

`self` refers to the **current object** (the instance calling the method).

```python
class Dog:
    def __init__(self, name, age):
        self.name = name   # self.name = attribute of THIS object
        self.age = age

    def bark(self):
        print(f"{self.name} says Woof!")

dog1 = Dog("Buddy", 3)
dog2 = Dog("Max", 5)

dog1.bark()   # Buddy says Woof!
dog2.bark()   # Max says Woof!
```

🧠 When you call `dog1.bark()`, Python internally calls `Dog.bark(dog1)`. So `self` = `dog1`.

### 🔸 Common Mistake: Forgetting `self`

```python
class Dog:
    def __init__(self, name):
        self.name = name

    # ❌ Forgot self parameter
    def bark():
        print("Woof!")

dog = Dog("Buddy")
dog.bark()   # ❌ TypeError: bark() takes 0 positional arguments but 1 was given

# ✅ Correct
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(f"{self.name} says Woof!")
```

### 🔸 `self` is NOT a Keyword

`self` is just a **convention**. You could name it anything, but **always use `self`**.

```python
# ✅ Works but DON'T do this
class Dog:
    def __init__(xyz, name):
        xyz.name = name

# ✅ Always use self
class Dog:
    def __init__(self, name):
        self.name = name
```

---

## 🔹 Instance Variables vs Class Variables (INTERVIEW FAVORITE 🔥)

### 🔸 Instance Variables — Unique to Each Object

```python
class Dog:
    def __init__(self, name, age):
        self.name = name   # instance variable
        self.age = age     # instance variable

dog1 = Dog("Buddy", 3)
dog2 = Dog("Max", 5)

print(dog1.name)   # Buddy
print(dog2.name)   # Max  (different for each object)
```

### 🔸 Class Variables — Shared by ALL Objects

```python
class Dog:
    species = "Canine"   # class variable (shared)

    def __init__(self, name):
        self.name = name   # instance variable (unique)

dog1 = Dog("Buddy")
dog2 = Dog("Max")

print(dog1.species)   # Canine
print(dog2.species)   # Canine  (same for all)
print(Dog.species)    # Canine  (accessed via class too)
```

### 🔸 Modifying Class Variables — Be Careful! ⚠️

```python
class Dog:
    count = 0   # class variable

    def __init__(self, name):
        self.name = name
        Dog.count += 1   # modify via CLASS name

dog1 = Dog("Buddy")
dog2 = Dog("Max")
dog3 = Dog("Rex")

print(Dog.count)   # 3
```

⚠️ **Trap:** If you modify via instance, it creates a NEW instance variable:

```python
class Dog:
    species = "Canine"

dog1 = Dog()
dog1.species = "Feline"   # creates instance variable, doesn't change class variable!

print(dog1.species)   # Feline  (instance variable)
print(Dog.species)    # Canine  (class variable unchanged)
```

### 🔸 Summary

| | Instance Variable | Class Variable |
|---|---|---|
| Defined in | `__init__` with `self.` | Directly in class body |
| Unique per object? | ✅ Yes | ❌ No (shared) |
| Access via | `self.var` or `obj.var` | `ClassName.var` |
| Common use | Object-specific data | Shared counters, constants |

---

## 🔹 Methods — Three Types

### 🔸 1. Instance Methods (Most Common)

- First parameter is `self`
- Can access and modify instance variables
- Can access class variables

```python
class Circle:
    pi = 3.14159   # class variable

    def __init__(self, radius):
        self.radius = radius   # instance variable

    def area(self):   # instance method
        return Circle.pi * self.radius ** 2

    def circumference(self):
        return 2 * Circle.pi * self.radius

c = Circle(5)
print(c.area())            # 78.53975
print(c.circumference())   # 31.4159
```

### 🔸 2. Class Methods (`@classmethod`)

- First parameter is `cls` (the class itself, not an instance)
- Can access and modify **class variables**
- Cannot access instance variables
- Often used as **factory methods** (alternative constructors)

```python
class Person:
    count = 0

    def __init__(self, name, age):
        self.name = name
        self.age = age
        Person.count += 1

    @classmethod
    def get_count(cls):
        return cls.count

    @classmethod
    def from_string(cls, data_string):
        name, age = data_string.split("-")
        return cls(name, int(age))

# Normal creation
p1 = Person("Giridhar", 25)

# Factory method — alternative way to create
p2 = Person.from_string("Ravi-30")

print(p2.name)              # Ravi
print(p2.age)               # 30
print(Person.get_count())   # 2
```

🧠 **Constructor Overloading:** Python doesn't support multiple `__init__` methods. Use `@classmethod` as factory methods instead.

```python
class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    @classmethod
    def from_string(cls, date_string):
        year, month, day = date_string.split("-")
        return cls(int(year), int(month), int(day))

    @classmethod
    def today(cls):
        import datetime
        t = datetime.date.today()
        return cls(t.year, t.month, t.day)

d1 = Date(2025, 4, 19)
d2 = Date.from_string("2025-04-19")
d3 = Date.today()
```

### 🔸 3. Static Methods (`@staticmethod`)

- No `self` or `cls` parameter
- Cannot access instance or class variables
- Just a regular function that lives inside the class
- Used for utility/helper functions related to the class

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def is_even(n):
        return n % 2 == 0

print(MathUtils.add(3, 4))      # 7
print(MathUtils.is_even(10))    # True
```

### 🔸 Comparison: Instance vs Class vs Static

| | Instance Method | Class Method | Static Method |
|---|:---:|:---:|:---:|
| First param | `self` | `cls` | None |
| Access instance vars? | ✅ | ❌ | ❌ |
| Access class vars? | ✅ | ✅ | ❌ |
| Decorator | None | `@classmethod` | `@staticmethod` |
| Called on | Object or Class | Class (usually) | Class (usually) |
| Common use | Object behavior | Factory methods | Utility functions |

---

## 🔹 Encapsulation (PILLAR 1 🔥)

Encapsulation means **hiding internal data** and controlling access through methods.

### 🔸 Access Modifiers in Python

| Convention | Syntax | Meaning |
|-----------|--------|---------|
| Public | `self.name` | Accessible from anywhere |
| Protected | `self._name` | "Please don't access directly" (convention only) |
| Private | `self.__name` | Name-mangled, harder to access |

### 🔸 Public (Default)

```python
class Person:
    def __init__(self, name, age):
        self.name = name   # public
        self.age = age     # public

p = Person("Giridhar", 25)
print(p.name)   # Giridhar  ✅ accessible
p.name = "Ravi"  # ✅ can modify
```

### 🔸 Protected (Single Underscore `_`)

```python
class Person:
    def __init__(self, name, age):
        self._name = name   # protected (convention)
        self._age = age

p = Person("Giridhar", 25)
print(p._name)   # Giridhar  ✅ still accessible (just a convention!)
```

⚠️ Python does **NOT enforce** protected access. The underscore is just a signal to other developers: "Don't touch this directly."

### 🔸 Private (Double Underscore `__`)

```python
class Person:
    def __init__(self, name, age):
        self.__name = name   # private
        self.__age = age

p = Person("Giridhar", 25)
print(p.__name)   # ❌ AttributeError: 'Person' object has no attribute '__name'
```

🧠 Python uses **name mangling** — it renames `__name` to `_Person__name`:

```python
print(p._Person__name)   # Giridhar  ✅ (but don't do this!)
```

### 🔸 Getters and Setters (Manual Way)

```python
class Person:
    def __init__(self, name, age):
        self.__name = name
        self.__age = age

    def get_name(self):
        return self.__name

    def set_name(self, name):
        if not isinstance(name, str):
            raise ValueError("Name must be a string")
        self.__name = name

    def get_age(self):
        return self.__age

    def set_age(self, age):
        if age < 0:
            raise ValueError("Age cannot be negative")
        self.__age = age

p = Person("Giridhar", 25)
print(p.get_name())   # Giridhar
p.set_age(26)
print(p.get_age())    # 26
p.set_age(-5)         # ❌ ValueError: Age cannot be negative
```

### 🔸 `@property` Decorator (Pythonic Way ✅)

```python
class Person:
    def __init__(self, name, age):
        self.__name = name
        self.__age = age

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        if not isinstance(value, str):
            raise ValueError("Name must be a string")
        self.__name = value

    @property
    def age(self):
        return self.__age

    @age.setter
    def age(self, value):
        if value < 0:
            raise ValueError("Age cannot be negative")
        self.__age = value

p = Person("Giridhar", 25)

# Looks like attribute access, but calls the property methods!
print(p.name)   # Giridhar  (calls getter)
p.name = "Ravi"  # calls setter
print(p.name)   # Ravi

p.age = -5   # ❌ ValueError: Age cannot be negative
```

✔ `@property` lets you use **attribute syntax** (`p.name`) while still having **validation logic** behind the scenes.

### 🔸 Read-Only Property

```python
class Circle:
    def __init__(self, radius):
        self.__radius = radius

    @property
    def radius(self):
        return self.__radius

    @property
    def area(self):
        return 3.14159 * self.__radius ** 2

c = Circle(5)
print(c.radius)   # 5
print(c.area)     # 78.53975

c.radius = 10   # ❌ AttributeError: can't set attribute (no setter defined)
```

---

## 🔹 Inheritance (PILLAR 2 🔥)

Inheritance lets a **child class** reuse code from a **parent class**.

### 🧠 Real-World Analogy

> 👉 A **Dog** is an **Animal**. It inherits all animal properties (name, age, eat, sleep) and adds its own (bark, fetch).

### 🔸 Basic Inheritance

```python
# Parent class
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def eat(self):
        print(f"{self.name} is eating")

    def sleep(self):
        print(f"{self.name} is sleeping")

# Child class
class Dog(Animal):
    def bark(self):
        print(f"{self.name} says Woof!")

# Child class
class Cat(Animal):
    def meow(self):
        print(f"{self.name} says Meow!")

dog = Dog("Buddy", 3)
dog.eat()    # Buddy is eating  (inherited from Animal)
dog.bark()   # Buddy says Woof! (own method)

cat = Cat("Whiskers", 2)
cat.eat()    # Whiskers is eating  (inherited)
cat.meow()   # Whiskers says Meow! (own method)
```

### 🔸 `super()` — Call Parent's Method

```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Dog(Animal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)   # call parent's __init__
        self.breed = breed            # add own attribute

dog = Dog("Buddy", 3, "Labrador")
print(dog.name)    # Buddy
print(dog.breed)   # Labrador
```

🧠 `super()` gives you access to the **parent class**. Without it, you'd have to repeat the parent's code.

### 🔸 Method Overriding (VERY IMPORTANT 🔥)

A child class can **redefine** a method from the parent class.

```python
class Animal:
    def speak(self):
        print("Some generic sound")

class Dog(Animal):
    def speak(self):   # overrides parent's speak()
        print("Woof!")

class Cat(Animal):
    def speak(self):   # overrides parent's speak()
        print("Meow!")

animal = Animal()
dog = Dog()
cat = Cat()

animal.speak()   # Some generic sound
dog.speak()      # Woof!   (overridden)
cat.speak()      # Meow!   (overridden)
```

### 🔸 Calling Parent's Method After Overriding

```python
class Animal:
    def speak(self):
        print("Some generic sound")

class Dog(Animal):
    def speak(self):
        super().speak()          # call parent's version first
        print("...and also Woof!")

dog = Dog()
dog.speak()
```

Output:
```
Some generic sound
...and also Woof!
```

### 🔸 Types of Inheritance

#### 1. Single Inheritance

```python
class Parent:
    pass

class Child(Parent):
    pass
```

#### 2. Multilevel Inheritance

```python
class Grandparent:
    pass

class Parent(Grandparent):
    pass

class Child(Parent):
    pass
```

#### 3. Multiple Inheritance

```python
class Father:
    def skill(self):
        print("Coding")

class Mother:
    def skill(self):
        print("Painting")

class Child(Father, Mother):
    pass

child = Child()
child.skill()   # Coding  (Father comes first in MRO)
```

#### 4. Hierarchical Inheritance

```python
class Animal:
    pass

class Dog(Animal):
    pass

class Cat(Animal):
    pass
```

### 🔸 Method Resolution Order (MRO) — The Diamond Problem (INTERVIEW 🔥)

When multiple parents have the same method, Python uses **MRO** to decide which one to call. This situation is commonly known as the **"Diamond Problem"** — a term interviewers specifically use.

🧠 **The Diamond Problem:** When class D inherits from B and C, and both B and C inherit from A, which version of A's method does D get? Python solves this with MRO.

```python
class A:
    def greet(self):
        print("A")

class B(A):
    def greet(self):
        print("B")

class C(A):
    def greet(self):
        print("C")

class D(B, C):
    pass

d = D()
d.greet()   # B

# Check MRO
print(D.__mro__)
# (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)
```

✔ Python uses the **C3 Linearization** algorithm. The order is: `D → B → C → A → object`.

### 🔸 `isinstance()` and `issubclass()`

```python
class Animal:
    pass

class Dog(Animal):
    pass

dog = Dog()

print(isinstance(dog, Dog))      # True
print(isinstance(dog, Animal))   # True  (Dog IS an Animal)
print(isinstance(dog, object))   # True  (everything inherits from object)

print(issubclass(Dog, Animal))   # True
print(issubclass(Animal, Dog))   # False
```

---

## 🔹 Polymorphism (PILLAR 3 🔥)

Polymorphism means **"many forms"** — the same method name behaves differently depending on the object.

### 🔸 Method Overriding (Already Covered Above)

```python
class Animal:
    def speak(self):
        print("Generic sound")

class Dog(Animal):
    def speak(self):
        print("Woof!")

class Cat(Animal):
    def speak(self):
        print("Meow!")

# Same method name, different behavior
animals = [Dog(), Cat(), Animal()]

for animal in animals:
    animal.speak()
```

Output:
```
Woof!
Meow!
Generic sound
```

### 🔸 Method Overloading — Python Doesn't Support It Directly!

In Java/C++, you can have multiple methods with the same name but different parameters. **Python does NOT support this.**

```python
# ❌ In Python, the LAST definition wins
class Calculator:
    def add(self, a, b):
        return a + b

    def add(self, a, b, c):   # this REPLACES the previous add()
        return a + b + c

calc = Calculator()
# calc.add(1, 2)      # ❌ TypeError: add() missing 1 required argument
calc.add(1, 2, 3)     # 6  (only this works)
```

### 🔸 Workaround 1: Default Parameters

```python
class Calculator:
    def add(self, a, b, c=0):
        return a + b + c

calc = Calculator()
print(calc.add(1, 2))      # 3
print(calc.add(1, 2, 3))   # 6
```

### 🔸 Workaround 2: *args

```python
class Calculator:
    def add(self, *args):
        total = 0
        for num in args:
            total = total + num
        return total

calc = Calculator()
print(calc.add(1, 2))         # 3
print(calc.add(1, 2, 3))      # 6
print(calc.add(1, 2, 3, 4))   # 10
```

### 🔸 Duck Typing (Python's Way of Polymorphism)

> "If it walks like a duck and quacks like a duck, it's a duck."

Python doesn't care about the **type** — it cares about the **behavior** (methods).

```python
class Duck:
    def speak(self):
        print("Quack!")

class Person:
    def speak(self):
        print("Hello!")

class Car:
    def speak(self):
        print("Vroom!")

# All have speak() — Python doesn't care about the type
things = [Duck(), Person(), Car()]

for thing in things:
    thing.speak()
```

Output:
```
Quack!
Hello!
Vroom!
```

✔ No inheritance needed. As long as the object has the method, Python will call it.

---

## 🔹 Operator Overloading (VERY IMPORTANT 🔥)

You can define how operators (`+`, `-`, `==`, `<`, etc.) work with your custom objects using **dunder methods**.

### 🔸 The Problem

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

p1 = Point(1, 2)
p2 = Point(3, 4)

print(p1 + p2)   # ❌ TypeError: unsupported operand type(s) for +
```

### 🔸 The Solution: `__add__`

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"Point({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)

p3 = p1 + p2   # calls p1.__add__(p2)
print(p3)       # Point(4, 6)
```

### 🔸 Common Operator Overloading Methods

| Operator | Method | Example |
|:--------:|--------|---------|
| `+` | `__add__(self, other)` | `a + b` |
| `-` | `__sub__(self, other)` | `a - b` |
| `*` | `__mul__(self, other)` | `a * b` |
| `/` | `__truediv__(self, other)` | `a / b` |
| `//` | `__floordiv__(self, other)` | `a // b` |
| `%` | `__mod__(self, other)` | `a % b` |
| `**` | `__pow__(self, other)` | `a ** b` |
| `==` | `__eq__(self, other)` | `a == b` |
| `!=` | `__ne__(self, other)` | `a != b` |
| `<` | `__lt__(self, other)` | `a < b` |
| `>` | `__gt__(self, other)` | `a > b` |
| `<=` | `__le__(self, other)` | `a <= b` |
| `>=` | `__ge__(self, other)` | `a >= b` |
| `len()` | `__len__(self)` | `len(a)` |
| `str()` | `__str__(self)` | `print(a)` |
| `repr()` | `__repr__(self)` | `repr(a)` |
| `[]` | `__getitem__(self, key)` | `a[0]` |
| `in` | `__contains__(self, item)` | `x in a` |
| `bool()` | `__bool__(self)` | `if a:` |

### 🔸 Full Example: Vector Class

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)

    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    def __lt__(self, other):
        return (self.x ** 2 + self.y ** 2) < (other.x ** 2 + other.y ** 2)

    def __len__(self):
        # __len__ MUST return an integer in Python, otherwise TypeError
        return int((self.x ** 2 + self.y ** 2) ** 0.5)

    def __str__(self):
        return f"Vector({self.x}, {self.y})"

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(3, 4)
v2 = Vector(1, 2)

print(v1 + v2)      # Vector(4, 6)
print(v1 - v2)      # Vector(2, 2)
print(v1 * 3)       # Vector(9, 12)
print(v1 == v2)     # False
print(v1 == Vector(3, 4))  # True
print(len(v1))      # 5  (magnitude)
print(v1 < v2)      # False
```

### 🔸 `__str__` vs `__repr__` (INTERVIEW 🔥)

| Method | Purpose | Called By |
|--------|---------|----------|
| `__str__` | Human-readable string | `print()`, `str()` |
| `__repr__` | Developer-readable string | `repr()`, interactive shell |

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, age {self.age}"

    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

p = Person("Giridhar", 25)

print(str(p))    # Giridhar, age 25     (human-friendly)
print(repr(p))   # Person('Giridhar', 25)  (developer-friendly, can recreate object)
```

✔ If only one is defined, define `__repr__`. Python falls back to `__repr__` when `__str__` is missing, but not vice versa.

### 🔸 `__del__` — Destructor (Brief Mention)

The counterpart to `__init__`. Called when an object is about to be **garbage collected**.

```python
class File:
    def __init__(self, name):
        self.name = name
        print(f"File {self.name} opened")

    def __del__(self):
        print(f"File {self.name} closed (destructor called)")

f = File("data.txt")   # File data.txt opened
del f                   # File data.txt closed (destructor called)
```

⚠️ **Don't rely on `__del__`** in real code. Python's garbage collector decides *when* to call it, and it may not run immediately. Use **context managers** (`with` statement) instead for cleanup.

---

## 🔹 Abstraction (PILLAR 4 🔥)

Abstraction means **hiding complex implementation** and showing only the essential features.

### 🔸 Abstract Classes — Using `ABC` Module

An abstract class **cannot be instantiated**. It forces child classes to implement certain methods.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

# ❌ Cannot create instance of abstract class
# shape = Shape()   # TypeError: Can't instantiate abstract class

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

rect = Rectangle(5, 3)
print(rect.area())        # 15
print(rect.perimeter())   # 16

circle = Circle(7)
print(circle.area())      # 153.93791
```

### 🔸 What Happens If You Don't Implement All Abstract Methods?

```python
class Triangle(Shape):
    def area(self):
        return 0
    # forgot perimeter()!

# ❌ TypeError: Can't instantiate abstract class Triangle
# with abstract method perimeter
t = Triangle()
```

✔ Abstract classes **enforce** that child classes implement all required methods.

---

## 🔹 The 4 Pillars — Summary

| Pillar | Meaning | Python Feature |
|--------|---------|---------------|
| **Encapsulation** | Hide data, control access | `_`, `__`, `@property` |
| **Inheritance** | Reuse code from parent class | `class Child(Parent)` |
| **Polymorphism** | Same method, different behavior | Method overriding, duck typing |
| **Abstraction** | Hide complexity, show essentials | `ABC`, `@abstractmethod` |

---

> 🚀 **Next:** OOP Advanced (Composition, Dataclasses, `__slots__`, more dunder methods, interview programs) →
