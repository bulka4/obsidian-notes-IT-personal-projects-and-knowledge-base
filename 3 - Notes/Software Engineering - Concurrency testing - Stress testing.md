Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Stress testing verifies how a system behaves under extreme load or conditions beyond normal usage.

It tries to find failures caused by high resource usage, such as:
- too many users/requests
- many concurrent threads
- large amounts of data
- high CPU or memory usage

Example:
```
Normal:
1,000 requests/sec → works ✅

Stress test:
100,000 requests/sec → observe behavior
```

The test checks:
- does the system fail gracefully?
- does it recover after the load decreases?
- are there memory leaks?
- do timeouts, crashes, or data corruption occur?

In concurrent code testing:
```
Create many threads
        ↓
Run operations simultaneously
        ↓
Look for:
- race conditions
- deadlocks
- synchronization bugs
```