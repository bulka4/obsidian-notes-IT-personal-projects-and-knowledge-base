Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Partial failures happen when some parts of a distributed system ([[Backend Engineering - Distributed systems|link]]) fail while others keep working.

For example, user request goes through multiple services like this:
```
API Gateway → Order Service → Payment Service → Inventory Service
```
And only the Payment Service doesn't work.
# Core consequences
Partial failures lead to:
1. Inconsistent state
	- payment succeeded but order not updated
 2. Duplicate operations
	- retries after timeout
 3. Lost operations (if not designed well)
	- request succeeds but response lost
# How systems handle partial failures
1. Data Consistency Patterns ([[Backend Engineering - Distributed systems - Data Consistency Patterns (distributed transactions)|link]])
2. Timeouts - Never wait forever.
3. Retries (with backoff + jitter, [[Software Engineering - Handling failures - Retries with backoff|link]]) - But must be idempotent.
4. Circuit breaker ([[Software Engineering - Handling failures - Circuit breakers|link]]) - Stop calling failing service temporarily.
5. Bulkhead isolation ([[Software Engineering - Handling failures - Bulkheads|link]]) - Prevent one failure from taking down everything.
6. Idempotency ([[Backend Engineering - Event-driven architecture - Idempotency|link]]) - Ensures retries don’t corrupt state.