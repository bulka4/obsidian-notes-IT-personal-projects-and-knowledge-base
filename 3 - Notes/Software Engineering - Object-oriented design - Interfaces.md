Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
An interface ([[Software Engineering - Architecture concepts - Interface|link]]) can be implemented as a class. In one class we define which methods exist and in other classes we define their logic.

So interface specifies which methods should be available in every implementation of that interface (i.e. in every class that defines a logic for those methods).
# Example
Interface specifying that each object of the `Storage` type should have the `save` method:
```python
from abc import ABC, abstractmethod

class Storage(ABC):
    @abstractmethod
    def save(self, data):
        pass
```

Different classes can implement the same interface:
```python
class DatabaseStorage(Storage):
    def save(self, data):
        print("Saving to database")

class FileStorage(Storage):
    def save(self, data):
        print("Saving to file")
```

Now code can depend on the interface, for example we specify that a function argument should be of the `Storage` class:
```python
def store_data(storage: Storage):
    storage.save("hello")
```

and as the `storage` argument we can pass object of any class which have the `save` method. It does not care whether it gets a database or file storage.