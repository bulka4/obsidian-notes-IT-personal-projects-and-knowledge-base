Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Locks are mechanisms that control access to shared resources ([[Software Engineering - Concurrency - Shared resources|link]], e.g. data in memory) when multiple threads/processes execute concurrently.

A lock ensures only one thread/task ([[Software Engineering - Threads|link]]) is allowed to execute a critical section ([[Software Engineering - Concurrency - Critical section|link]] , a sensitive piece of code) at a time:
```
lock.acquire()

# modify shared resource

lock.release()
```
# Example
Two threads update the same data at the same time → race condition ([[Software Engineering - Concurrency - Race conditions|link]]).
```
Thread A: read balance = 100
Thread B: read balance = 100
Thread A: subtract 50 → save 50
Thread B: subtract 30 → save 70
```

The correct result should be 20, but one update was lost.
# Common types
- Mutex (mutual exclusion lock) ([[Software Engineering - Concurrency - Mutex|link]])
- Read-write lock ([[Software Engineering - Concurrency - Read-write lock|link]])
- Distributed lock ([[Software Engineering - Concurrency - Distributed lock|link]])
# Problems
- Deadlock ([[Software Engineering - Concurrency - Deadlocks|link]]): two threads wait forever for each other's locks.
    ```
    Thread A holds Lock 1 → waits for Lock 2
    Thread B holds Lock 2 → waits for Lock 1
    ```
- Lock contention: many threads wait for the same lock, reducing performance.
- Starvation: one thread never gets the lock because others keep acquiring it.