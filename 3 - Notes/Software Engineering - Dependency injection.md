Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Dependency Injection (DI) is a software design technique where an object receives its dependencies from the outside instead of creating them itself.

The main idea:
> A class should not create the objects it depends on; those objects should be provided to it.
# Example
Without dependency injection:
```python
class UserService:
    def __init__(self):
        self.database = PostgreSQLDatabase()
```

`UserService` creates its own database.

With dependency injection:
```python
class UserService:
    def __init__(self, database):
        self.database = database
```

Now someone else provides the database:
```python
db = PostgreSQLDatabase()

service = UserService(db)
```

For a test:
```python
fake_db = FakeDatabase()

service = UserService(fake_db)
```
# Why to use it
- Easier testing - We can replace a real dependency with a fake one for testing ([[Software Engineering - Test doubles|link]])
- Lower coupling and easier changes - We can use different dependencies without changing the service's code.
# Types of dependency injection
## 1. Constructor injection (most common)

Dependencies are passed through the constructor.
```python
class Service:
    def __init__(self, logger):
        self.logger = logger
```
## 2. Setter injection
Dependencies are assigned after object creation.
```python
service.set_logger(logger)
```
## 3. Method injection
Dependency is passed only to a specific method.
```python
service.process(data, logger)
```