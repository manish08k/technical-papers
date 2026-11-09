
# Python SOLID Principles Cheatsheet

## 1. What is SOLID?

SOLID is a set of five object-oriented design principles that help developers write clean, maintainable, reusable, and scalable code.

| Letter | Principle | Meaning |
|---|---|---|
| S | Single Responsibility Principle | One class, one responsibility |
| O | Open/Closed Principle | Open for extension, closed for modification |
| L | Liskov Substitution Principle | Child classes should replace parent classes |
| I | Interface Segregation Principle | Prefer small, specific interfaces |
| D | Dependency Inversion Principle | Depend on abstractions, not concrete classes |

---

## 2. S — Single Responsibility Principle (SRP)

**Definition:** A class should have only one responsibility and one reason to change.

### Bad Example

One class handles user data, database operations, and email notifications.

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def save_to_database(self):
        print("Saving user to database")

    def send_email(self):
        print("Sending email")
```

### Good Example

Separate responsibilities into different classes.

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email


class UserRepository:
    def save(self, user):
        print("Saving user to database")


class EmailService:
    def send_email(self, user):
        print(f"Sending email to {user.email}")


user = User("Manish", "manish@example.com")

repository = UserRepository()
email_service = EmailService()

repository.save(user)
email_service.send_email(user)
```

**Remember:** One class should have one main responsibility.

---

## 3. O — Open/Closed Principle (OCP)

**Definition:** Software entities should be open for extension but closed for modification.

You should be able to add new functionality without changing existing working code.

### Bad Example

Every new payment method requires modifying the existing class.

```python
class Payment:
    def pay(self, payment_type, amount):
        if payment_type == "upi":
            print(f"Paying {amount} using UPI")

        elif payment_type == "card":
            print(f"Paying {amount} using Card")
```

### Good Example

Use separate classes with a common interface.

```python
from abc import ABC, abstractmethod


class PaymentMethod(ABC):

    @abstractmethod
    def pay(self, amount):
        pass


class UPIPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Paying {amount} using UPI")


class CardPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Paying {amount} using Card")


class PaymentProcessor:
    def process(self, payment, amount):
        payment.pay(amount)


processor = PaymentProcessor()

processor.process(UPIPayment(), 1000)
processor.process(CardPayment(), 2000)
```

To add a new payment method, create another class without modifying `PaymentProcessor`.

**Remember:** Extend behavior without changing existing code.

---

## 4. L — Liskov Substitution Principle (LSP)

**Definition:** Objects of a child class should be usable wherever objects of the parent class are expected without breaking the program's expected behavior.

### Bad Example

A square inherits from a rectangle, but changing its width or height independently violates the expected rectangle behavior.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def set_width(self, width):
        self.width = width

    def set_height(self, height):
        self.height = height

    def area(self):
        return self.width * self.height


class Square(Rectangle):
    def set_width(self, width):
        self.width = width
        self.height = width

    def set_height(self, height):
        self.width = height
        self.height = height


def calculate_area(rectangle):
    rectangle.set_width(5)
    rectangle.set_height(10)
    return rectangle.area()


print(calculate_area(Rectangle(0, 0)))  # 50
print(calculate_area(Square(0, 0)))     # 100
```

The square changes the expected behavior of the rectangle.

### Good Example

Use separate abstractions for shapes.

```python
from abc import ABC, abstractmethod


class Shape(ABC):

    @abstractmethod
    def area(self):
        pass


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height


class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side * self.side


def calculate_area(shape):
    return shape.area()


print(calculate_area(Rectangle(5, 10)))
print(calculate_area(Square(5)))
```

**Remember:** A child class should not break the behavior expected from its parent abstraction.

---

## 5. I — Interface Segregation Principle (ISP)

**Definition:** A class should not be forced to implement methods it does not need.

Prefer smaller, specific interfaces instead of one large interface.

### Bad Example

A basic printer is forced to implement scanning and faxing.

```python
from abc import ABC, abstractmethod


class Machine(ABC):

    @abstractmethod
    def print_document(self):
        pass

    @abstractmethod
    def scan_document(self):
        pass

    @abstractmethod
    def fax_document(self):
        pass


class BasicPrinter(Machine):

    def print_document(self):
        print("Printing")

    def scan_document(self):
        raise NotImplementedError

    def fax_document(self):
        raise NotImplementedError
```

### Good Example

Split the interface into smaller ones.

```python
from abc import ABC, abstractmethod


class Printer(ABC):

    @abstractmethod
    def print_document(self):
        pass


class Scanner(ABC):

    @abstractmethod
    def scan_document(self):
        pass


class Fax(ABC):

    @abstractmethod
    def fax_document(self):
        pass


class BasicPrinter(Printer):

    def print_document(self):
        print("Printing document")


class MultiFunctionPrinter(Printer, Scanner, Fax):

    def print_document(self):
        print("Printing document")

    def scan_document(self):
        print("Scanning document")

    def fax_document(self):
        print("Faxing document")
```

**Remember:** Keep interfaces small and specific.

---

## 6. D — Dependency Inversion Principle (DIP)

**Definition:** High-level modules should not depend directly on low-level modules. Both should depend on abstractions.

### Bad Example

The notification service directly depends on a specific email service.

```python
class EmailService:

    def send(self, message):
        print(f"Email: {message}")


class Notification:

    def __init__(self):
        self.email = EmailService()

    def notify(self, message):
        self.email.send(message)


notification = Notification()
notification.notify("Hello Manish")
```

### Good Example

Make the notification service depend on an abstraction.

```python
from abc import ABC, abstractmethod


class MessageService(ABC):

    @abstractmethod
    def send(self, message):
        pass


class EmailService(MessageService):

    def send(self, message):
        print(f"Email: {message}")


class SMSService(MessageService):

    def send(self, message):
        print(f"SMS: {message}")


class Notification:

    def __init__(self, service):
        self.service = service

    def notify(self, message):
        self.service.send(message)


email = Notification(EmailService())
sms = Notification(SMSService())

email.notify("Hello Manish")
sms.notify("Hello Manish")
```

**Remember:** Depend on abstractions, not concrete implementations.

---

# 7. SOLID Summary

| Principle | Main Idea | Avoid |
|---|---|---|
| SRP | One responsibility per class | One class doing everything |
| OCP | Extend without modifying existing code | Repeatedly editing existing logic |
| LSP | Child should replace parent safely | Breaking inherited behavior |
| ISP | Small, focused interfaces | Large interfaces with unused methods |
| DIP | Depend on abstractions | Tight coupling to concrete classes |

---

# 8. Real-World Example: E-Commerce Application

```python
from abc import ABC, abstractmethod


# SRP: Product contains product information
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price


# OCP + DIP: Payment abstraction
class PaymentMethod(ABC):

    @abstractmethod
    def pay(self, amount):
        pass


class UPIPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Paid {amount} using UPI")


class CardPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Paid {amount} using Card")


# SRP: Handles order operations
class Order:
    def __init__(self, product):
        self.product = product

    def total(self):
        return self.product.price


# DIP: Depends on payment abstraction
class Checkout:
    def __init__(self, payment_method):
        self.payment_method = payment_method

    def process(self, order):
        amount = order.total()
        self.payment_method.pay(amount)


product = Product("Laptop", 50000)

order = Order(product)

checkout = Checkout(UPIPayment())
checkout.process(order)

checkout = Checkout(CardPayment())
checkout.process(order)
```

---

# 9. SOLID Interview Questions

**Q1. What is SOLID?**

Five object-oriented design principles used to build maintainable and extensible software.

**Q2. Why is SRP important?**

It reduces responsibility overlap and makes classes easier to maintain and test.

**Q3. What is the difference between OCP and DIP?**

- OCP focuses on extending functionality without modifying existing code.
- DIP focuses on reducing dependency between high-level and low-level modules.

**Q4. What is LSP?**

A child class should be usable in place of its parent without unexpected behavior.

**Q5. What is ISP?**

Classes should not be forced to implement methods they do not use.

**Q6. Does Python support interfaces?**

Python does not have a dedicated interface keyword. Abstract Base Classes (`abc`) and `Protocol` from `typing` can define interface-like contracts.

**Q7. Does following SOLID always mean creating more classes?**

No. Apply the principles when they improve clarity, flexibility, and maintainability. Avoid unnecessary abstraction.

---

# 10. Quick Revision

```text
S → Single Responsibility
    One class = One responsibility

O → Open/Closed
    Open for extension, closed for modification

L → Liskov Substitution
    Child should replace parent safely

I → Interface Segregation
    Small and specific interfaces

D → Dependency Inversion
    Depend on abstractions, not concrete classes
```
