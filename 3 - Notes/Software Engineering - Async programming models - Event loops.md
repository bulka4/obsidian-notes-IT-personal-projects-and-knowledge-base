Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
An event loop is a mechanism that allows a program to run asynchronous tasks efficiently by repeatedly checking for events and executing tasks when they are ready.

It is the core component behind many async programming systems.
# Basic idea
Instead of having a thread wait for I/O:
```
data = database.query()  # thread waits here
process(data)
```

the program uses an event loop:
```
Event loop
    |
    ├── Task 1: waiting for database response
    ├── Task 2: waiting for HTTP response
    ├── Task 3: ready to run
    |
    └── execute Task 3
```

When a task needs to wait (for example, for network data), the event loop pauses that task and runs another one.
# Main components
1. **Event queue**
    - Stores events/tasks that are ready to execute.
    - Example:
        - "HTTP response received"
        - "Timer finished"
        - "File read completed"
2. **Event loop**
    - Continuously checks the queue.
    - Runs callbacks/coroutines when they are ready.
3. **Async tasks/coroutines**
	- Functions that can pause and resume.
# Event loop vs threads
Traditional threads:
```
Thread 1 → Request A → waiting
Thread 2 → Request B → waiting
Thread 3 → Request C → processing
```

Many threads are blocked.

Event loop:
```
Single thread:
    Request A → waiting
    Request B → waiting
    Request C → processing
```

The same thread switches between tasks.