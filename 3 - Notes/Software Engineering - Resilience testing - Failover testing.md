Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Failover testing** verifies that a system can **automatically switch from a failed component to a backup component** and continue operating.

The question:
> "If the primary component fails, does the backup take over correctly?"
# Examples
## Database failover
Normal:
```
Application
     |
     v
Primary Database
     |
     v
Replica Database
```

Test:
```
Primary Database ❌
        ↓
Replica becomes primary
        ↓
Application continues working
```

Check:
- failover happens automatically
- no or minimal downtime
- data is not lost
- clients reconnect correctly
## Server failover
Before:
```
Load Balancer
      |
      +-- Server A ✅
      +-- Server B ✅
```

Failure:
```
Server A ❌
```

Expected:
```
Load Balancer
      |
      +-- Server B ✅
```

Users should not notice the failure.
## Kubernetes example
```
Pod A ❌
    ↓
Kubernetes detects failure
    ↓
Creates new Pod A
    ↓
Traffic continues
```

# Important metrics
- **Failover time** — how long switching takes
- **Availability** — whether the service remains accessible
- **Data consistency** — whether state is preserved

Example:
```
Database failure:
10:00:00  Primary crashes
10:00:15  Replica promoted
10:00:20  Application reconnects
```

Failover time = ~20 seconds