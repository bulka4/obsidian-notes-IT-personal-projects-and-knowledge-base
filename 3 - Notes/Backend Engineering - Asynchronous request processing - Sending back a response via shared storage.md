Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
A shared storage can be used for sending back a response in asynchronous request processing ([[Backend Engineering - Asynchronous request processing - Sending back a response|link]]).

- Client sends a request to the worker to process
- Worker processes it and saves results in a shared storage
- Client can read the result whenever they want