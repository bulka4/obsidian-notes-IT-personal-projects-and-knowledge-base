Tags: [[_Databases]]
#Databases  

# Introduction
ACID transactions provide:
- Atomicity
- Consistency
- Isolation
- Durability
# Atomicity
A transaction either fully succeeds or fully fails.
# Consistency
Every transaction moves the database from one valid state to another valid state (valid state = rules and constraints remain true).

If a transaction would violate those rules, it is rejected or rolled back.

Example rules:
- User ID must be unique
- Foreign keys must exist
- Balance cannot be negative
# Isolation
Concurrent operations don't corrupt each other.
# Durability
Once committed, data survives crashes