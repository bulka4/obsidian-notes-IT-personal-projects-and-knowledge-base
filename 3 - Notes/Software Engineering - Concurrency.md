Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
Concurrency is the ability of a system to manage multiple tasks using:
- Asynchronous programming - switching between tasks. Stop one task when it waits for something (e.g. to finish reading data from a database) and progress on another one in the meantime
- Parallelism - execute tasks simultaneously using different CPU cores or servers.

It can refer to multiple threads or processes executing tasks within a single application, or to multiple separate applications.
# Important definitions
- **Threads and processes** - Threads ([[Software Engineering - Threads|link]]) and processes are one way to implement concurrency. While one thread / process is waiting for something and is idle, another thread / process can process on another task.
- **Shared resources** ([[Software Engineering - Concurrency - Shared resources|link]]) - a resource that multiple execution paths (threads/processes/services) can access and potentially interfere with each other over
- **Critical section** ([[Software Engineering - Concurrency - Critical section|link]]) - a piece of code (a section of instructions) that accesses or modifies a shared resource.
# Locks
Locks are mechanisms that control access to shared resources ([[Software Engineering - Concurrency - Shared resources|link]], e.g. data in memory) when multiple threads or processes execute concurrently. This can refer to processes within a single application or to multiple applications.

A lock ensures only one thread/task ([[Software Engineering - Threads|link]]) is allowed to execute a critical section ([[Software Engineering - Concurrency - Critical section|link]] , a sensitive piece of code) at a time.

More information can be found here - [[Software Engineering - Concurrency - Locks]].
# Semaphores
A semaphore is a synchronization mechanism that controls how many execution paths ([[Software Engineering - Execution path|link]]) / threads / services can access a resource at the same time. This can refer to threads within a single application or to multiple applications.

More information can be found here - [[Software Engineering - Concurrency - Semaphores]].
# Synchronization bugs
Synchronization bugs are bugs caused by incorrect coordination between concurrent operations (threads, processes, coroutines, distributed nodes).

Types of synchronization bugs. include:
- Race conditions ([[Software Engineering - Concurrency - Race conditions|link]]) - multiple concurrent operations access and modify shared data, and the final result depends on the timing or order in which those operations execute. 
	- This can refer to operations within a single application or to multiple applications.
- Deadlocks  ([[Software Engineering - Concurrency - Deadlocks|link]]) - two or more concurrent operations are waiting for each other to release resources (locks), so none of them can continue. 
	- This can refer to operations within a single application or to multiple applications.
	- For example:
	  ```
		Thread A:
		Holds Lock 1
		Waits for Lock 2
		
		Thread B:
		Holds Lock 2
		Waits for Lock 1
	  ```
# Other topics
1. [[Software Engineering - Concurrency - Condition variables]]
2. [[Software Engineering - Concurrency - Monitors]]
3. [[Software Engineering - Concurrency - Actor model]]
4. [[Software Engineering - Concurrency - Deterministic schedulers]]
# Related topics
1. [[Software Engineering - Concurrency - Parallelism]]
2. [[Software Engineering - Concurrency - Threads & processes]]
3. [[Software Engineering - Concurrency - Shared resources]]
4. [[Software Engineering - Concurrency - Critical section]]
5. [[Software Engineering - Concurrency - Locks]]
	1. [[Software Engineering - Concurrency - Mutex]]
	2. [[Software Engineering - Concurrency - Read-write lock]]
	3. [[Software Engineering - Concurrency - Distributed lock]]
6. [[Software Engineering - Concurrency - Condition variables]]
7. [[Software Engineering - Concurrency - Semaphores]]
8. [[Software Engineering - Concurrency - Monitors]]
9. [[Software Engineering - Concurrency - Actor model]]
10. [[Software Engineering - Concurrency - Synchronization bugs]]
	1. [[Software Engineering - Concurrency - Race conditions]]
	2. [[Software Engineering - Concurrency - Deadlocks]]
11. [[Software Engineering - Concurrency - Deterministic schedulers]]