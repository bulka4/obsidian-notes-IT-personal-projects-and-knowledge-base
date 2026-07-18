Tags: [[_Python]] [[__Programming_languages]] [[_Software_Engineering]]
#Python #ProgrammingLanguages #SoftwareEngineering 

# Introduction
Exceptions are mechanisms in Python for handling errors or unexpected situations during program execution.

Instead of crashing immediately, a program can raise an exception and catch it.
# Catching an exception
Catching an exception means to do something else when some activity raises an error, for example:
```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```
# Raising exceptions
We can raise exceptions ourself:
```python
def withdraw(amount):
    if amount < 0:
        raise ValueError("Amount cannot be negative")
```
# Common built-in exceptions
- `ValueError` → wrong value type/content
- `TypeError` → wrong type
- `FileNotFoundError` → missing file
- `KeyError` → missing dictionary key
- `IndexError` → invalid list index
- `ConnectionError` → network/database connection problem
# Creating exceptions
We can create custom exceptions:
```python
class UserNotFoundError(Exception):
    pass
```

and use:
```python
raise UserNotFoundError("User does not exist")
```
