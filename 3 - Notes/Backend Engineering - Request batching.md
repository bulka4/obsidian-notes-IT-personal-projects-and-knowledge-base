Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Batching requests is an optimization technique where we combine multiple small requests into one larger request to reduce network overhead and improve performance.
# Benefits
Making one request instead of multiple ones is better because each network call has overhead:
- connection setup (sometimes)
- request headers
- serialization/deserialization
- latency (biggest cost)
# Drawbacks
- higher memory usage per request
- more complex error handling (partial failures)
- added latency for single item (wait for batch)
- larger payloads
# Where batching is used
## Database access
Instead of:
```sql
SELECT * FROM users WHERE id = 1;SELECT * FROM users WHERE id = 2;
```

Better:
```sql
SELECT * FROM users WHERE id IN (1,2,3);
```
## APIs
- bulk endpoints (`/createUsers`, `/getOrders`) ([[Backend Engineering - Bulk endpoints|link]])
- GraphQL (naturally reduces overfetching) ([[Backend Engineering - API architectures - GraphQL|link]])
## Event processing
In event-driven systems ([[Backend Engineering - Asynchronous communication|link]]), instead of sending one event at a time, we can send events in chunks to Kafka or queues.
## Machine learning / analytics
Perform ETL processes (read data, transform and insert into a database) or make predictions using a ML model on data batches instead of per record.

Making predictions on batches is especially beneficial when using GPUs as we can do more computations in parallel.