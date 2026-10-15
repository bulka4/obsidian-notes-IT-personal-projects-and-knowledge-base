Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Both stateful and stateless services have a state ([[Software Engineering - State|link]]) but the difference is about whether the service keeps information about previous interactions (handled requests) inside the service itself (not in an external database) and uses it to handle further requests:
- If yes, then it is a stateful service
- If not, then it is a stateless service

If the service retrieves data needed to handle requests from an external database, then it is stateless and that database is stateful. Even though that service relies on the information from previous handled requests to handle further requests, it is stateless because that information lives outside of that service, in an external database.
# Benefits
Stateless design is beneficial because it:
- Enables horizontal scaling
	- When we create a new instance of a service, we don't need to load the state from the previous instances.
- Makes load balancing simpler
	- In a stateful design, a request must go to the instance that has a proper state, with the information needed to handle that request
- Avoids server-side session coupling
	- That is avoids a situation where a backend service depends on a stored session state on a specific service instance to understand or continue user’s interaction.
	- So a user can start interaction with one service instance and later continue it with another instance