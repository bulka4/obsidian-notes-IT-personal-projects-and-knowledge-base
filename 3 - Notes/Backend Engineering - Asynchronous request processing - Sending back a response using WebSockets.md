Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Websockets ([[Networking - Protocols - WebSockets|link]]) can be used for sending back a response in asynchronous request processing ([[Backend Engineering - Asynchronous request processing - Sending back a response|link]]).

It works like this:
- Client sends a request to a worker over a connection
- Client keeps that connection open
- Worker pushes result when ready using the same connection

It is used for example in:
- dashboards
- live updates
- chat apps