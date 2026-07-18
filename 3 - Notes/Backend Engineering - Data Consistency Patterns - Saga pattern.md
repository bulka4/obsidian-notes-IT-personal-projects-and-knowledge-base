Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Saga pattern is a data consistency pattern ([[Backend Engineering - Distributed systems - Data Consistency Patterns (distributed transactions)|link]]) used in distributed microservices ([[Backend Engineering - Distributed systems|link]]).

In this situation, using Saga pattern we use compensating actions which can cancel actions performed earlier. 

For example, when we have services like:
- Order Service → create order
- Payment Service → charge card
- Inventory Service → reserve stock

and service 3 failed - product can't be sent, then we can perform as compensating steps - return money and cancel order.
# Two types
## 1. Choreography (event-driven)
Each service reacts to events ([[Backend Engineering - Event-driven architecture - Events and messages|link]]):
```
Order created → Payment starts
Payment success → Inventory reserves stock
```

If failure:
```
Payment failed → Order canceled event
```
## 2. Orchestration
A central coordinator controls the flow:
```
Saga Orchestrator:
1. Call Payment
2. Call Inventory
3. If failure → run compensation steps
```
