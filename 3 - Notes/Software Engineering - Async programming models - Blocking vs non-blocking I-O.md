Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
blocking vs non-blocking I/O describes what happens when a program performs an input/output operation (reading a file, waiting for a network response, querying a database, etc.).
# Blocking I/O
The program waits until the operation finishes.

While waiting:
- the thread is blocked
- it cannot do other work
- CPU may sit idle

Advantages:
- simple programming model
- easier to understand and debug

Disadvantages:
- inefficient when many operations wait (e.g., thousands of network connections)
- often requires many threads to handle concurrency

Example:
- A web server creates one thread per request. If 10,000 clients wait for responses, you may need 10,000 threads.
# Non-blocking I/O
The program **starts an operation and continues doing other work**. It checks later whether the operation finished or receives a notification.

For example:
```
socket.receive_async(callback)
do_other_work()
```
the program:
1. starts reading data
2. continues executing
3. gets notified when data is available

Advantages:
- handles many concurrent operations efficiently
- fewer threads needed
- better resource usage

Disadvantages:
- more complex programming model
- harder error handling and debugging

Example:
- A modern event-driven server (like Node.js or systems using `epoll`/`kqueue`) can handle thousands of connections with a small number of threads.