Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Event-driven systems are systems where services send messages about events to each other:
- One service publishes an event
- Message broker receives and stores a message with information about the event
- Multiple other services receives and processes the message
- There is no response sent back to the requester (the service that published the event)

Event-driven systems are a method for obtaining an asynchronous communication ([[Backend Engineering - Asynchronous communication|link]]), i.e. a communication where one service sends a message to another one, doesn't wait for a response and can continue with other tasks.

This allows to keep independent the service that emits an event and services that process it.

For example, we might have services like:
```
Customer
    │
    ▼
Order Service
    │
    │ publishes "OrderCreated" event
    ▼
Message Broker
    │
 ┌──┼───────────┬───────────┐
 ▼  ▼           ▼           ▼
Payment     Inventory    Email
Service      Service     Service
```
- Client makes a request to the `Order Service`
- `Order Service` sends requests to other services `Payment` etc.
- The `Order Service` response to the client quickly "order received" without waiting for other services to finish processing the request.
# More notes related to event-driven architecture
1. [[Backend Engineering - Event-driven architecture - Benefits and drawbacks]]
2. [[Backend Engineering - Event-driven architecture - Events and messages]]
3. [[Backend Engineering - Event-driven architecture - Producer and consumer]]
4. [[Backend Engineering - Event-driven architecture - Message broker]]
5. [[Backend Engineering - Event-driven architecture - Queues (point-to-point)]]
6. [[Backend Engineering - Event-driven architecture - Topics (pub-sub)]]
	1. [[Backend Engineering - Event-driven architecture - Consumer group]]
7. [[Backend Engineering - Event-driven architecture - Partitioning]]
	1. [[Backend Engineering - Event-driven architecture - Partition replication]]
8. [[Backend Engineering - Fault tolerance - Event-driven architecture]]
	1. [[Backend Engineering - Event-driven architecture - Dead Letter Queue (DLQ)]]
	2. [[Backend Engineering - Event-driven architecture - Idempotency]]
	3. [[Backend Engineering - Event-driven architecture - Ordering]]
	4. [[Backend Engineering - Event-driven architecture - Delivery Guarantees]]