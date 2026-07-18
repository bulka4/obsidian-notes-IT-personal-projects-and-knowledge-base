Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Soak testing** (also called **endurance testing**) checks whether a system remains stable under a normal workload for a long period of time.

The question:
> "Does the system keep working after running continuously for hours, days, or weeks?"
# Example 1
```
Run API with normal traffic for 7 days

Monitor:
- memory usage
- CPU usage
- errors
- response time
```

It helps find:
- memory leaks
- resource exhaustion
- gradual performance degradation
- connection leaks
# Example 2
```
Start:
Memory = 2 GB

After 3 days:
Memory = 8 GB

After 7 days:
Service crashes
```

This indicates a memory leak.

Soak testing is mainly about **long-term stability**, not maximum capacity.