Tags: [[_Databases]]
#Databases  

# Introduction
A foreign key enforces that values in one column must exist in a referenced column (usually a primary key) in another table.

For example, if we have two tables:
```sql
-- orders table
userID <- foreign key referencing users.userID
orderID

-- users table
userID <- primary key
userName
```

then all values in the `orders.userID` column must exist in the `users.userID` column.
# Important facts
- Referenced column must be unique
- We can control what happens when referenced data changes - For example:
	- we can't delete a primary key as long as another table contains a foreign keys referencing it
	- When deleting a value in a primary key column, the same values in the foreign key column in another table gets deleted