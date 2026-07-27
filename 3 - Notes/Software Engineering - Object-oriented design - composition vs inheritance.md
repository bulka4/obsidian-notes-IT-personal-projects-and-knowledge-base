Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Composition vs inheritance are two ways to reuse code and model relationships.
# Inheritance ("is-a")
A class inherits behavior from another class.

Example:
```python
class Animal:
    def eat(self):
        pass

class Dog(Animal):
    def bark(self):
        pass
```

Relationship:
```
Dog is an Animal
```

Pros:
- Easy code reuse
- Supports polymorphism

Cons:
- Creates strong coupling
- Changes in parent can affect children
- Deep inheritance hierarchies become difficult to maintain
# Composition ("has-a")
A class contains other objects and delegates work to them.

Example:
```python
class Engine:
    def start(self):
        pass

class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
```

Relationship:
```
Car has an Engine
```

Pros:
- More flexible
- Lower coupling
- Components can be swapped easily

Cons:
- Sometimes requires more code