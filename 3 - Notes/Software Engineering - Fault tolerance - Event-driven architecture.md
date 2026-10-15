Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Techniques for handling failures in event-driven systems:
- **Dead Letter Queue (DLQ)** - when processing a message ([[Software Engineering - Event-driven architecture - Events and messages|link]]) fails multiple times in a row, it is moved aside to the Dead Letter Queue for inspection in order not to block other messages from being processed and so we don't retry processing this message forever
- **Idempotency** - processing a request / message multiple times has the same effect as processing it one. This makes retries safe in case of failure.
- **Ordering** - Some brokers ([[Software Engineering - Event-driven architecture - Message broker|link]]) preserve an order of messages, some don't. Processing messages in a wrong order can give wrong results.
- **Delivery Guarantees** - Describing how many times a message ([[Software Engineering - Event-driven architecture - Events and messages|link]]) can be delivered when failures occur - at most once, at least once or exactly once.

Topics related to a fault tolerance in event-driven systems:
1. [[Software Engineering - Event-driven architecture - Dead Letter Queue (DLQ)]]
2. [[Software Engineering - Event-driven architecture - Idempotency]]
3. [[Software Engineering - Event-driven architecture - Ordering]]
4. [[Software Engineering - Event-driven architecture - Delivery Guarantees]]