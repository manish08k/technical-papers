# Python OOP – Countdown and Triangle

## 1. Countdown (Counter Class)
'''
class Counter:
    def __init__(self):
        self.value = 0

    def inc(self):
        self.value += 1

    def dec(self):
        self.value -= 1

    def incrn(self, n):
        self.value += n

    def decn(self, n):
        self.value -= n


c = Counter()
c.inc()
print(c.value)
c.incrn(5)
print(c.value)
'''

## 2. Triangle and Point

```python
import math


class Triangle:
    def __init__(self):
        self.points = []

    def add_point(self, x, y):
        self.points.append((x, y))

    def perimeter(self):
        a = self.points[0]
        b = self.points[1]
        c = self.points[2]

        side1 = math.dist(a, b)
        side2 = math.dist(b, c)
        side3 = math.dist(c, a)

        return side1 + side2 + side3

    def __eq__(self, other):
        return self.points == other.points


t1 = Triangle()
t1.add_point(0, 0)
t1.add_point(0, 3)
t1.add_point(4, 0)

t2 = Triangle()
t2.add_point(1, 2)
t2.add_point(2, 1)
t2.add_point(1, 5)

t3 = Triangle()
t3.add_point(1, 2)
t3.add_point(2, 1)
t3.add_point(1, 5)

print(t1.perimeter())
print(t2.perimeter())

print(t1 == t2)
print(t1 == t3)
```

##  Expected Output

```text
12.0
10.06449510224598
False
True
```


## 3.  OOPs

OOPs has four main pillars:

1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

---

## 3.1 Encapsulation

**Meaning:** Wrapping variables and methods together inside a class. It also helps protect data from direct access.

### Code Example

```python
class Bank:
    def __init__(self):
        self.__balance = 1000

    def deposit(self, amount):
        self.__balance += amount

    def show_balance(self):
        print(self.__balance)


b = Bank()

b.deposit(500)
b.show_balance()
```

### Output

```text
1500
```

### Explanation

- `Bank` is a class.
- `__balance` is a private-style variable.
- `deposit()` adds money.
- `show_balance()` displays the balance.

---

## 3.2 Inheritance

**Meaning:** One class can acquire the properties and methods of another class.

It helps with code reusability.

### Code Example

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    def bark(self):
        print("Dog is barking")


d = Dog()

d.eat()
d.bark()
```

### Output

```text
Animal is eating
Dog is barking
```

### Explanation

- `Animal` is the parent class.
- `Dog` is the child class.
- `Dog` inherits the `eat()` method from `Animal`.

---

## 3.3 Polymorphism

**Meaning:** One method name can have different behaviors depending on the object.

### Code Example

```python
class Dog:
    def sound(self):
        print("Dog barks")


class Cat:
    def sound(self):
        print("Cat meows")


d = Dog()
c = Cat()

d.sound()
c.sound()
```

### Output

```text
Dog barks
Cat meows
```

### Explanation

Both classes have the same method name `sound()`, but they perform different actions.

---

## 3.4 Abstraction

**Meaning:** Hiding implementation details and showing only essential functionality.

In Python, we can implement abstraction using the `abc` module.

### Code Example

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


d = Dog()
c = Cat()

d.sound()
c.sound()
```

### Output

```text
Dog barks
Cat meows
```

### Explanation

- `ABC` is used to create an abstract class.
- `@abstractmethod` defines a method that child classes must implement.
- `Animal` cannot be instantiated directly because it has an abstract method.
- `Dog` and `Cat` provide their own implementations.

---

## 4. Quick Comparison of Four Pillars

| OOP Concept | Meaning | Main Purpose |
|---|---|---|
| Encapsulation | Wrapping data and methods together | Data protection |
| Inheritance | Acquiring properties from another class | Code reusability |
| Polymorphism | Same interface, different behavior | Flexibility |
| Abstraction | Hiding implementation details | Simplicity |

---

## 5. Additional OOP Concepts


### 5.1 Method Overriding

When a child class provides its own implementation of a method already defined in the parent class.

```python
class Animal:
    def sound(self):
        print("Animal makes sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


d = Dog()
d.sound()
```

Output:

```text
Dog barks
```

### 5.2 Method Overloading

Method overloading means using the same method name with different parameters.

Python does not support traditional method overloading directly, but we can achieve similar behavior using default arguments.

```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c


c = Calculator()

print(c.add(10))
print(c.add(10, 20))
print(c.add(10, 20, 30))
```

Output:

```text
10
30
60
```

