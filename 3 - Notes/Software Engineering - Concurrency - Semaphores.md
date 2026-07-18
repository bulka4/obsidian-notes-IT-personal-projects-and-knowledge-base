Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A semaphore is a synchronization mechanism that controls how many execution paths can access a resource at the same time.

Unlike a mutex ([[Software Engineering - Concurrency - Mutex|link]]):
- Mutex → allows only one thread at a time.
- Semaphore → allows N threads at a time.
# Example
Limit access to a database connection pool with 5 connections.
```
Semaphore count = 5

Thread A → takes one slot (count = 4)
Thread B → takes one slot (count = 3)
Thread C → takes one slot (count = 2)
...
Thread F → waits (count = 0)
```

When a thread finishes:
```
Thread A releases slot (count = 1)
Thread F can continue
```
# Common uses
- Limit the number of concurrent requests.
- Control access to a limited resource (database connections, API rate limits, worker threads).
- Prevent too many tasks from running simultaneously.