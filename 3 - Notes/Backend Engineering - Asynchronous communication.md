Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Asynchronous communication is a communication where one service sends a message to another one, doesn't wait for a response and can continue with other tasks.

This allows to keep independent the service that emits an event and services that process it.

Note that a service normally can send multiple requests simultaneously so asynchronous communication doesn't help with a situation when an entire service waits for a single request to receive a response but with a situation when a single request waits for a response (e.g. a user makes a request and only that one user needs to wait for a response).

When a single request is made using asynchronous communication, it doesn't wait for the request to be fully processed but immediately receives a response confirming that the request has been submitted and once it is processed, a final response will be sent back later (or saved in some database).

Architectures for obtaining asynchronous communication include:
- Event-driven systems ([[Backend Engineering - Event-driven architecture (EDA)|link]])
- Asynchronous request processing ([[Backend Engineering - Asynchronous request processing|link]])
# Related topics
- Synchronous communication - [[Backend Engineering - Synchronous communication|link]] 
- Asynchronous request processing - [[Backend Engineering - Asynchronous request processing|link]] 