Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
There are two approaches that we can use:
- Create multiple threads each one executing different operation
- Create one thread which executes different operations one by one in an event loop ([[Software Engineering - Async programming models - Event loops|link]])
# Multiple threads
Using multiple threads, each operation might be executed by a different thread:
```
Thread 1 → operation A → waiting
Thread 2 → operation B → waiting
Thread 3 → operation C → processing
```

**Pros:**
- Different threads can run in parallel if we have multiple CPU cores
- Simple programming model (normal sequential code).
- The OS manages scheduling.
- A blocked thread does not block other threads.
- Good when you have a moderate number of concurrent tasks.

**Cons:**
- Threads consume memory (each has its own stack).
- Creating/managing many threads by OS has overhead.
- Thousands of threads become difficult to manage.
- Shared memory creates synchronization problems:
    - race conditions,
    - locks,
    - deadlocks.
# Event loop
Using async programming, a single thread can handle multiple operations - it executes one operation at a time but it can switch between operations - pause one operation and progress with another one:
```
Single thread:
    operation A → waiting
    operation B → waiting
    operation C → processing
```

**Pros:**
- Very lightweight (thousands of coroutines are possible).
- No need for many threads.
- Less shared-state complexity.
- Very efficient for I/O-heavy applications.

**Cons:**
- Code is more complex if you are not familiar with async.
- All code must cooperate (`await` points).
- One blocking operation can block the whole event loop.
- Not good for CPU-heavy tasks.
# Typical use cases
**Threads:**
- background jobs,
- applications with fewer concurrent operations,
- mixed workloads,
- when simplicity is important.

**Async/event loop:**
- web servers,
- APIs with many simultaneous users,
- chat systems,
- proxy servers,
- applications making many external API calls.