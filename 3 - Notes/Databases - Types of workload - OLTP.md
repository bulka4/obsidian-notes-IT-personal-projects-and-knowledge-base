Tags: [[_Databases]]
#Databases  

# Introduction
OLTP (Online Transaction Processing) describes a type of database workload/application which focus on:
- Many small transactions
- Fast response time
- Frequent inserts/updates/deletes
- Strong consistency and transactions

Examples:
- Banking transactions
- E-commerce orders
- User accounts
- Inventory systems

Example query:
```sql
UPDATE accounts
SET balance = balance - 100
WHERE id = 1;
```