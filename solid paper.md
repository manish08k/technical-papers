# SOLID Principles in Python

SOLID is a set of five principles used in Object-Oriented Programming (OOP) to write clean, reusable, and maintainable code.

SOLID stands for:

1. S – Single Responsibility Principle
2. O – Open/Closed Principle
3. L – Liskov Substitution Principle
4. I – Interface Segregation Principle
5. D – Dependency Inversion Principle

## 1. Single Responsibility Principle (SRP)

**Meaning:** A class should have only one responsibility (one main job).

Example:

```python
class Student:
    def get_details(self):
        print("Getting student details")


class Marks:
    def calculate_marks(self):
        print("Calculating marks")


class Database:
    def save_data(self):
        print("Saving data")


s = Student()
m = Marks()
d = Database()

s.get_details()
m.calculate_marks()
d.save_data()
```

Output:

```text
Getting student details
Calculating marks
Saving data
```

**Explanation:** Each class performs only one job.

## 2. Open/Closed Principle (OCP)

**Meaning:** A class should be open for extension but closed for modification.

In simple words, we should be able to add new functionality without changing existing code.

Example:

```python
class Payment:
    def pay(self):
        pass


class UPI(Payment):
    def pay(self):
        print("Payment through UPI")


class Card(Payment):
    def pay(self):
        print("Payment through Card")


p1 = UPI()
p2 = Card()

p1.pay()
p2.pay()
```

Output:

```text
Payment through UPI
Payment through Card
```

**Explanation:** We can add new payment methods by creating new classes without modifying existing payment classes.

## 3. Liskov Substitution Principle (LSP)

**Meaning:** A child class should be usable wherever its parent class is expected without breaking the program.

Example:

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


def animal_eat(animal):
    animal.eat()


d = Dog()
c = Cat()

animal_eat(d)
animal_eat(c)
```

Output:

```text
Animal is eating
Animal is eating
```

**Explanation:** Both Dog and Cat can replace Animal because they support its inherited `eat()` behavior.

## 4. Interface Segregation Principle (ISP)

**Meaning:** A class should not be forced to implement methods it does not need.

Example:

```python
class Printer:
    def print_document(self):
        pass


class Scanner:
    def scan_document(self):
        pass


class BasicPrinter(Printer):
    def print_document(self):
        print("Printing document")


class MultiFunctionPrinter(Printer, Scanner):
    def print_document(self):
        print("Printing document")

    def scan_document(self):
        print("Scanning document")


p = BasicPrinter()
m = MultiFunctionPrinter()

p.print_document()

m.print_document()
m.scan_document()
```

Output:

```text
Printing document
Printing document
Scanning document
```

**Explanation:** BasicPrinter only needs printing, while MultiFunctionPrinter supports printing and scanning.

## 5. Dependency Inversion Principle (DIP)

**Meaning:** Classes should depend on abstractions rather than directly depending on specific classes.

Example:

```python
class Email:
    def send(self):
        print("Sending email")


class SMS:
    def send(self):
        print("Sending SMS")


class Notification:
    def __init__(self, service):
        self.service = service

    def notify(self):
        self.service.send()


e = Email()
s = SMS()

n1 = Notification(e)
n2 = Notification(s)

n1.notify()
n2.notify()
```

Output:

```text
Sending email
Sending SMS
``
