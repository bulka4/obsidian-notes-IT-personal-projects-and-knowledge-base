Tags: [[_Databases]]
#Databases  

# Introduction
There are two different definitions of consistency:
# Read consistency
Read consistency describes what happens after a successful write (change in data). This refers to systems consisting of multiple nodes (servers) and also to a single machine:
- Strong consistency - After a successful write:
	- All nodes in the system contains the latest data during any read
	- So any read will return the latest data
- Eventual consistency - After a successful write:
	- All nodes in the system will contain the latest data after some time, not necesserily before the first read
	- So the first read might return an old data and later reads will return the latest one
# Database correctness (ACID consistency)
The database guarantees that every transaction moves the database from one valid state to another valid state (valid state = database rules and constraints remain true).

If a transaction would violate those rules, it is rejected or rolled back.

Example rules:
- User ID must be unique
- Foreign keys must exist
- Balance cannot be negative