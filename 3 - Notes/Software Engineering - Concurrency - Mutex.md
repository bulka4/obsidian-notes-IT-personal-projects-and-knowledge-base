Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A mutex (mutual exclusion lock) is a type of lock ([[Software Engineering - Concurrency - Locks|link]]) that allows only one thread to enter a critical section ([[Software Engineering - Concurrency - Critical section|link]]) at a time.

The idea:
- A shared resource can be modified by multiple threads.
- A mutex acts like a gate.
- A thread must **acquire** the mutex before entering the critical section.
- After finishing, it **releases** the mutex.
# Example
```python
mutex.acquire()

# critical section
balance = balance - 50

mutex.release()
```

With two threads:
```
Thread A                  Thread B

acquire mutex
    |
    v
modify balance
    |
release mutex
                          acquire mutex
                              |
                              v
                         modify balance
```

Thread B must wait while Thread A holds the mutex.
# Example resources protected by a mutex
- a counter in memory
- a list/map shared between threads
- a file being written
- an in-memory cache