Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A distributed lock is a type of lock ([[Software Engineering - Concurrency - Locks|link]]) used when multiple processes or servers need to coordinate access to a shared resource.

A normal mutex/read-write lock usually works inside one machine (between threads). A distributed lock works across multiple machines.
# Example
You have 3 backend servers:
```
Server A
Server B
Server C
```

All of them run the same scheduled job:
```
Generate daily report
```

Without a distributed lock:
```
09:00

Server A: starts generating report
Server B: starts generating report
Server C: starts generating report
```

You get duplicate work.

With a distributed lock:
```
Server A: acquires lock
Server B: tries to acquire lock → waits/fails
Server C: tries to acquire lock → waits/fails

Server A: generates report
Server A: releases lock
```
# Where a lock is stored
The lock is stored in some shared system that all servers can see, for example:
- a database row
- Redis
- ZooKeeper
- etcd
# Use cases
- Only one worker processes a specific job.
- Prevent multiple services from updating the same external resource.
- Leader election (choose one server to perform a task).
- Prevent duplicate payment/order processing.