Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Protocols let us define what methods and attributes an object should have. 

For example, when defining what is a type of arguments and returned value in functions:
- We can specify that this type should be a class created using a protocol 
- then, this argument / returned value can be an object of any class which posses the same methods as the specified class with a protocol (but it can be an object of a different class)
# Example
We create a class using a protocol like this:
```python
from typing import Protocol

class Storage(Protocol):
    def save(self, data: str) -> None:
        ...
```

and when we write a function like that:
```python
def store_data(storage: Storage):
    storage.save("hello")
```

that means that we can pass as an argument into this function any object which has the same methods as the Storage class (the `save` method in this case).