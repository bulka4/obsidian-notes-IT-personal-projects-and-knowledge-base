Tags: [[_Databases]]
#Databases  

# Introduction
There are two different definitions of consistency:
# Read consistency
Read consistency describes what happens when a service tries to read data after a successful write (change in data), what data is returned.

There are two types of consistency:
- Strong consistency - After a successful write any read done by any service will return the latest data
- Eventual consistency - After a successful write the first read done a service might return an old data but after some time, all the reads will return the latest one

This refers to a situation when the same or related data live in different places. 

There can be a situation where we update data in one place and before we update related data in another place, we read from that place stale data.

For example, we might have:
- The same value stored in different places:
	- in different databases (e.g. on-disk database and in-memory cache, or one database replica and its copy)
	- in different tables
- Two different but related values stored in different places:
	- Orders table and customers table with the order count column. When a new order appears in the orders table, then in the customers table we want to have updated order count.
- A table:
	- When we change a name of some value in all records in a table, e.g. "TV" -> "Television", then we might change this value in some records and before we finish updating all the records, some service reads old data from the rest of records.
# Database correctness (ACID consistency)
The database guarantees that every transaction moves the database from one valid state to another valid state (valid state = database rules and constraints remain true).

If a transaction would violate those rules, it is rejected or rolled back.

Example rules:
- User ID must be unique
- Foreign keys must exist
- Balance cannot be negative
