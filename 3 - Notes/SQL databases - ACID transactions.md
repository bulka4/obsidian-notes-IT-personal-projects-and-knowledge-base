Tags: [[_Databases]]
#Databases  

# Transactions
Most of the operations in SQL are transactions ([[Software Engineering - Transactions|link]]):
```sql
INSERT
UPDATE
DELETE
```

We can also grab multiple commands into a single transaction:
```sql
BEGIN;

<command 1>

<command 2>

COMMIT;
```
# Atomicity with Write-Ahead Log (WAL)
Atomicity is sometimes implemented using Write-Ahead Log (WAL).

Before modifying data pages, the database writes records to a log:
```
Transaction 123:

UPDATE account A:
100 -> 0

UPDATE account B:
50 -> 150
```

Only then are actual data pages modified.

If the database crashes, on restart it checks the log and:
- If transaction was incomplete, it performs a rollback
- If transaction committed, it redo changes

This guarantees atomicity and durability.
# Consistency
Consistency is implemented using:
- constraints
- foreign keys
- check constraints
- unique indexes
- triggers (sometimes)
# Isolation
Without isolation, if we have for example:
- Data about products with a column `quantity`
- Currently `quantity = 1`
- Two users buys the same product at the same time
- We end up with `quantity = -1` - incorrect
## Implementation
Isolation can be implemented using for example:
- Locks
- MVCC (Multi-Version Concurrency Control)
### Locks
Database locks rows, so one transaction which wants to modify a row, needs to wait for other transactions which modifies currently the same row to finish.
### MVCC (Multi-Version Concurrency Control)
Instead of overwriting rows, transactions see different versions depending on when they started.

This allows many reads without blocking writes.
## Isolation levels
SQL defines several isolation levels.
### Read Uncommitted
- Can see data that may later roll back.
- Rarely used.
### Read Committed
- Only committed changes are visible.
- Default in PostgreSQL.
### Repeatable Read
A transaction sees a stable snapshot.

Example:
```
T1:
SELECT balance -> 100

T2:
UPDATE balance -> 50
COMMIT

T1:
SELECT balance -> still 100
```
### Serializable
- Transactions behave as if they executed one after another.
- Strongest isolation.
- Most expensive.
# Durability
Once COMMIT succeeds, data survives crashes. This is again mainly implemented using Write-Ahead Log (WAL). Commit sequence:
1. Write transaction log to disk
2. Return COMMIT success
3. Flush actual pages later

Even if server crashes, it can replay logs.