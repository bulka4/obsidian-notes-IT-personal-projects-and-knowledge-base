Tags: [[_Databases]]
#Databases  

# Introduction
Referential integrity is a rule saying that when column A references another column B, then all values in the A column must exist in the column B.

An example implementation of this rule is a foreign key in SQL database - [[SQL databases - Foreign key|link]].

For example, when we create one column that references another column like this:
```sql
FOREIGN KEY (user_id)
REFERENCES users(id)
```
then we can't create a record with such value of `user_id` which doesn't exist in the `users` table, `id` column.