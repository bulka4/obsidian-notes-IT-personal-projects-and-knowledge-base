Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
CQRS is a technique separates writes (commands) and reads (queries) responsibilities. This separation might be implemented using for writes and reads different:
- Data models (tables used for writes and reads)
- Storage systems
- code

This technique:
- is often used in distributed microservices ([[Backend Engineering - Distributed systems|link]]) and event-driven systems ([[Backend Engineering - Asynchronous request processing|link]]). 
- is useful when reads and writes have different needs:
	- writes need consistency / correctness
	- reads need speed and scalability
# Data models
We can separate reads and writes using read and write data models (database tables / documents) optimized for reads and writes.

It doesn't mean that when a table is optimized for writes we don't read from it. For every table we always do both reads and writes.
## Write data model
The write data model is optimized for write speed, correctly applying changes to data while enforcing business rules and maintaining consistency.

It is the authoritative representation / source of truth of an application state ([[Software Engineering - State|link]]).

To optimize a data model for writes, we can use:
- **Normalization**: reduces unnecessary duplication of data and the risk of inconsistent updates.
- **Constraints**: primary keys, foreign keys, uniqueness constraints and other rules help protect data integrity.
- **Transactions**: allow related changes to succeed or fail together.
- **Concurrency control**: locks or conditional updates prevent conflicting changes, such as two customers buying the last item.
- **Domain rules**: the application enforces rules such as "a shipped order cannot be cancelled."

When updating data (performing a write), we might need to update multiple records and tables, and enforce certain rules. 

For example, in an e-commerce app, when placing an order, the application needs to:
1. Check that sufficient inventory is available.
2. Create the order and its items.
3. Decrease inventory.
4. Ensure concurrent requests don't oversell the same product.
5. Commit the changes safely, potentially in a database transaction.

A part of the write data model might be the orders table:
```
| OrderID | amount | productID |
| 1       | 1      | 1         |
| 2       | 3      | 5         |
```

or in the semantic search system we might have one write table with text documents and another read table with embeddings for those text documents which are used for semantic search.
## Read data model
A read model is optimized to retrieve the data needed for queries quickly, often by reducing the amount of work required when reading.

Common techniques include:
- **Denormalization**: store related data together to avoid expensive joins.
- **Indexes**: speed up lookups and filtering.
- **Precomputed aggregates**: stores calculated values such as total sales instead of computing them for every query.
- **Materialized views**: store the results of frequently used queries.
- **Specialized storage**: use a database or data structure suited to the query patterns.

For example, instead of joining `Orders`, `OrderItems`, and `Products` every time a customer views their order history, a read model could store a ready-to-display order summary.

The trade-off is that maintaining the read model requires extra work when the underlying data changes, and asynchronous updates can make it temporarily stale.

A part of the read data model might be a table with total sales per customer:
```
| customerID | totalSales |
| 1          | 1000       |
| 2          | 5000       |
```

or in the semantic search system we might have one write table with text documents and another read table with embeddings for those text documents which are used for semantic search.
# Code
We can separate also code for reads and writes, such that each function or a class is designed just for reads or writes.
## Write side
**Responsibilities**:
- validate input
- enforce business rules
- update database
- emit events (often)

Commands can change a state of an application ([[Software Engineering - State|link]]).

This side is focused on:
> “Make the change happen correctly”

For example, we might have functions like:
- create order
- update Orders table
- publish `OrderCreated` event
- the `POST /orders` route
## Read side
**Responsibilities**:
- serve fast reads
- optimized for queries
- often denormalized data

Queries shouldn't change a state of an application ([[Software Engineering - State|link]]).

This side is focused on:
> “Return data fast and efficiently”

For example, we might have functions like:
- read from a read data model
- the `GET /orders/123` route
# Typical architecture
```
Command → Write DB → Event → Read DB updated → Query uses Read DB
```

Often combined with event-driven systems ([[Backend Engineering - Asynchronous request processing|link]]).