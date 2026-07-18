Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Concurrency is the ability of a system to manage multiple tasks by switching between them (stop one task to progress on another one) or executing them simultaneously.
# Parallelism
Parallelism is a type of concurrency and it is ability of a system to work on different tasks at the same time using for example two different CPU cores.
# Why use concurrency?
To efficiently handle things that spend time waiting:
- network requests
- disk I/O
- database queries
- user requests
- messages from brokers
# Common concurrency mechanisms
- threads
- processes
- async/await
- coroutines
- actors
- event loops
# Related topics
2. [[Software Engineering - Concurrency - Critical section]]
3. [[Software Engineering - Concurrency - Shared resources]]
4. [[Software Engineering - Concurrency - Locks]]
	1. [[Software Engineering - Concurrency - Mutex]]
	2. [[Software Engineering - Concurrency - Read-write lock]]
	3. [[Software Engineering - Concurrency - Distributed lock]]
5. [[Software Engineering - Concurrency - Condition variables]]
6. [[Software Engineering - Concurrency - Semaphores]]
7. [[Software Engineering - Concurrency - Monitors]]
8. [[Software Engineering - Concurrency - Actor model]]
9. [[Software Engineering - Concurrency - Async programming models]]
10. [[Software Engineering - Concurrency - Synchronization bugs]]
	1. [[Software Engineering - Concurrency - Race conditions]]
	2. [[Software Engineering - Concurrency - Deadlocks]]
11. [[Software Engineering - Concurrency - Deterministic schedulers]]