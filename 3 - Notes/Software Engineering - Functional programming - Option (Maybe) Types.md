Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
An option (maybe) type is a type used to explicitly indicate that a given variable can have no value (can be `None` or `null`).

A variable of this type represents a value that may or may not exist. It has two possible states:
- Some - means that the variable has some value
- None - means that the variable has no value
# Example
Python has no built-in option variable type but we can implement it like this:

Define the Option variable type:
```python
from typing import Generic, TypeVar

T = TypeVar("T")

class Option(Generic[T]):
    def __init__(self, value: T | None):
        self.value = value
        self.is_none = value is None

    def has_value(self) -> bool:
        return not self.is_none
```

Use it in a function to clearly indicate that the returned value can be `None`:
```python
def find_user(user_id: int) -> Option[str]:
    if user_id == 1:
        return Option("John")

    return Option(None)
```

Now, we can check whether the variable returned by this function is `None` this way:
```python
user = find_user(2)

if user.has_value():
    print(user.value)
else:
    print("User does not exist")
```