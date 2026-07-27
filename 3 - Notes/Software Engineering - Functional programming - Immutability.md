Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Immutability means that once an object is created, it cannot be changed. Instead of modifying it, you create a new object with the desired changes.
# Example
Mutable - change the `name` attribute of the `user` class:
```python
user.name = "John"
```

Immutable - create a new `user` object:
```python
new_user = user.create_user_with_name("John")
```
# Benefits
- **Easier debugging** — data does not unexpectedly change somewhere else.
- **Safer concurrency** — multiple threads/processes can read the same data without worrying about modifications.
- **Better testing** — functions have fewer hidden dependencies.
- **Clearer code flow** — state changes are explicit.
