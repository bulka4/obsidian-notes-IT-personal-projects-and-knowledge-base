Tags: [[_Databases]]
#Databases  

# Introduction
Database migrations are a way to manage and track changes to a database schema over time.

Instead of manually changing the database, you create migration files that describe changes and use special tools that apply those changes using those files.
# Migration example
Initial database:
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Later you need an email column:

Migration:
```sql
ALTER TABLE users
ADD email VARCHAR(255);
```

The migration system applies this change to the database.
# Up and down migration
A migration usually has:

1. **Up migration** → apply the change
```sql
ALTER TABLE users ADD email VARCHAR(255);
```

2. **Down migration** → undo the change
```sql
ALTER TABLE users DROP COLUMN email;
```
# Migration history
Migration systems usually save information about which migrations have already been applied inside the database itself, in a special metadata table.

Example:
```sql
CREATE TABLE migration_history (
    id INT PRIMARY KEY,
    migration_name VARCHAR(255),
    applied_at DATETIME
);
```

After applying migrations:
```
migration_history

id | migration_name       | applied_at
---|----------------------|-------------------
1  | create_users_table   | 2026-07-01
2  | add_email_column     | 2026-07-05
3  | create_orders_table  | 2026-07-10
```

When you run migrations again:
1. Migration tool checks this table.
2. It compares it with available migration files:
```
Available:
001_create_users.sql
002_add_email.sql
003_create_orders.sql
004_add_payments.sql  <-- new

Database:
001
002
003
```

3. It runs only missing migrations:
```
004_add_payments.sql
```

4. It inserts a new record:
```
4 | add_payments_table | 2026-07-17
```
# Why migration history is useful
- Decide which migrations to run - When user wants to perform migrations, a migration tool checks in the history which migrations have not been performed yet and performs only those 
	- If it tries to perform a migration that was already performed, e.g. create a table which already exists, it would through an error
- Keep different environments synchronized - When we changed something in a development database and want to have the same schema in another database instance (prod), we can use migration history to apply only missing migrations
- Roll back changes - undo certain migrations
- Collaboration between developers - make sure everyone applies changes in the correct order