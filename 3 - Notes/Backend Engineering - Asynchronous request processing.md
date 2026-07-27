Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Asynchronous request processing is an architecture where:
- Client submits a request to one service (API Gateway).
- Service immediately responds with something like `202 Accepted`.
- API Gateway sends a request to another service (worker) which does the hard work in the background.
# Related topics
- Benefits and drawbacks - [[Backend Engineering - Asynchronous request processing - Benefits and drawbacks|link]] 
- Message queue - [[Backend Engineering - Asynchronous request processing - Message queue|link]] 
- Sending back a response - [[Backend Engineering - Asynchronous request processing - Sending back a response|link]] 