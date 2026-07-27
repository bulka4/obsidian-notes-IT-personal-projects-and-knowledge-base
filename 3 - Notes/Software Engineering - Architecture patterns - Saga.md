Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Saga pattern is a data consistency pattern ([[Backend Engineering - Distributed systems - Data Consistency Patterns (distributed transactions)|link]]) used in distributed microservices ([[Backend Engineering - Distributed systems|link]]).

In case of partial failures (some operations succeeded and some failed), in the Saga pattern we use compensating actions which can cancel actions performed earlier. 
# Example
For example, when we have services like:
- Order Service → create order
- Payment Service → charge card
- Inventory Service → reserve stock

and service 3 failed - product can't be sent, then we can perform as compensating steps - return money and cancel order.
# Two types
- [[Software Engineering - Saga pattern - Choreography (event-driven) type]]
- [[Software Engineering - Saga pattern - Orchestration type]]
