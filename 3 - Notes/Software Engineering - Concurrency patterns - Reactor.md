Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The Reactor pattern is an event-driven design pattern used to handle many concurrent I/O operations ([[Software Engineering - I-O operations|link]]) efficiently.

It is the architectural pattern that connects ideas like sockets ([[Networking - Network Socket|link]]), non-blocking I/O ([[Software Engineering - Blocking vs non-blocking I-O|link]]), event loops ([[Software Engineering - Async programming models - Event loops|link]]), and `epoll` ([[Linux & Bash - Epoll|link]]).
# Basic idea
Instead of having one thread per socket, where each thread ([[Software Engineering - Threads|link]]) waits for some event related to one socket (e.g. data arriving through that socket):
```
Thread 1 → wait for socket 1
Thread 2 → wait for socket 2
Thread 3 → wait for socket 3
```

we can use the reactor pattern to create less threads than the number of sockets (it can be one or multiple threads but it is independent on number of sockets) that waits for events and dispatches them to handlers that process those events:
```
              Events
                |
                ↓
          Reactor / Event Loop
                |
     ┌──────────┼──────────┐
     ↓          ↓          ↓
 Handler A  Handler B  Handler C
(socket 1) (socket 2) (socket 3)
```
# Components
## Event loop (Reactor)
The reactor pattern is also called an event loop because it performs the same actions repeatedly:
- waits for I/O events
- determines which events occurred
- dispatches them to handlers
- repeat the process
## Handlers
Handlers are application code that processes events.
## Event demultiplexer
- OS mechanism that waits for events
- Examples:
	- Linux: `epoll`
	- macOS: `kqueue`
	- Windows: IOCP
# Threads
What threads ([[Software Engineering - Threads|link]]) do we have in the reactor pattern and what operations they represent:
- Our program, which implements the reactor pattern, creates one or multiple threads that represent executing the reactor pattern (the entire pattern i.e. an event loop plus handlers).
- There are two operations that can be executed as a single or separate threads:
	- Running the event loop (listening to events and calling handlers)
	- Running a handler
# Example flow
A web server:
1. Reactor registers sockets with `epoll`
2. `epoll` tells the reactor:
    - "socket 42 has incoming data"
3. Reactor calls the correct handler:
    - "HTTP request received → process it"
```
Client request
      ↓
Socket
      ↓
epoll detects event
      ↓
Reactor event loop
      ↓
HTTP handler
```
# Where it is used
- Nginx
- Node.js (internally through libuv)
- Netty (Java networking framework)
- High-performance servers

Relationship between concepts:
```
Sockets
   ↓
Non-blocking I/O
   ↓
Event demultiplexer (epoll)
   ↓
Reactor pattern
   ↓
Async/event-driven server
```
