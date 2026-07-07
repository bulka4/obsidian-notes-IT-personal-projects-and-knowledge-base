Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In asynchronous request processing ([[Backend Engineering - Asynchronous request processing|link]]), a message queue is used to store HTTP requests from an API server for later processing.

API server converts incoming HTTP requests into a job entry which is then stored in a message queue.

This queue can be:
- in-memory queue (simple systems)
- Redis queue
- database table
- dedicated job system (e.g. background job runner)