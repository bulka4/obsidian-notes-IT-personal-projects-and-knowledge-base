Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Asynchronous (async in short) programming is a concurrency model where a program can pause an operation when it waits for something and start another operation to progress in a meantime.

For example, when one operation is waiting to get data from a database, in a meantime the program can start another operation and get back to the previous operation once data from a database is loaded and another started operation is paused / finished.

We don't have to use here multiple threads / processes but it can happen within a single thread.
# Coroutines & tasks
In async programming ([[Software Engineering - Async programming models|link]]):
- **Tasks** are operations that can be paused and resumed later
- **Coroutines** are functions defining those tasks

When a coroutine pauses (e.g. because it waits to load data from a database), another coroutine within the same event loop ([[Software Engineering - Async programming models - Event loops|link]]) can progress with its tasks.

More info is here - [[Software Engineering - Async programming models - Coroutines & tasks]].
# Event loop
In async programming ([[Software Engineering - Async programming models|link]]), we can run coroutines / tasks ([[Software Engineering - Async programming models - Coroutines & tasks|link]]) only within an event loop. Event loop coordinates tasks - decides which one to run.

When one coroutine waits for something, then it can be paused and another coroutine can be started by the event loop (so both coroutines needs to be within a single event loop).

If we have multiple event loops, then their tasks can run independently, and they can run in parallel (if there are multiple CPU cores).

More info is here - [[Software Engineering - Async programming models - Event loops]].
# Related topics
1. [[Software Engineering - Async programming models - Coroutines & tasks]]
2. [[Software Engineering - Async programming models - Event loops]]
3. [[Software Engineering - Async programming model vs multiple threads]]