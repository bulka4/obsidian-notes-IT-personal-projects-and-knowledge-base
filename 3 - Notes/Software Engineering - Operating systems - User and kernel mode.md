Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
User mode and kernel mode are two privilege levels of the CPU that separate normal applications from the operating system.

The idea is protection: applications should not be able to directly control hardware or damage the system.
# User mode
- Where normal applications run.
- Has limited privileges.
- Cannot directly:
    - access hardware
    - modify memory belonging to other programs
    - execute sensitive CPU instructions
    - communicate directly with devices

Examples running in user mode:
- Web browser
- Python program
- Database application
- Text editor
# Kernel mode
- Where the operating system core runs.
- Has full privileges.
- Can:
    - access hardware
    - manage memory
    - create and terminate processes
    - communicate with devices
    - schedule CPU time
# Examples running in kernel mode
- Linux kernel
- Windows kernel
- Device drivers
# Examples: Reading a file
When a program reads a file, then the flow is:
1. Python program runs in user mode.
2. It calls the OS function (`open()` system call).
3. CPU switches to kernel mode.
4. Kernel:
    - checks permissions
    - finds the file on disk
    - asks the disk driver to read data
5. Kernel returns the result.
6. CPU switches back to **user mode**.
7. Python program continues.
```
+------------------------+
| Application            |
| (Python, browser)      |
|                        |
|       User mode        |
+------------------------+
          |
          | system call
          ↓
+------------------------+
| Operating System       |
| (kernel)               |
|                        |
|      Kernel mode       |
+------------------------+
          |
          ↓
+------------------------+
| Hardware               |
| Disk, CPU, memory      |
+------------------------+
```