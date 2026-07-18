Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A Repository is a pattern used to separate business logic from data access. It acts as an abstraction over where and how data is stored.

In simple terms:
> A repository provides an interface for retrieving and saving domain objects ([[Software Engineering - Architecture concepts - Domain objects|link]]) without exposing database details.
# Example
```
Application Layer
        |
        v
OrderRepository (interface / repository)
        |
        v
PostgresOrderRepository (implementation)
        |
        v
Database
```

The domain/application code says:
```python
order = order_repository.get(order_id)

order.confirm()

order_repository.save(order)
```

It does not know:
- SQL queries
- database connections
- table structure
- ORM details