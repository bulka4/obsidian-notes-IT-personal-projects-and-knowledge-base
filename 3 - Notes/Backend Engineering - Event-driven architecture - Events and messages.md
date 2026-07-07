Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Events and messages are used in asynchronous communication ([[Backend Engineering - Asynchronous communication|link]]):
- An event represents something that happened 
	- For example order created, transaction made
- A message carries information about an event and is sent from one service to another
	- For example, the `Orders` service creates an order (that's an event) and sends a message about that event to the `Payment` service
- With an event there is often a database update related to it
	- For example, after creating an order, data about it is saved in a database