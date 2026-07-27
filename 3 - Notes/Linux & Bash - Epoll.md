Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]] [[_Software_Engineering]]
#InfrastructureEngineering #LinuxBash #SoftwareEngineering 

# Introduction
**`epoll`** is a Linux kernel mechanism for efficiently monitoring many I/O events ([[Software Engineering - I-O events|link]]) at once (especially events related to network sockets ([[Networking - Network Socket|link]])).

It is commonly used to build high-performance event loops.
# Example - sockets
## Problem
A problem with sockets is that a server may have thousands of connections (sockets):
```
Socket 1 → waiting for data
Socket 2 → waiting for data
Socket 3 → ready
...
Socket 10000 → waiting
```

Checking every socket repeatedly is inefficient.
## `epoll` solution
The program tells the kernel:
> "Notify me when any of these sockets is ready."

The kernel tracks them and returns only the sockets that have events (state of a socket has changed).

Flow:
```
Application
    |
    | register sockets
    ↓
  epoll
    |
    | wait for events
    ↓
Kernel returns:
  - socket 3 has data
  - socket 500 has a connection
```

The event loop then processes those ready sockets.
# Why it matters
- Scales to thousands/millions of connections.
- Avoids constantly polling every connection.
- Used by systems like:
    - Nginx
    - Node.js (through libuv)
    - many Linux network servers