Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
The Reactor pattern is an **event-driven design pattern** used to handle many concurrent I/O operations efficiently.

It is the architectural pattern that connects ideas like **sockets, non-blocking I/O, event loops, and `epoll`**.
# Basic idea
A **reactor** waits for events and dispatches them to handlers:
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

Instead of:
```
Thread 1 → wait for socket 1
Thread 2 → wait for socket 2
Thread 3 → wait for socket 3
```

one thread can manage many connections.
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
# Main components
- **Event demultiplexer**
    - OS mechanism that waits for events
    - Examples:
        - Linux: `epoll`
        - macOS: `kqueue`
        - Windows: IOCP
- **Reactor**
    - Event loop that receives events and dispatches work
- **Handlers**
    - Application code that processes events
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