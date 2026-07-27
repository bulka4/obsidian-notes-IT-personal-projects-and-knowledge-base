Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The singleton design pattern ([[Software Engineering - Object-oriented design - Design patterns|link]]) ensures that only one instance of a class exists and provides a global access point to it.
# Example
```python
class DatabaseConnection:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```

Usage:
```python
db1 = DatabaseConnection()
db2 = DatabaseConnection()

print(db1 is db2)  # True
```

Both variables point to the same object.
# Common use cases
- configuration manager
- logging service
- connection pool manager
- application-wide settings
# Problems
Singleton introduces global state, that means that the state of an object is accessible and modifiable from many places in the application, without explicitly passing it around.

For example, we can create an object in one place:
```python
config = Config()
config.debug = True
```

and if we try to create this object again in another place we don't create a new object by get the same object as created earlier:
```python
config = Config()
config.debug # this is still True as we set up earlier
```

This can make code:
- harder to test
- harder to reason about
- more coupled