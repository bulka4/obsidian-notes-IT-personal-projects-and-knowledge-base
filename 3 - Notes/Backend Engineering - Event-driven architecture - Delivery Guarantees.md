Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Delivery guarantees describe what the messaging system for asynchronous communication ([[Backend Engineering - Asynchronous communication|link]])
guarantees about message ([[Backend Engineering - Event-driven architecture - Events and messages|link]]) delivery, especially when failures occur:
- **At-most-once**
    - Deliver the message **at most one time**.
    - If delivery or processing fails, **no retry is performed**, so the message may be lost.
- **At-least-once**
    - Retry delivery until the consumer acknowledges that the message.
    - Reliable because messages aren't lost, but message can be delivered multiple times and without idempotency it can cause wrong results
- **Exactly-once**
    - Ensure that the message is **processed exactly once**, even if failures or retries occur.
    - Typically requires support from both the messaging system and the application (e.g., transactions, deduplication, or idempotency).