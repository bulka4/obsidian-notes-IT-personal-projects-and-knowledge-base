Tags: [[_Databases]]
#Databases  

# Introduction
ORM lets you work with database records as objects/classes instead of writing SQL directly.
# Example (Python `SQLAlchemy`)
```python
user = User(name="John")
session.add(user)
session.commit()
```

The ORM generates SQL:
```sql
INSERT INTO users (name) VALUES ('John');
```
# Benefits
- Less SQL code
- Easier CRUD operations
- Object-oriented programming style
- Database models can be reused
- Often includes migrations and validation
# Drawbacks
- Can hide what SQL is executed
- Complex queries may become harder
- Possible performance issues if used incorrectly