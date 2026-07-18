Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Reliability testing checks whether a system can operate correctly and consistently over time, including under failures and unexpected conditions.

The question:
> "Can the system keep working correctly for a long time?"

It focuses on dependability, not just speed.
# Examples
## Long-running service
Run an API for 7 days:
```
Requests:
1 billion

Check:
- crashes?
- memory leaks?
- increasing error rate?
- degraded performance?
```
## Distributed system
Simulate failures:
```
Database node fails
        ↓
System continues working
        ↓
Data is not lost
```

Check:
- failover works
- data consistency is preserved
- services recover
## Data pipeline
Run daily jobs for months:

Check:
- no missing data
- no duplicate processing
- retries work correctly
- corrupted inputs are handled