Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Instance methods — normal methods
Normal methods without any decorator:
```python
class User:
    def __init__(self, name):
        self.name = name
        
    def greet(self):
        return f"Hello {self.name}"
```
The first parameter is conventionally `self`.
# Class method - `@classmethod`
A class method receives the **class** as its first argument, conventionally called `cls`.
```python
class User:
    def __init__(self, name):
        self.name = name

    @classmethod
    def from_dict(cls, data) -> "User":
        # Return User(data["name"])
        return cls(data["name"])
```

```python
# This is the same as using user = User('Marcin')
user = User.from_dict({"name": "Marcin"})
```
# Static method - `@staticmethod`
A static method receives **neither `self` nor `cls` automatically**.
```python
class MathUtils:

    @staticmethod
    def add(a, b):
        return a + b
```

You call:
```python
MathUtils.add(2, 3)
```

It's basically a normal function that happens to be placed inside the class namespace.

It doesn't have access to instance or class state unless you explicitly pass something.
# Property - `@property`
Turns a method into something accessed like an attribute:
```python
class User:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name
```

Instead of:
```python
user.name()
```

we write:
```python
user.name
```

We can also define a setter:
```python
@property
def name(self):
    return self._name

@name.setter
def name(self, value):
    self._name = value
```

Then:
```python
user.name = "John"
```
# Abstract method - `@abstractmethod`
Used with abstract base classes.
```python
from abc import ABC, abstractmethod

class DataSource(ABC):

    @abstractmethod
    def load(self):
        pass
```

A subclass is required to implement `load()` before it can be instantiated.

This is particularly relevant to the interface-style code you've been working with.
