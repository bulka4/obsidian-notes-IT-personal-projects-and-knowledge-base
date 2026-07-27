Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A variable of the result (either) type contains information about:
- The value of this variable
- Whether or not the operation that created this variable was successful
- The error that occurred when creating this variable
# Example
For example, in Python we can implement such a type like this:
```python
from typing import Generic, TypeVar

T = TypeVar("T")
E = TypeVar("E")

class Result(Generic[T, E]):
    def __init__(self, value=None, error=None):
        self.value = value
        self.error = error

    def is_success(self):
        return self.error is None
```

Then we can create a function that returns a variable of the `Result` type:
```python
def divide(a: int, b: int) -> Result[float, str]:
    if b == 0:
        return Result(error="Cannot divide by zero")

    return Result(value=a / b)
```

And when we use this function, we can check whether the returned variable was created successfully or whether there was some error:
```python
result = divide(10, 2)

if result.is_success():
    print(result.value)   # 5.0
else:
    print(result.error)
```
