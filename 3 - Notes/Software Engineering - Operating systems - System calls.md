Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
System calls are the interface that allows a user program to request services from the operating system kernel.

A normal application cannot directly access hardware or critical resources (CPU control, memory management, disks, network devices), so it asks the OS through system calls.
# How system calls work
The flow is like this:
```
User application
      |
      | system call (e.g., read(), write())
      ↓
Operating system kernel
      |
      | interacts with hardware
      ↓
Hardware
```

and when a process wants to access critical resources (e.g. disk), it performs a system call:
- Application switches from user mode to kernel mode ([[Software Engineering - Operating systems - User and kernel mode|link]]).
- Kernel checks permissions and performs the disk operation.
- Kernel returns the result to the application.
- Program continues in user mode.
# Examples of system calls
- **Process management**
    - `fork()` — create a new process (Unix/Linux)
    - `exec()` — replace a process with another program
    - `exit()` — terminate a process
- **File operations**
    - `open()` — open a file
    - `read()` — read data
    - `write()` — write data
    - `close()` — close a file
- **Memory management**
    - `mmap()` — map memory
    - `brk()` — change process memory size
- **Networking**
    - `socket()` — create a network socket
    - `send()` / `recv()` — communicate over network