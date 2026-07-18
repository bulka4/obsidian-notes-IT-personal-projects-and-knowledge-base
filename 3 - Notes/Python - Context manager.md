Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
A context manager is an object that defines what should happen when entering and leaving a block of code.

It is used with the `with` statement
# Example
```python
with open("file.txt") as f:
    data = f.read()
```

Here the context manager automatically:
1. **Opens** the file when entering the block.
2. **Closes** the file when leaving the block (even if an error occurs).
# Methods
A context manager implements two methods:
- `__enter__()` → runs at the start of the `with` block
- `__exit__()` → runs at the end of the `with` block
# Defining a context manager
We can define our own context managers like this:
```python
class MyContext:
    def __enter__(self):
        print("Start")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Cleanup")

with MyContext():
    print("Inside")
```

Output:
```python
Start
Inside
Cleanup
```
# Common uses
- Opening/closing files
- Database connections
- Locks (`threading.Lock`)
- Managing resources (memory, network connections)
# Creating context managers using `contextlib`
```python
from contextlib import contextmanager

@contextmanager
def my_context():
    print("Start")
    yield
    print("Cleanup")
```