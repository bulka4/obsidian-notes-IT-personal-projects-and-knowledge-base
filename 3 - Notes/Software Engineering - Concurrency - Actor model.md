Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The Actor model is a concurrency model where the basic unit of computation is an actor.

An actor is an independent entity (an abstract object) that:
- has its own private state,
- processes messages one at a time,
- communicates with other actors only by sending messages.

An actor is an abstraction above threads and processes:
- many actors can share a small number of threads
- many actors can run inside one process, or actors can be distributed across processes/machines

There is no shared data that multiple threads may want to access but there are actors sending messages to each other instead.
# Key ideas
- No shared memory → actors do not directly access each other's data.
- Message passing → actors communicate by sending messages.
- Single-threaded processing per actor → an actor handles one message at a time, avoiding many race conditions.