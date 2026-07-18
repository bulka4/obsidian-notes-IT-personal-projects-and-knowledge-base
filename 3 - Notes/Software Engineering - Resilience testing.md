Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Resilience testing** checks whether a system can **continue operating and recover when failures happen**.

The question:
> "How well does the system handle things going wrong?"

It is closely related to reliability testing, but focuses more specifically on **failure handling and recovery**.
# Examples
## Service failure
A microservice crashes:
```
Order Service
      |
      X
Payment Service crashes
```

Resilience test checks:
- Does the system retry correctly?
- Does it return a graceful error?
- Are requests queued?
- Does it recover automatically?
## Database failure
```
Application
    |
Primary Database ❌
    |
Replica Database ✅
```

Test:
- Does failover happen?
- Is data lost?
- How long does recovery take?
## Network problems
Simulate:
- high latency
- packet loss
- temporary disconnections

Check:
- timeouts work
- retries do not overload the system
- services degrade gracefully
