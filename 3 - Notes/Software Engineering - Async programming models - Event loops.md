Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
In async programming ([[Software Engineering - Async programming models|link]]), we can run coroutines / tasks ([[Software Engineering - Async programming models - Coroutines & tasks|link]]) only within an event loop. Event loop coordinates tasks - decides which one to run.

When one coroutine waits for something, then it can be paused and another coroutine can be started by the event loop (so both coroutines needs to be within a single event loop).

If we have multiple event loops, then their tasks can run independently, and they can run in parallel (if there are multiple CPU cores).
# Main components
## Event queue
Stores events/tasks that are ready to execute, for example:
- "HTTP response received"
- "Timer finished"
- "File read completed"
## Event loop
- Continuously checks the queue.
- Runs callbacks/coroutines when they are ready.
## Async tasks/coroutines
- Tasks are operations that can be paused and resumed
- Coroutines are functions defining tasks
- More info is here - [[Software Engineering - Async programming models - Coroutines & tasks|link]] 
# Threads in an event loop
Usually, in one event loop we run a single thread.