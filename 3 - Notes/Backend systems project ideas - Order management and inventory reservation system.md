Tags: [[__My_projects]]
#MyProjects 

# Introduction
The idea: build a backend that manages orders, inventory and payment processing.

You don't need a frontend, real payment providers or a sophisticated product catalog.

You only need:
- Customers.
- Products.
- Inventory.
- Orders.
- Payments (mock provider).
# Feature 1. Inventory reservation
Problem: overselling products

Imagine your store has 5 units of a product.

Two customers simultaneously attempt to purchase 4 units.

Without proper concurrency control, both requests might succeed, resulting in 8 units being sold despite having only 5 available.

Implement inventory reservations.

Example:
```
Product A:
  Available: 5
  Reserved: 0

Customer 1 requests 4:
  Available: 1
  Reserved: 4

Customer 2 requests 4:
  Rejected: insufficient inventory
```

Techniques and tools:
- Database transactions.    
- Optimistic and pessimistic locking.    
- Atomic SQL updates.    
- Isolation levels.    
- Race condition prevention.    
- Unique constraints.    

This is an excellent practical exercise in concurrency.
# Feature 2. Order processing workflow
Problem: multiple independent operations must succeed together

When a customer places an order, several things need to happen:
1. Create an order.    
2. Reserve inventory.    
3. Process payment.    
4. Confirm the order.    
5. Notify the customer.    

What happens if payment succeeds but the inventory reservation fails?

Or if inventory is reserved but payment fails?

You cannot simply wrap everything in one database transaction because the payment provider is an external system.

This is where you can implement the Saga pattern.

Example:

Order workflow
1. Create order    
    Success    
2. Reserve inventory    
    Success    
3. Process payment    
    Failure    
4. Release inventory reservation    
    Compensation    
5. Mark order as failed    
    Completed    

Instead of rolling back one global transaction, you execute compensating operations.

What you learn:
- Saga orchestration.    
- Compensating transactions.    
- Distributed transactions.    
- State machines.    
- Partial failures.    
- Idempotency.    
- Event-driven workflows.    

You could implement the Saga yourself using Spring services and a database-backed workflow state. No need for a dedicated workflow engine.
# Feature 3. Reliable event processing
Problem: the database update succeeds but publishing the event fails

For example:
```
1. Order is created in database.
2. Application crashes.
3. OrderCreated event is never published.
```

Implement the transactional outbox pattern.

Store the order and the event in the same database transaction.

A background worker then publishes pending events to RabbitMQ.

You can also implement:
- Event consumers.    
- Duplicate message detection.    
- Retry policies.    
- Dead-letter queues.    
- Message acknowledgments.    
- Event ordering where necessary.    

What you learn: reliable asynchronous communication between application components.

This is particularly useful because it extends your previous event-driven architecture experience into actual Java implementation.
# Feature 4. Inventory reservation expiration
Problem: customers reserve products but never pay

For example, someone reserves a product but abandons the checkout.

You don't want inventory to remain reserved indefinitely.

Introduce expiration:
```
Reservation:
  Product: A
  Quantity: 2
  Status: ACTIVE
  Expires at: 14:30
```

A scheduled job periodically finds expired reservations and releases the inventory.

What you learn:
- Scheduling.    
- Background processing.    
- Race conditions between expiration and payment.    
- Atomic state transitions.    
- Distributed locking.    
- Timeouts.    
- Recovery after application restarts.    

This is a particularly nice way to learn how to deal with clocks and concurrent state transitions without implementing an artificial distributed clock algorithm.
# Feature 5. Reconciliation
Problem: your internal order state disagrees with the external payment provider

For example:
```
Your system:
  Order #123: PAYMENT_PENDING

Payment provider:
  Payment #456: COMPLETED
```

Your reconciliation process periodically checks outstanding payments and compares their state with the provider.

It can also detect cases where:
- A payment was completed but the order wasn't confirmed.    
- A refund was processed but the local system still says pending.    
- An operation was submitted multiple times.    
- An order was cancelled but the payment was successful.    

This gives you practical experience with reconciliation and recovery in distributed workflows.
# Feature 6. CQRS and reporting
You could maintain separate read models for:
- Order history.    
- Inventory availability.    
- Sales statistics.    
- Customer purchase history.    

Update these projections asynchronously when events occur.

This introduces CQRS and eventual consistency in a realistic business context.
# Concepts to cover
| Concept                  |
| ------------------------ |
| Java / Spring            |
| Dependency injection     |
| REST API design          |
| GraphQL                  |
| API Gateway / BFF        |
| Thread pools             |
| Semaphores               |
| Race conditions          |
| Locks / deadlocks        |
| Async processing         |
| Backpressure             |
| Rate limiting            |
| Optimistic locking       |
| Pessimistic locking      |
| Database transactions    |
| Isolation levels         |
| RabbitMQ                 |
| Transactional outbox     |
| Idempotency              |
| Retry mechanisms         |
| Reconciliation           |
| Conflict resolution      |
| Offline synchronization  |
| SSE / WebSockets         |
| CQRS                     |
| Event sourcing           |
| Saga                     |
| Distributed coordination |
| Partial failures         |
| Monitoring / logging     |
# Recommended tools and technologies
| Area                 | Technology                        | Why                                              |
| -------------------- | --------------------------------- | ------------------------------------------------ |
| Language             | Java                              | Core programming, concurrency                    |
| Backend framework    | Spring Boot                       | Standard backend development                     |
| Dependency injection | Spring IoC                        | Dependency management                            |
| Database             | PostgreSQL                        | Transactions, locking, SQL                       |
| Database migrations  | Flyway                            | Schema management                                |
| ORM                  | Spring Data JPA / Hibernate       | Database access                                  |
| Message broker       | RabbitMQ                          | Asynchronous processing                          |
| Caching              | Redis                             | Caching, distributed coordination, rate limiting |
| API documentation    | OpenAPI / Swagger                 | API contracts                                    |
| API testing          | Postman                           | Manual API testing                               |
| Unit testing         | JUnit + Mockito                   | Testing                                          |
| Integration testing  | Testcontainers                    | Real PostgreSQL and RabbitMQ in tests            |
| Monitoring           | Micrometer + Prometheus + Grafana | Metrics and monitoring                           |
| Distributed tracing  | OpenTelemetry                     | Request tracing                                  |
| Logging              | SLF4J + Logback                   | Structured logging                               |
| Containerization     | Docker Compose                    | Running infrastructure locally                   |