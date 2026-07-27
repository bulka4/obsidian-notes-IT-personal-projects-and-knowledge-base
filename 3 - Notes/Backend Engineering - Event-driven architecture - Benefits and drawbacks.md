Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Benefits and drawbacks of event-driven systems ([[Backend Engineering - Event-driven architecture (EDA)|link]]):
# Benefits
## Decoupling services
Service sends an message to the message broker and doesn't have to know about other services which will receive this request.

We can add another service that will receive this message without changing the `Order` service which sends messages.
## Better scalability and fault tolerance
If one service that receives messages is slow or crashes, it doesn't affect the service that sends messages. It can continue sending messages without waiting for a response.
# Drawbacks
- More complex debugging and consistency handling