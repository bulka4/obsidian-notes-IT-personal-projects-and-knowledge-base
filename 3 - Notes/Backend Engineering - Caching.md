Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Caching is one of the most important performance techniques in backend systems. The core idea is:
> Store frequently used data in a faster storage layer (e.g. memory) so we don’t recompute or refetch it every time.

We do this because reading data e.g. from memory is faster than from a disk and than recomputing this data.
# Examples
Common examples of what data can be cached:
- database query results
- API responses
- computed results (e.g., recommendations)
- session data (login state)
- static content (images, JS files)
# Types of caching
- In-memory cache - Store cache data in memory
- Distributed cache - Store cache data in a shared system used by many services
- CDN cache - cache distributed across servers around the world that stores static or infrequently changing content closer to users
# Problems
Problems with caching:
- Stale data - cache may not reflect latest DB state, it doesn't contain the latest updated data
- Memory limits - cache cannot store everything