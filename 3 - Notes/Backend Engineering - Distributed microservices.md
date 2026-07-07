Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Distributed microservices refers to a system where we have multiple services (applications) performing different actions and communicating with each other.

For example, we might have services like:
- Order - Where clients make orders
- Payment - Process payment for the order from the user
- Inventory - Prepare products to send to the client

In distributed microservices, there might be problems like:
- Partial failures (one service works, another doesn’t)
- Eventual consistency
- Duplicate messages
- Out-of-order events

