Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A monad is a pattern where we define a variable type (a class) where we define:
- Variable value
- Additional information about this variable (e.g. whether there was an error when creating this variable)
- Methods for what to do with this variable depending on the variable's value
# Example
For example, a monad could be a class in Python like this:
```python
class Result:
    def __init__(self, value=None, error=None):
        self.value = value
        self.error = error

    def is_success(self):
        return self.error is None

    def and_then(self, func):
        if self.is_success():
            return func(self.value)
        else:
            return self  # keep the error
```

so it specifies:
- Values of the variable
- Information about whether there was an error during creating this variable (and what error that was)
- What to do with this variable depending on its value (the `and_then` method)