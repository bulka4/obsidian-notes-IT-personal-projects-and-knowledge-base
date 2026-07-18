Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
The CAP theorem is a fundamental principle in distributed systems that states:
> A distributed system can guarantee at most two of the following three properties at the same time:
> - C – Consistency
> - A – Availability
> - P – Partition Tolerance

Here's what each term means:
1. **Consistency (C)**
    - Every read receives the most recent write (data) or an error.
    - All nodes see the same data at the same time.
    - Example: If you update your bank balance, every server immediately returns the updated balance.
2. **Availability (A)**
    - Every request receives a response, even if some servers are down.
    - The response may not always contain the latest data.
    - Example: A shopping website remains accessible even if some database nodes fail.
3. **Partition Tolerance (P)**
    - The system continues to operate despite communication failures (network partitions) between nodes.
    - Saying that "system continues to operate" doesn't mean it sends responses to requests. 
	    - It might not be able to send responses but the nodes/services are still running and the system has a defined behavior during the partition.
	    - It means all the services didn't restart or crash at the same time.
    - This is essential for distributed systems because network failures are inevitable.
# Why can't we have all three?
When a network partition (failure) occurs, servers cannot communicate with each other, so we can't have the latest data on each one. 

At that point, we must choose between consistency and availability:
- **Consistency**: To achieve consistency, we must reject some requests (loose availability) until nodes synchronize and each node has the latest data.
- **Availability**: To achieve availability, we must continue serving requests, even if some responses are based on stale data (so we loose consistency).

Or in other words:
- If we continue serving requests, then we maintain availability but some responses are based on stale data, so we loose consistency.
- If we stop serving requests, then we maintain consistency (we don't use stale data) but we loose availability.

So during a partition (network failure), we can have either:
- CP (Consistency + Partition Tolerance), or
- AP (Availability + Partition Tolerance)

We cannot guarantee both consistency and availability simultaneously while also tolerating the partition (network failure).
# Choice in practice
- P (Partition Tolerance) is usually non-negotiable in distributed systems because network failures are unavoidable.
- Therefore, in practice, the real design choice is between:
    - CP → Prefer correct data over always responding.
    - AP → Prefer always responding over immediately consistent data.