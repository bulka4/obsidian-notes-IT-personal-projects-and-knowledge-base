Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Websockets ([[Networking - Protocols - WebSockets|link]]) can be used for sending back a response in asynchronous request processing ([[Backend Engineering - Asynchronous request processing - Sending back a response|link]]).

It works like this:
- Client sends a request to a worker
- Client keeps a connection open
- Worker pushes result when ready

It is used for example in:
- dashboards
- live updates
- chat apps