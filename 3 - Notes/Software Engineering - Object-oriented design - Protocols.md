Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Protocols let us define what methods and attributes an object should have, similarly to interface ([[Software Engineering - Architecture concepts - Interface|link]]).
# Example
We can create a class using a protocol like this:
```python
from typing import Protocol

class Storage(Protocol):
    def save(self, data: str) -> None:
        ...
```

and when we write a function where we specify a type of an argument like that:
```python
def store_data(storage: Storage):
    storage.save("hello")
```

that means that we can pass as an argument into this function any object which has the same methods as the Storage class (the `save` method in this case).