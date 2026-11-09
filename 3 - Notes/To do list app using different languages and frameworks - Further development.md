Tags: [[__My_projects]]
#MyProjects 

# Backend operations to implement
1. Authentication
	- User registration
	- User login
	- User logout
	- Token/session validation
	- Password hashing and verification
2. User management
	- Get current user information
	- Update user profile
	- Delete user account
3. Task management (CRUD)
	- Create a task
	- Get all tasks belonging to the authenticated user
	- Get a specific task
	- Update task (title, description, status)
	- Delete a task
4. Additional operations
	- Filter tasks by status
	- Search tasks by title
	- Sort tasks (e.g. by creation date)
	- Pagination (retrieve tasks in batches)
5. Backend infrastructure
	- Input validation
	- Authorization (users can only access their own tasks)
	- Error handling (fault tolerance)
	- Logging
	- API documentation (OpenAPI/Swagger)
6. use async programming to allow executing multiple operations concurrently, for example:
	- loading multiple datasets using `Promise.all()` (e.g. user tasks, profile, notification count)
	- allow users to perform multiple operations at the same time (e.g. Add a task, Update  task's status, Delete a task). Each operation could make an independent API request which are async `async function updateTask() {await fetch("/api/tasks/${id}", ...}`.
7. Develop some plugins
8. Dependency management (e.g. dependency injection)
# Concurrent modifications and optimistic locking
What if:
- user A loads an app
- user B updates task X
- user A wants to update task X (but doesn't see the update made by the user B because didn't refresh the app)
- if user A completed the update, then update made by the user B is lost

Try to use OCC ([[Software Engineering - Concurrency patterns - Optimistic Concurrency Control (OCC)|link]]).

Concepts and tools:

| Problem                   | Technique/tool                 |
| ------------------------- | ------------------------------ |
| Lost updates              | Optimistic concurrency control |
| Concurrent modifications  | Database transactions          |
| Version management        | Version columns                |
| HTTP-level concurrency    | ETag and If-Match              |
| Exclusive access          | Pessimistic locking            |
| Concurrent update testing | JUnit, integration tests       |

I would also implement pessimistic locking as an alternative and compare the two approaches.

For example, use `SELECT ... FOR UPDATE` to lock a task while a transaction modifies it.

This is a particularly useful exercise because you'll understand that Java synchronization and database locking solve different problems.
# Concurrent processing of multiple tasks
When a lot of requests arrive simultaneously, we can have multiple workers to process them concurrently.

Each worker communicates with the mock payment provider.

You could implement a simple worker pool using Java's `ExecutorService` and a shared queue.

Initially, you could have just one application with multiple worker threads.

What you learn:
- Threads and thread pools.    
- Producer-consumer pattern.    
- Blocking queues.    
- Synchronization.    
- Race conditions.    
- Thread safety.    
- Atomic operations.    
- Database locking.    

One particularly interesting problem:
>Two workers accidentally attempt to process the same payment.

How do you prevent that? You could introduce:
- Atomic database updates.    
- Pessimistic locking.    
- Optimistic locking.    
- Unique constraints.    

These techniques are widely applicable to backend systems.
## Handling too many incoming requests
This is another thing I'd definitely implement.

Imagine 10,000 requests arrive within a few seconds.

You don't want to create an unlimited number of threads or overload your database.

Introduce several mechanisms.
1. Thread pool

Use a bounded thread pool to limit concurrent execution.

For example:
```
Incoming requests: 10,000

Worker threads: 20
Maximum queued requests: 100

Remaining requests:
  Rejected or deferred
```

In Spring MVC, learn how request handling uses the servlet container's thread pool. Then experiment with a separate `ThreadPoolExecutor` for background tasks.

2. Semaphores
Suppose your backend can safely handle only 10 simultaneous calls to an external service.

Use a semaphore to limit concurrent access.

3. Rate limiting
Limit requests per user or API key.

For example:
```
Maximum 100 requests per minute per user.
```

You can implement a token bucket algorithm or use Bucket4j.

4. Backpressure
Suppose background tasks are arriving faster than workers can process them.

Use bounded queues and reject, defer or throttle new work rather than allowing an unlimited backlog.

5. Load shedding
When the system is overloaded, reject lower-priority requests rather than allowing the entire application to become unresponsive.

Concepts and tools:

|Problem|Technique/tool|
|---|---|
|Too many concurrent requests|Thread pools|
|Limited external resources|Semaphores|
|Too many requests per user|Rate limiting / Bucket4j|
|Overloaded workers|Bounded queues|
|Overloaded application|Load shedding|
|Resource exhaustion|Timeouts and bulkheads|
|Temporary overload|Backpressure|

One clarification: `async` doesn't automatically solve overload. Asynchronous programming changes how you wait for operations; it doesn't eliminate resource limits. You still need bounded concurrency and capacity management.
# Concurrent bulk operations and transactions
Suppose a user selects 20 tasks and clicks "Mark as completed".

Your backend needs to update all 20 tasks.

Now consider:
- The operation succeeds for 10 tasks.    
- The application crashes.    
- The remaining 10 aren't updated.    

Should you allow partially completed operations?

Implement two versions:

Version 1: Atomic bulk operation
>All updates happen in one database transaction. Either all succeed or none do.

Version 2: Independent asynchronous operations
>Each task update is independent and can succeed or fail separately.

Compare the two approaches.

Then introduce concurrent bulk operations:
- Request A updates tasks 1–20.    
- Request B updates tasks 15–30.    

This introduces potential locking conflicts and deadlocks.

Concepts and tools:
- ACID transactions.    
- Transaction isolation levels.    
- Atomicity.    
- Database locking.    
- Deadlocks.    
- Transaction propagation in Spring.    
- `@Transactional`.    
- Batch operations.    
- Handling transaction failures.    

You could deliberately create a deadlock by having two transactions acquire locks in opposite orders. Then fix it by acquiring locks in a consistent order.

This is a very practical database engineering exercise.
# Offline modifications and synchronization
This is probably the most interesting extension of your to-do application.

Imagine a user opens the application, disconnects from the internet and continues modifying tasks.

When the connection returns, the application must synchronize local modifications with the server.

Introduce a local database in the frontend, for example IndexedDB.

Your frontend maintains:
- A local copy of tasks.    
- A list of pending modifications.    
- A version number for each task.    
- A unique ID for every operation.    

Example:
```
Local changes:

Operation 1:
  Task 123
  Change status to DONE

Operation 2:
  Task 124
  Change description to "Buy bread"
```

When the connection returns, send the pending operations to the backend.

But what if the server has already received a modification to task 123 from another device?

You need to detect and resolve the conflict.

Techniques that we can implement:

|Problem|Technique|
|---|---|
|Detect changes since last synchronization|Version numbers / change cursors|
|Duplicate operations|Idempotency keys|
|Concurrent changes|OCC|
|Deleted records|Tombstones|
|Conflict resolution|Last-write-wins or manual resolution|
|Synchronizing changes|Incremental synchronization|
|Ordering operations|Sequence numbers|
|Recovering missed updates|Reconciliation|

For a first implementation, I would use a simple approach:
1. Each task has a version number.    
2. Each modification has a unique operation ID.    
3. The server rejects modifications based on outdated versions.    
4. The frontend downloads the current server version.    
5. The user can choose which conflicting change to keep.    

Later, experiment with automatic conflict resolution.

An important distinction: You don't need CRDTs for this. Version-based synchronization and explicit conflict handling are much more appropriate starting points for a typical business application.
# Live updates using WebSockets or SSE
Imagine user A and user B are viewing the same task list.

User A updates a task.

You want user B's application to update automatically without refreshing the page.

Implement server-to-client notifications.

Two options:
- SSE (Server-Sent Events): server pushes updates to clients over an HTTP connection.    
- WebSockets: bidirectional communication between client and server.    

For your application, SSE is probably sufficient initially.

For example:
```
User A updates task
       |
       v
Backend saves task
       |
       v
Backend publishes event
       |
       +---- SSE connection to User A
       |
       +---- SSE connection to User B
       |
       +---- SSE connection to User C
```

You don't need to transmit the entire task list. Just transmit the event and relevant task information.

Concepts and tools:
- Persistent connections.    
- Asynchronous communication.    
- Event broadcasting.    
- Connection management.    
- Concurrent clients.    
- Backpressure.    
- Spring WebSocket / Spring MVC SSE support.    

One interesting problem: what happens when a user is disconnected while several events are published?

You can combine this with your offline synchronization mechanism. When the client reconnects, it requests all changes since its last known version/cursor.
# Event sourcing / audit log
What about event sourcing?

I'd implement an audit log first, rather than full event sourcing.

For example:
```
TaskCreated
TaskDescriptionChanged
TaskStatusChanged
TaskDeleted
```

Store these events in a separate table.

You can use them to:
- Show task history.    
- Audit changes.    
- Investigate unexpected modifications.    
- Rebuild a statistics projection.    

Then, if you're interested, implement a small event-sourced task entity where the current state is reconstructed from its events.

Full event sourcing is a substantially bigger architectural commitment and isn't necessary for most CRUD applications.
# Distributed systems concepts
| Concept              | Practical exercise                                                      |
| -------------------- | ----------------------------------------------------------------------- |
| Partial failures     | Disconnect the database or message broker temporarily                   |
| Eventual consistency | Asynchronously update task statistics                                   |
| Duplicate delivery   | Process the same task event multiple times                              |
| Idempotency          | Make event consumers safe against duplicates                            |
| Logical ordering     | Use task versions and event sequence numbers                            |
| Conflict resolution  | Synchronize offline modifications                                       |
| Distributed locking  | Prevent two application instances from executing the same scheduled job |
| Clock problems       | Simulate clients with different system clocks                           |
One important lesson: don't use timestamps as the primary mechanism for detecting concurrent modifications.

Client clocks can be inaccurate or differently synchronized. Use database versions, sequence numbers or other explicit ordering mechanisms instead.
# Problems
- What if the task list becomes huge?
	- we need to prevent somehow:
		- loading all the data at once because that would take too much time
		- displaying all the tasks at once because that would take too much space and there would be too much scrolling
# Other things to implement
- Code testing

|Feature|Concepts practiced|
|---|---|
|Concurrent modifications|Race conditions|
|Version numbers|Optimistic concurrency control|
|Database transactions|ACID, isolation levels|
|Row-level locking|Pessimistic concurrency|
|Conflict detection|Version conflicts|
|Conflict resolution|Last-write-wins, custom policies|
|Live updates|WebSockets|
|Offline modifications|Synchronization|
|Collaborative editing|CRDTs or operational transformation|

Note: Consensus and conflict resolution are different problems. Raft helps nodes agree on an ordered sequence of operations. CRDTs help independently modified data converge without necessarily requiring a central leader.