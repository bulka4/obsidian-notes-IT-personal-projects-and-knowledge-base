Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A Repository is an interface ([[Software Engineering - Architecture concepts - Interface|link]]) for reading / saving domain objects ([[Software Engineering - Architecture concepts - Domain objects|link]]) in a database.

Repository:
- Provides functions for reading and saving domain objects without exposing database details (it abstracts database details)
- Separates business logic from data access
- Acts as an abstraction over where and how data is stored.
# Example
For example, we can have `OrderRepository` class as a repository (interface) and `SqlOrderRepository` class as a specific implementation:
```
Application Layer
        |
        v
OrderRepository (interface / repository)
        |
        v
SqlOrderRepository (implementation)
        |
        v
Database
```

The `OrderRepository` class interface can look like this:
```python
from abc import ABC, abstractmethod

# Repository interface
class OrderRepository(ABC):

    @abstractmethod
    def get(self, order_id: int):
        """Retrieve an Order aggregate by its ID."""
        pass

    @abstractmethod
    def save(self, order):
        """Persist an Order aggregate."""
        pass
```

And a specific implementation can look like this:
```python
class SqlOrderRepository(OrderRepository):

    def __init__(self, database):
        self.database = database

    def get(self, order_id):
        # Database-specific code for reading data
		...

    def save(self, order):
        # Database-specific code for saving data
        ...
```

Then, in the application, we read and save data using the interface and providing a specific implementation as an argument like this:
```python
class OrderService:
    def __init__(self, order_repository: OrderRepository):
        self.order_repository = order_repository

    def confirm_order(self, order_id):
        order = self.order_repository.get(order_id)
        order.confirm()
        self.order_repository.save(order)
      

# Provide a specific implementation of the interface
database = DatabaseConnection()
repository = SqlOrderRepository(database)

# Use the interface for any implementation
order_service = OrderService(
    order_repository=repository
)

order_service.confirm_order(123)
```

So:
- In the app, we doesn't show any database-specific code for reading or saving data. We show it only in a specific implementation.
- This app will work for any database (any implementation).
- We provide a specific database implementation as an argument.
- After some time, we can create a different implementation (e.g. use a different database) and change only the argument used in the application
