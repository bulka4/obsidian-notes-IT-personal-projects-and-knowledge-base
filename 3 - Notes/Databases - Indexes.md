Tags: [[_Databases]]
#Databases  

# Introduction
Indexes are additional data structures that organize data to make certain operations faster. They are mainly associated with data retrieval, but they also affect writes because they must be maintained when data changes.
# Common index structures
Common index structures include:
- B-tree - [[Databases - Indexes - B-tree index|link]] 
- Hash index - [[Databases - Indexes - Hash index|link]] 
- LSM-tree - [[Databases - Indexes - LSM-tree index|link]] 
# How indexes work
Let's assume, we have a table like this:
```
users

id | name  | age
---+-------+----
1  | Alice | 30
2  | Bob   | 25
3  | Carol | 40
```

Without an index, when searching for a specific value, for example when running a query:
```sql
SELECT *
FROM users
WHERE name = 'Carol';
```
database needs to scan every row.

With an index, we create a separate structure with values from a specific column and information about which row / rows contain this value:
```
Index:

Alice → row location 1
Bob   → row location 2
Carol → row location 3
```

When we search for a specific value, e.g. `WHERE name = 'Carol'`, the database searches the index first to find which rows contains this value:
```
Carol → row location 3 → fetch row
```

So with an index it is faster because we search through just an index which doesn't contain all the columns.
# Updating and writing data
Indexes improve reads but make writes and updates more expensive because database must update not only table but also an index.
# Clustered vs non-clustered indexes
## Clustered index
The table data itself is organized according to the index.

Example:
```
Primary key order:

1 Alice
2 Bob
3 Carol
```

The rows are physically stored in that order.

Common in:
- SQL Server
- InnoDB primary key storage
## Non-clustered index
Separate structure:
```
Index:

Alice → row 500
Bob   → row 200
```

The table remains separately stored.
