Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Lamport logical clock is an example of a logical clock ([[Backend Engineering - Distributed microservices - Logical clocks (timestamps)|link]]).
# Happened-before relation
Lamport introduced a relation:
```
a -> b
```
which means that event `a` happened before event `b`. This relation is based on causality, not physical time.

Rules:
## Same process
If events `a` and `b` happened on the same machine and `a` happened first, then `a -> b`
## Message passing
If one server sends a message (that's event `a`) to another server (event `b` is another server reading this message), then `a -> b`
## Transitivity
If `a -> b` and `b -> c`, then `a -> c`
## Concurrent events
If two events happen on two different servers and there are no messages sent between them, then we consider that neither happened before the other, there is no order and we write:
  ```
a -> /b
b -> /a
  ```
	
Both events are concurrent.
# Lamport clocks / timestamps
Each process keeps a logical counter. It starts with 0.

Rules:
## Rule 1
Before every local event, we increase the counter by 1.
## Rule 2
When sending a message, increase the counter by 1 and attach the counter value to the message as a timestamp.
## Rule 3
When receiving a message, set the counter to:
```
max(local_clock, message_timestamp)
```
where:
- `local_clock` - A local counter of the process
- `message_timestamp` - A value of the counter attached to the message when sending it
# Causality implies timestamp ordering
An important property is that causality implies timestamp ordering, so if `a -> b`, then `L(a) < L(b)` where `L(event)` is a Lamport timestamp (value of the logical counter).

But the opposite is not true, so when `L(a) < L(b)`, it doesn't mean that `a -> b`.
# Use cases
Logical clocks are useful for:
- event ordering
- replication
- distributed logs
- conflict resolution
- leader election algorithms
# Problems
A problem with this method is that we can't distinguish causal order from coincidental ordering, i.e. we can't determine what was a real order of all events across all the servers.

That's because we might have a situation when `L(a) < L(b)` and `b -> a` (as explained in the "Causality implies timestamp ordering" section).
# Questions
- In total ordering, why do you say that we can create a total order we can't compare timestamps for different processes? How to compare (5, A) with (4, B)?