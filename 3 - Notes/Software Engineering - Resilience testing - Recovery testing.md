Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Recovery testing** checks whether a system can **restore normal operation after a failure**.

The question:
> "After something breaks, can the system recover correctly and how long does it take?"
# Examples
## Server crash
Test:
```
Application server crashes
        ↓
Restart server
        ↓
Check system behavior
```

Verify:
- service starts correctly
- users can continue working
- no data is lost
## Database failure
Test:
```
Primary database fails
        ↓
Switch to backup/replica
        ↓
Restore normal operation
```

Check:
- failover works
- data consistency is preserved
- recovery time is acceptable
## Data pipeline failure
Example:
```
Spark job fails halfway
        ↓
Restart job
        ↓
Pipeline completes without duplicates
```

Check:
- checkpoints work
- failed tasks can retry
- state is restored
# Important recovery metrics
## RTO (Recovery Time Objective)  
How quickly must the system recover?

Example:
```
Service must recover within 5 minutes
```
## RPO (Recovery Point Objective)  
How much data loss is acceptable?

Example:
```
Maximum acceptable data loss: 5 minutes of data
```