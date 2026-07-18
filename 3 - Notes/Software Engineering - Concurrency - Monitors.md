Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A monitor is a higher-level synchronization mechanism that combines:
1. A lock ([[Software Engineering - Concurrency - Locks|link]]) (to ensure only one thread executes protected code at a time)
2. Condition variables ([[Software Engineering - Concurrency - Condition variables|link]]) (to allow threads to wait for a specific condition)
3. Shared state (data) ([[Backend Engineering - Distributed systems - State|link]])
4. Methods (functions)

Its purpose is to control access to its internal state (shared data) and coordinate threads that tries to access or modify this state.

A monitor uses:
- Locks to ensure that only one thread can execute code that accesses the shared state at a time. Other threads wait if the lock is already held (i.e. if some other thread is already accessing the state)
- Condition variables to make a thread wait with accessing or modifying state until some condition is satisfied
# Example
A queue shared between producer and consumer - queue is a list containing messages from a producer to consumer.

Multiple threads may want to:
- add items to it (producers add a message for a consumer to process)
- remove items from it (consumers process a message)

A monitor contains this queue and methods for modifying it. For example, it can be a class like this:
```python
class BlockingQueue:
    queue = []
    mutex = ...
    not_empty = ...

    def put(item): # Add an item to the queue
        ...

	def get(): # Remove an item from the queue
        ...
```

The problem is when multiple threads try to modify the queue simultaneously. That can lead to race conditions ([[Software Engineering - Concurrency - Race conditions|link]]).

For example, two consumers might try to remove the same item from a queue at the same time and then:
- One consumer removes the item
- Another consumer tries to remove it but it is not there any more (already removed)

A monitor can:
- Use locks to cause that one consumer will wait with removing an item until another consumer finishes removing
- Use condition variables to make a consumer wait until some item appears in a queue when it tries to remove an item from an empty queue