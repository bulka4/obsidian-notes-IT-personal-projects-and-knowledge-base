Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
A stateful service is such a service which has a state - i.e. an information needed for that service to work properly, stored in some storage system.

A stateless service is a service which also has a state but it doesn't store client/session-specific data between requests.

For example, a state might contain an information about:
- Logged in users
- Database connections
- Cached data
- Loaded models / in-memory structures

and when a user wants to perform some action, the service checks in its state whether or not that user is logged in.
# Benefits
Stateless design is beneficial because it:
- Enables horizontal scaling
	- When we create a new instance of a service, we don't need to load the state from the previous instances.
- Makes load balancing simpler
	- In a stateful design, a request must go to the instance that has a proper state (with an information needed) to handle that request
- Avoids server-side session coupling
	- That is avoids a situation where a backend service depends on a stored session state on a specific service instance to understand or continue a user’s interaction.