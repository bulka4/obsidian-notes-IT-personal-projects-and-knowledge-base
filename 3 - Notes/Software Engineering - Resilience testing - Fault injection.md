Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Fault injection** is a testing technique where you **intentionally introduce failures** into a system to check how it behaves.

The idea:
> "Break things on purpose and verify that the system handles failures correctly."

It is a tool/technique often used in **resilience testing**.
# Examples of injected faults
## Server failure
```
Before:

API → Service A → Database


Inject fault:

API → Service A ❌ → Database
```

Check:
- Does the API return a proper error?
- Does it retry?
- Does another instance take over?
## Network failure
Inject:
- packet loss
- high latency
- connection timeout

Example:
```
Database response:
Normal: 10 ms
Injected: 5 seconds
```

Check whether timeouts and fallbacks work.
## Resource exhaustion
Inject:
- high CPU usage
- low memory
- full disk

Example:
```
CPU:
20% → 100%
```

Check whether the system remains stable.
## Data failures
Inject:
- corrupted messages
- invalid input
- duplicate events

Check:
- validation
- error handling
- recovery mechanisms