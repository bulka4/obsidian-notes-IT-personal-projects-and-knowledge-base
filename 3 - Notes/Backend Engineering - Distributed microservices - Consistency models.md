Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Consistency models define how and when state changes become visible across the system (services) after a write. 

That state is data. Changed state means that data was inserted, updated or deleted.

In event-driven systems ([[Backend Engineering - Event-driven architecture|link]]):
- A state is a result of applying all the events emitted so far which can be:
	- a single value
	- a structured object
	- or a collection of records
- When an event is being emitted, that is a state change (change in the data which is a result of applying all events).

For example:
- User data gets updated in a database - That's a state change (data is a state).
- An event `OrderCreated` gets emitted - That's a state change and the current state is a result of applying all the events emitted so far, i.e. all the data about clients and their orders.

Different types include:
- Strong consistency - [[Backend Engineering - Consistency models - Strong consistency|link]] 
- Sequential consistency - [[Backend Engineering - Consistency models - Sequential consistency|link]] 
- Causal consistency - [[Backend Engineering - Consistency models - Causal consistency|link]] 
- Eventual consistency - [[Backend Engineering - Consistency models - Eventual consistency|link]] 
- Weak consistency - [[Backend Engineering - Consistency models - Weak consistency|link]] 
- Read-your-writes consistency - [[Backend Engineering - Consistency models - Read-your-writes  consistency|link]] 
- Monotonic reads consistency - [[Backend Engineering - Consistency models - Monotonic reads consistency|link]] 
- Session consistency - [[Backend Engineering - Consistency models - Session consistency|link]] 