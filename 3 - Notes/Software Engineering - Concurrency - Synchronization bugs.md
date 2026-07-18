Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Synchronization bugs** are bugs caused by incorrect coordination between concurrent operations (threads, processes, coroutines, distributed nodes).

Types of synchronization bugs. include:
- Race conditions ([[Software Engineering - Concurrency - Race conditions|link]])
- Deadlocks  ([[Software Engineering - Concurrency - Deadlocks|link]])
- Lost notification
- Incorrect lock usage
- Visibility problems
# Lost notification
Example:
```
Thread A:
signal "work finished"

Thread B:
starts waiting AFTER the signal
```

As a result, thread B waits forever.
# Incorrect lock usage
Example:
```
Acquire lock
Throw exception
Forget to release lock
```

As a result, other threads become blocked.
# Visibility problems
One thread updates a variable, but another thread does not see the new value because of memory caching or missing synchronization.

Example:
```
Thread A:
done = true

Thread B:
while (!done) { ... }
```

Thread B may never observe the update.