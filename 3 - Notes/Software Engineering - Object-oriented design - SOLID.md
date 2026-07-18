Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**SOLID** is a set of five principles for designing maintainable, flexible, and understandable object-oriented software.
# **S — Single Responsibility Principle (SRP)**
A class should have **one reason to change** (one main responsibility).

Bad:
```python
class User:
    def save_to_database(self):
        pass

    def send_email(self):
        pass
```

Better:
```python
class UserRepository:
    def save(self):
        pass

class EmailService:
    def send(self):
        pass
```
# **O — Open/Closed Principle (OCP)**
Software entities should be **open for extension, closed for modification**.

Meaning: add new behavior without changing existing code.

Example:
```python
class Payment:
    def pay(self):
        pass
```

Add:
```python
class CreditCardPayment(Payment):
    def pay(self):
        pass
```

instead of modifying `Payment` every time.
# **L — Liskov Substitution Principle (LSP)**
A parent class should be replaceable with its subclass without breaking the program. So when we use a subclass instead of a parent class, code should work.

For example, when we have classes:
```python
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):
    def bark(self):
        print("Woof")
```

and a function:
```python
def feed(animal: Animal):
    animal.eat()
```

we can use in this function both classes, we can use the subclass instead of the parent class:
```python
feed(Dog())  # works fine
```
# **I — Interface Segregation Principle (ISP)**
When we create a child class, it shouldn't have to define functions it doesn't need.

Sometimes a class forces that every child class must define some specific functions, for example when we have a class like this:
```python
from abc import ABC, abstractmethod

class Machine(ABC):
    @abstractmethod
    def print(self):
        pass

    @abstractmethod
    def scan(self):
        pass

    @abstractmethod
    def fax(self):
        pass
```

now every child class must implement all those functions.

So we can't create a simple child class without some of those functions, for example:
```python
class SimplePrinter(Machine):
    def print(self):
        print("Printing")

    # missing scan()
    # missing fax()
```
# **D — Dependency Inversion Principle (DIP)**
High-level code should depend on **abstractions**, not concrete implementations.

Bad:
```python
class OrderService:
    def __init__(self):
        self.database = MySQLDatabase()
```

Better:
```python
class OrderService:
    def __init__(self, database):
        self.database = database
```

Now it can work with MySQL, PostgreSQL, mocks, etc.
# In short

|Principle|Meaning|
|---|---|
|**S**|One class → one responsibility|
|**O**|Extend behavior without modifying existing code|
|**L**|Subclasses should behave like their parent|
|**I**|Don't force unused interfaces|
|**D**|Depend on abstractions, not concrete implementations|
# Questions
- 