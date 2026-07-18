Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
State is the information that describes the current condition of a system at a specific moment. It is a result of applying different operations in a system.

A system can be represented as:
```
Current state + operation → New state
```

Example:
```
State:
Bank account balance = $100

Operation:
Deposit $50

New state:
Bank account balance = $150
```

The state is the result of all the operations that happened before.
# Examples of state
## Application state
A web application:
```
State:
User is logged in
Shopping cart contains 3 items
```
## Application configuration
Application configuration is also a state.
## Database state
Database:
```
State:

Users table:
----------------
ID | Name
1  | Alice
2  | Bob
```

A change:
```
INSERT User(3, "John")
```

New state:
```
Users table:
----------------
1 | Alice
2 | Bob
3 | John
```
## Distributed system state
Multiple replicas:
```
Node A:
balance = $100

Node B:
balance = $100

Node C:
balance = $100
```

The distributed state is the state that all nodes should agree on.
## Event-driven systems
In event-driven systems ([[Backend Engineering - Event-driven architecture|link]]):
- A state is a result of applying all the events emitted so far which can be:
	- a single value
	- a structured object
	- or a collection of records
- When an event is being emitted, that is a state change (change in the data which is a result of applying all events).
# Related terms
- Operation / Command - An action that changes state
- Change - A modification to the state (difference between two states)
- Write - A request to modify stored state
- Commit - After a commit, a change becomes official and durable
- Replication - Keeping copies of a state
- State transition - A process of moving from one state to another
- Stateless and stateful service - [[Backend Engineering - Stateful vs stateless service|link]] 
- Operation log - An ordered list of all the operations performed in a system. The current state is a result of applying all those operations in sequence.
# Saving a write in a log, committing and applying it
There are three operations we need to distinguish:
- Saving a write in a log - Add information about the operation to perform to the log (which is like a to-do list)
- Committing a write - Making sure that information about a write is durable and will not be lost
- Applying a write - Implement the write operation to actually change the state