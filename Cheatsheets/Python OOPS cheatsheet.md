Python OOPSPython OOPS
# Python OOP (Object-Oriented Programming) Cheatsheet

## 1. What is OOP?

OOP stands for Object-Oriented Programming.

It is a programming approach based on **classes and objects**.

Main OOP concepts:
1. Class
2. Object
3. Encapsulation
4. Inheritance
5. Polymorphism
6. Abstraction

## 2. Class and Object

```python
# Class
class Student:
    name = "Manish"
    age = 21

    def display(self):
        print(self.name, self.age)


# Object
s1 = Student()

# Access attributes
print(s1.name)
print(s1.age)

# Call method
s1.display()
```

- **Class:** Blueprint for creating objects.
- **Object:** Instance of a class.
- **self:** Refers to the current object.

## 3. Constructor (`__init__`)

The constructor initializes an object's attributes when it is created.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(self.name, self.age)


s1 = Student("Manish", 21)
s2 = Student("Rahul", 22)

s1.display()
s2.display()
```

## 4. Instance Variables and Class Variables

```python
class Student:
    # Class variable
    college = "JNTUH"

    def __init__(self, name, age):
        # Instance variables
        self.name = name
        self.age = age


s1 = Student("Manish", 21)
s2 = Student("Rahul", 22)

# Instance variables
print(s1.name)
print(s2.name)

# Class variable
print(s1.college)
print(Student.college)
```

- **Instance variable:** Different for each object.
- **Class variable:** Shared by instances unless overridden.

## 5. Instance Methods

Instance methods work with object-specific data.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


s1 = Student("Manish")
s1.display()
```

## 6. Class Methods

Class methods work with class-level data.

Use `@classmethod`.

```python
class Student:
    college = "JNTUH"

    @classmethod
    def change_college(cls, name):
        cls.college = name


Student.change_college("IIT Hyderabad")

print(Student.college)
```

- `cls` refers to the class.
- `@classmethod` defines a class method.

## 7. Static Methods

Static methods do not require `self` or `cls`.

Use `@staticmethod`.

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

## 8. Types of Methods

| Method | First Parameter | Decorator |
|---|---|---|
| Instance method | `self` | None |
| Class method | `cls` | `@classmethod` |
| Static method | None | `@staticmethod` |

---

# Four Pillars of OOP

## 9. Encapsulation

Encapsulation means combining data and methods inside a class and controlling access to the data.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def get_balance(self):
        return self.__balance


account = BankAccount(1000)

account.deposit(500)

print(account.get_balance())

# Direct access is name-mangled
# print(account.__balance)  # AttributeError
```

### Access Modifiers in Python

```python
class Student:
    def __init__(self):
        self.name = "Manish"       # Public
        self._age = 21             # Protected convention
        self.__salary = 50000      # Private name-mangled
```

| Type | Syntax | Meaning |
|---|---|---|
| Public | `name` | Accessible normally |
| Protected | `_name` | Internal-use convention |
| Private | `__name` | Name mangling |

**Note:** Python does not enforce strict private or protected access.

## 10. Inheritance

Inheritance allows one class to acquire properties and methods from another class.

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


d = Dog()

d.eat()
d.bark()
```

### Types of Inheritance

**1. Single Inheritance**

```python
class Parent:
    def display(self):
        print("Parent")


class Child(Parent):
    pass


obj = Child()
obj.display()
```

**2. Multilevel Inheritance**

```python
class Grandparent:
    def display(self):
        print("Grandparent")


class Parent(Grandparent):
    pass


class Child(Parent):
    pass


obj = Child()
obj.display()
```

**3. Multiple Inheritance**

```python
class Father:
    def father_method(self):
        print("Father")


class Mother:
    def mother_method(self):
        print("Mother")


class Child(Father, Mother):
    pass


obj = Child()
obj.father_method()
obj.mother_method()
```

**4. Hierarchical Inheritance**

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    pass


class Cat(Animal):
    pass


Dog().eat()
Cat().eat()
```

**5. Hybrid Inheritance**

Combination of two or more inheritance types.

```python
class A:
    def display(self):
        print("A")


class B(A):
    pass


class C(A):
    pass


class D(B, C):
    pass


obj = D()
obj.display()
```

## 11. `super()` Function

`super()` is used to access methods from a parent class.

```python
class Parent:
    def __init__(self, name):
        self.name = name

    def display(self):
        print("Parent method")


class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age

    def display(self):
        super().display()
        print(self.name, self.age)


obj = Child("Manish", 21)
obj.display()
```

## 12. Method Overriding

When a child class provides its own implementation of a parent method, it is called method overriding.

```python
class Animal:
    def sound(self):
        print("Animal sound")


class Dog(Animal):
    def sound(self):
        print("Bark")


obj = Dog()
obj.sound()
```

## 13. Polymorphism

Polymorphism means one interface can have different implementations.

```python
class Dog:
    def sound(self):
        print("Bark")


class Cat:
    def sound(self):
        print("Meow")


def make_sound(animal):
    animal.sound()


make_sound(Dog())
make_sound(Cat())
```

### Duck Typing

Python focuses on whether an object supports the required behavior rather than its exact type.

```python
class Bird:
    def fly(self):
        print("Flying")


class Airplane:
    def fly(self):
        print("Airplane flying")


def start_flying(obj):
    obj.fly()


start_flying(Bird())
start_flying(Airplane())
```

### Method Overloading

Python does not support traditional method overloading by defining multiple methods with the same name.

Use default arguments or variable-length arguments instead.

```python
class Calculator:
    def add(self, a, b, c=0):
        return a + b + c


obj = Calculator()

print(obj.add(10, 20))
print(obj.add(10, 20, 30))
```

## 14. Abstraction

Abstraction hides implementation details and exposes essential functionality.

Use the `abc` module.

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass


class Dog(Animal):
    def sound(self):
        print("Bark")


obj = Dog()
obj.sound()
```

- `ABC`: Base class for abstract classes.
- `@abstractmethod`: Declares an abstract method.
- Abstract classes cannot be instantiated while abstract methods remain unimplemented.

---

# Special Methods (Dunder Methods)

## 15. Common Dunder Methods

Dunder means double underscore.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Student: {self.name}"

    def __repr__(self):
        return f"Student('{self.name}')"

    def __len__(self):
        return len(self.name)

    def __eq__(self, other):
        if not isinstance(other, Student):
            return NotImplemented
        return self.name == other.name


s1 = Student("Manish")
s2 = Student("Manish")

print(s1)
print(repr(s1))
print(len(s1))
print(s1 == s2)
```

## 16. Operator Overloading

Define how operators behave for your custom objects.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(
            self.x + other.x,
            self.y + other.y
        )

    def __str__(self):
        return f"({self.x}, {self.y})"


p1 = Point(2, 3)
p2 = Point(4, 5)

p3 = p1 + p2

print(p3)
```

### Important Dunder Methods

| Method | Purpose |
|---|---|
| `__init__` | Initialize object |
| `__new__` | Create object |
| `__str__` | User-friendly string |
| `__repr__` | Developer representation |
| `__len__` | Length |
| `__eq__` | Equality (`==`) |
| `__lt__` | Less than (`<`) |
| `__gt__` | Greater than (`>`) |
| `__add__` | Addition (`+`) |
| `__sub__` | Subtraction (`-`) |
| `__mul__` | Multiplication (`*`) |
| `__getitem__` | Indexing (`[]`) |
| `__setitem__` | Assign indexed value |
| `__contains__` | Membership (`in`) |
| `__call__` | Call object like a function |
| `__iter__` | Create iterator |
| `__next__` | Get next iterator value |
| `__enter__` | Context manager entry |
| `__exit__` | Context manager exit |

---

# Advanced OOP Concepts

## 17. Property Decorator

Use `@property` to access a method like an attribute.

```python
class Student:
    def __init__(self, marks):
        self._marks = marks

    @property
    def marks(self):
        return self._marks

    @marks.setter
    def marks(self, value):
        if value < 0:
            raise ValueError("Marks cannot be negative")
        self._marks = value


s = Student(90)

print(s.marks)

s.marks = 95
print(s.marks)
```

## 18. Composition

Composition means one class contains an object of another class.

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
        print("Car started")


car = Car()
car.start()
```

## 19. Aggregation

Aggregation is a relationship where one object uses another object, but the contained object can exist independently.

```python
class Teacher:
    def teach(self):
        print("Teaching")


class School:
    def __init__(self, teacher):
        self.teacher = teacher


teacher = Teacher()
school = School(teacher)

school.teacher.teach()
```

## 20. Association

Association means two independent objects are connected or interact with each other.

```python
class Student:
    def study(self):
        print("Student studying")


class Teacher:
    def teach(self, student):
        student.study()


student = Student()
teacher = Teacher()

teacher.teach(student)
```

## 21. Class Attributes vs Instance Attributes

```python
class Employee:
    company = "HIGHH"  # Class attribute

    def __init__(self, name):
        self.name = name  # Instance attribute


e1 = Employee("Manish")
e2 = Employee("Rahul")

print(e1.company)
print(e2.company)

e1.name = "John"
print(e1.name)
print(e2.name)
```

## 22. `isinstance()` and `issubclass()`

```python
class Animal:
    pass


class Dog(Animal):
    pass


d = Dog()

# Check object's type
print(isinstance(d, Dog))

# Check inheritance relationship
print(isinstance(d, Animal))

# Check whether one class inherits another
print(issubclass(Dog, Animal))
```

## 23. Method Resolution Order (MRO)

MRO determines the order in which Python searches for methods in inheritance.

```python
class A:
    def show(self):
        print("A")


class B(A):
    def show(self):
        print("B")


class C(A):
    def show(self):
        print("C")


class D(B, C):
    pass


obj = D()
obj.show()

# View method resolution order
print(D.mro())
print(D.__mro__)
```

## 24. `__slots__`

`__slots__` restricts which instance attributes can be created and can reduce memory usage.

```python
class Student:
    __slots__ = ("name", "age")

    def __init__(self, name, age):
        self.name = name
        self.age = age


s = Student("Manish", 21)

print(s.name)

# s.city = "Bangalore"  # AttributeError
```

## 25. Dataclasses

Dataclasses automatically generate common methods such as `__init__` and `__repr__`.

```python
from dataclasses import dataclass


@dataclass
class Student:
    name: str
    age: int
    marks: float


s = Student("Manish", 21, 90.5)

print(s)
print(s.name)
```

## 26. Enum

Enums define a fixed set of named constants.

```python
from enum import Enum


class Status(Enum):
    PENDING = 1
    APPROVED = 2
    REJECTED = 3


print(Status.PENDING)
print(Status.PENDING.name)
print(Status.PENDING.value)
```

## 27. Singleton Pattern

Singleton ensures that a class has only one shared instance.

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance


a = Singleton()
b = Singleton()

print(a is b)  # True
```

---

# OOP Design Principles

## 28. SOLID Principles

| Principle | Meaning |
|---|---|
| S - Single Responsibility | One class should have one main responsibility |
| O - Open/Closed | Open for extension, closed for modification |
| L - Liskov Substitution | Child objects should work wherever parent objects are expected |
| I - Interface Segregation | Prefer smaller, focused interfaces |
| D - Dependency Inversion | Depend on abstractions, not concrete implementations |

## 29. DRY, KISS and YAGNI

- **DRY:** Don't Repeat Yourself.
- **KISS:** Keep It Simple, Stupid.
- **YAGNI:** You Aren't Gonna Need It.

## 30. Inheritance vs Composition

| Inheritance | Composition |
|---|---|
| IS-A relationship | HAS-A relationship |
| Child inherits parent behavior | Class contains another object |
| Creates a parent-child hierarchy | Combines independent objects |
| Can create tight coupling | Often provides more flexibility |

---

# Common Interview Questions

## 31. Class vs Object

| Class | Object |
|---|---|
| Blueprint | Instance |
| Defines attributes and methods | Uses attributes and methods |
| Logical definition | Actual instance |
| `class Student:` | `s = Student()` |

## 32. Encapsulation vs Abstraction

| Encapsulation | Abstraction |
|---|---|
| Bundles data and methods | Hides implementation details |
| Controls access to data | Exposes essential functionality |
| Uses access conventions and properties | Uses ABC and abstract methods |

## 33. Overloading vs Overriding

| Overloading | Overriding |
|---|---|
| Same method name with different signatures | Child redefines parent method |
| Traditional signature-based overloading is not built in | Supported through inheritance |
| Use defaults or `*args` in Python | Define method in child class |

## 34. `self` vs `cls`

| self | cls |
|---|---|
| Refers to current object | Refers to current class |
| Used in instance methods | Used in class methods |
| Accesses instance attributes | Accesses class attributes |

## 35. `__new__` vs `__init__`

| `__new__` | `__init__` |
|---|---|
| Creates object | Initializes object |
| Runs before `__init__` | Runs after `__new__` |
| Usually returns an instance | Usually returns `None` |

---

# Practical OOP Example

## 36. Bank Account System

```python
class BankAccount:

    bank_name = "HIGHH Bank"

    def __init__(self, account_holder, balance=0):
        self.account_holder = account_holder
        self.__balance = balance

    def deposit(self, amount):
        if amount <= 0:
            print("Invalid amount")
            return

        self.__balance += amount
        print(f"Deposited: {amount}")

    def withdraw(self, amount):
        if amount <= 0:
            print("Invalid amount")
        elif amount > self.__balance:
            print("Insufficient balance")
        else:
            self.__balance -= amount
            print(f"Withdrawn: {amount}")

    def get_balance(self):
        return self.__balance

    def display(self):
        print("Bank:", self.bank_name)
        print("Account Holder:", self.account_holder)
        print("Balance:", self.__balance)


account = BankAccount("Manish", 10000)

account.deposit(5000)
account.withdraw(2000)

account.display()
```

---

# Quick Reference

## 37. OOP Syntax

| Concept | Syntax |
|---|---|
| Class | `class Student:` |
| Object | `s = Student()` |
| Constructor | `def __init__(self):` |
| Instance method | `def display(self):` |
| Class method | `@classmethod` |
| Static method | `@staticmethod` |
| Inheritance | `class Child(Parent):` |
| Parent method | `super().method()` |
| Encapsulation | `self.__value` |
| Property | `@property` |
| Setter | `@value.setter` |
| Abstraction | `from abc import ABC, abstractmethod` |
| Abstract method | `@abstractmethod` |
| Method overriding | Redefine parent method |
| Operator overloading | `def __add__(self, other):` |
| Type checking | `isinstance(obj, Class)` |
| Inheritance checking | `issubclass(Child, Parent)` |
| MRO | `Class.mro()` |
| Dataclass | `@dataclass` |
| Enum | `class Status(Enum):` |

## 38. Four Pillars - One-Line Revision

1. **Encapsulation:** Protect and control access to data.
2. **Inheritance:** Reuse properties and methods from another class.
3. **Polymorphism:** Same interface, different behavior.
4. **Abstraction:** Hide implementation and expose essential functionality.
