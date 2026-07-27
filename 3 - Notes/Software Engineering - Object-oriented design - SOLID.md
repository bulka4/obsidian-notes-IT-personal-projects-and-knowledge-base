Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
SOLID is a set of five principles for designing maintainable, flexible, and understandable object-oriented software.
# **S — Single Responsibility Principle (SRP)**
A class should have one main responsibility. 

So we could say that there should be only one reason to change this class code - that means that only a change in this one responsibility is a reason to change class code.

For example, instead of doing something like this:
```python
class User:
    def save_to_database(self):
        pass

    def send_email(self):
        pass
```

do this:
```python
class UserRepository:
    def save(self):
        pass

class EmailService:
    def send(self):
        pass
```
# **O — Open/Closed Principle (OCP)**
Software entities should be open for extension, closed for modification.

Meaning: add new behavior without changing existing code.

For example, when we have a class like this:
```python
class Payment:
    def pay(self):
        pass
```

We can extend this code by creating a new class (without modifying existing code):
```python
class CreditCardPayment(Payment):
    def pay(self):
        pass
```
# **L — Liskov Substitution Principle (LSP)**
A parent class should be replaceable with its subclass without breaking the program. So when we use a subclass instead of a parent class, the code should work.

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

then every child class must implement all those functions.

So we can't create a simple child class without some of those functions, for example:
```python
class SimplePrinter(Machine):
    def print(self):
        print("Printing")

    # missing scan()
    # missing fax()
```
# **D — Dependency Inversion Principle (DIP)**
Code that implements the main logic / business rules of the application, should depend on abstractions, not concrete implementations.

For example, instead of writing to use MySQL database:
```python
class OrderService:
    def __init__(self):
        self.database = MySQLDatabase()
```

It is better to provide an argument which specifies which database we want to use:
```python
class OrderService:
    def __init__(self, database):
        self.database = database
```

This way, when we change technical details (e.g. use PostgreSQL instead of MySQL), we don't need to make big changes in code that defines the main logic of the application, instead we just change one parameter specifying which database to use.
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