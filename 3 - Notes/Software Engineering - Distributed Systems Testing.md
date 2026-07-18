Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Failure testing in distributed systems verifies that a system behaves correctly when components fail.

Because distributed systems assume failures can happen, tests intentionally introduce failures and check recovery behavior.

When one service sends a request to another one, then expected is that:
- requests are retried
- errors are handled
- data remains consistent
- system recovers
# Common failures tested
- service crash
- network timeout
- network partition
- message loss/delay
- database unavailable
- node failure
- high latency
# Techniques
- Fault injection → deliberately introduce failures
- Chaos testing → randomly disrupt systems to test resilience
- Failover testing → verify switching to backup systems
# What to test
- Retry testing - verify that a system correctly handles temporary failures by retrying failed operations.
- Timeout testing - test timeouts
- Eventual consistency testing - verifies that a distributed system eventually reaches the correct state after temporary inconsistencies.
- Idempotency testing - verifies that repeating the same operation multiple times produces the same final result as performing it once (important for retries and distributed systems).
- Concurrency testing - verifies that a system behaves correctly when multiple operations happen simultaneously (e.g., preventing race conditions, deadlocks, or inconsistent data).
- Chaos engineering - intentionally introduces failures into a system (e.g., killing services, adding latency) to verify that it remains reliable and recovers correctly.