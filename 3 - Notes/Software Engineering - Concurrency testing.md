Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Race conditions
([[Software Engineering - Concurrency - Race conditions|link]]) 
Testing tries to detect cases where concurrent execution causes incorrect results by running operations in different interleavings and verifying that shared data remains correct.
# Deadlocks 
([[Software Engineering - Concurrency - Deadlocks|link]])
Testing verifies that concurrent operations do not get stuck waiting for each other by running code under different locking scenarios and using timeouts or deadlock detection tools. 

Common prevention methods:
- always acquire locks in the same order
- use lock timeouts
- avoid unnecessary locks
- reduce shared mutable state
# Synchronization bugs 
([[Software Engineering - Concurrency - Synchronization bugs|link]]) 
Testing checks whether synchronization mechanisms (locks, semaphores, atomic operations, etc.) correctly protect shared resources and coordinate threads. 

Testing usually involves:
- running many threads concurrently
- changing execution order
- using deterministic schedulers
- stress testing
- verifying invariants after concurrent operations
# Deterministic schedulers 
([[Software Engineering - Concurrency - Deterministic schedulers|link]]) 
Testing uses controlled thread scheduling to reproduce specific execution orders, making intermittent concurrency bugs easier to find and debug.
# Thread testing
[[Software Engineering - Concurrency testing - Thread testing]]
# Stress testing
[[Software Engineering - Concurrency testing - Stress testing]]