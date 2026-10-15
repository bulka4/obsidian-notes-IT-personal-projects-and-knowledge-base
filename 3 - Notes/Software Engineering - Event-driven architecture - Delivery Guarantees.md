Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Delivery guarantees describe what the messaging system for asynchronous communication ([[Backend Engineering - Asynchronous request processing|link]])
guarantees about how many times a message ([[Software Engineering - Event-driven architecture - Events and messages|link]]) can be delivered, especially when failures occur. 

Message delivery usually means that a consumer receives a message but it can also mean that a broker receives a message from a producer.

Different delivery guarantees:
- **At-most-once**
    - Deliver the message at most one time.
    - If delivery or processing fails, no retry is performed, so the message may be lost.
- **At-least-once**
    - Retry delivery until the consumer acknowledges that the message.
    - Reliable because messages aren't lost, but message can be delivered multiple times and without idempotency it can cause wrong results
- **Exactly-once**
    - Ensure that the message is processed exactly once, even if failures or retries occur.
    - Typically requires support from both the messaging system and the application (e.g., transactions, deduplication, or idempotency).