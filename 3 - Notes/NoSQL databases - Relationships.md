Tags: [[_Databases]]
#Databases  

# Introduction
NoSQL databases don't handle well relations between tables (when a column in one tables references to a column in another table). SQL databases are much better for this [[SQL databases - Relationships|link]].

Usually in NoSQL databases there is no built-in support for joins, foreign keys, and referential integrity ([[SQL databases - Referential integrity|link]]) like SQL databases do.
# Simpler and faster joins
Joins in SQL have simpler syntax and are more efficient (faster).

For example, to find data for users and orders, we need two queries:
```python
user = users.find(id=1)
orders = orders.find(user_id=1)
```

We can't use a single join like in SQL database:
```sql
select * from
	users as u
	left join orders as o
		on o.user_id = u.user_id
```
# Denormalization
Because joins are difficult, NoSQL often duplicates data (denormalizes it ([[Data modelling - Normalization vs Denormalization|link]])). So for example, instead of storing users and orders data separately:
```json
{ // orders
    "_id": 10,
    "product": "Laptop",
    "user_id": 1
}
{ //users
	"_id": 1
	"name": "Alice"
}
```

we might include user data in orders data:
```json
{
    "_id": 10,
    "product": "Laptop",
    "user": {
        "id": 1,
        "name": "Alice"
    }
}
```

Because of that, updates becomes harder, we need to update more tables. For example, when user changes a name, we need to update both `users` and `orders` tables.