Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Interfaces define a contract: they specify what methods an object should provide, without specifying how they are implemented.
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