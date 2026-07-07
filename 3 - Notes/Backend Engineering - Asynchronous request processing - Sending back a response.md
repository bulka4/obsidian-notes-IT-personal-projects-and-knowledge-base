Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
When using asynchronous request processing ([[Backend Engineering - Asynchronous request processing|link]]), worker processes executes tasks sent by the API server and for sending back response, there are a few patterns:
- Pooling - [[Backend Engineering - Asynchronous request processing - Sending back a response using pooling|link]] 
- Webhook (callback) - [[Backend Engineering - Asynchronous request processing - Sending back a response using webhook (callback)|link]] 
- Push via WebSockets (real-time) - [[Backend Engineering - Asynchronous request processing - Sending back a response using WebSockets|link]] 
- Return via shared storage - [[Backend Engineering - Asynchronous request processing - Sending back a response via shared storage|link]] 