Tags: [[__My_projects]]
#MyProjects 

# Introduction
Those ideas are very advanced, very few people work on things like this. They are from ChatGPT.
## Concurrent job processing system- producer-queue-consumer architecture
Idea: Build a service that accepts jobs through an HTTP API and processes them asynchronously using multiple Java workers. Job requests go to a queue and workers picks them up when they have capacity.

Example: users submit image-processing, report-generation, or data-transformation jobs.

You don't need to implement the actual processing. Jobs can simply simulate work by performing calculations or waiting.

Features to implement:

| Feature                 | Concepts practiced                |
| ----------------------- | --------------------------------- |
| Multiple worker threads | Java concurrency, ExecutorService |
| Shared job queue        | BlockingQueue, producer-consumer  |
| Bounded queue           | Backpressure                      |
| Job priorities          | Scheduling, starvation            |
| Job cancellation        | Thread interruption, cancellation |
| Job retries             | Exponential backoff, jitter       |
| Duplicate submissions   | Idempotency                       |
| Worker failures         | Fault tolerance                   |
| Graceful shutdown       | Lifecycle management              |
| Multiple API requests   | Thread safety, race conditions    |

Interesting challenges:
- What happens when jobs arrive faster than workers can process them?    
- How do you prevent two workers from processing the same job?    
- What happens if a worker crashes halfway through processing?    
- How do you avoid retrying a job indefinitely?    
- How do you prevent one type of job from starving other jobs?    
- What happens when the service receives 10,000 requests simultaneously?    

Advanced extension: Run multiple instances of your application and distribute jobs between them using Redis or RabbitMQ.

This introduces distributed job coordination, competing consumers, message acknowledgment, and delivery guarantees.
### Questions
- why to use multiple threads? Each worker should be a separate thread?
## Distributed job scheduler
materials:
- [Design a Distributed Job Scheduler for Millions of Tasks in Daily Operations | by Mayil Bayramov | Medium](https://images.openai.com/static-rsc-4/Cv2WWvVBOCmW0W62_dsu67QqxstXnNmAe_CR08korOZZUumxIl20Stm1MbVAdbpOLCyKItU1K6tUokihzwQe54OD4ExqpAp5fl4DvZW_f0XjF62w3LRNtIdnktYHwrwMPwHhMUajRPQkRfcGOWJiOzh1yB85W2F8eo-S57F9N0o?purpose=inline)
- [medium.com](https://medium.com/%40mayilb77/design-a-distributed-job-scheduler-for-millions-of-tasks-in-daily-operations-4132dc6d645f?utm_source=chatgpt.com)

Imagine a system that schedules thousands of jobs across multiple machines.

For example:
- Generate reports every hour.    
- Process uploaded files.    
- Run ML model evaluations.    
- Execute scheduled database maintenance.    
- Trigger periodic data synchronization.    

You have three scheduler instances, all capable of scheduling and dispatching jobs.

The problem: How do you prevent all three schedulers from independently dispatching the same job?

You can use consensus to elect a leader.

What consensus does:
1. Three scheduler nodes participate in a Raft cluster.    
2. They elect one leader.    
3. The leader manages the schedule and assigns jobs.    
4. Followers replicate scheduling state.    
5. If the leader crashes, the remaining nodes elect another leader.    
6. The new leader resumes scheduling from replicated state.    

Concepts you can practice:
- Leader election.    
- Consensus and replicated logs.    
- Leader failure detection.    
- Failover.    
- Split-brain prevention.    
- Distributed leases.    
- Job deduplication.    
- At-least-once execution.    
- Idempotency.    
- Recovery after failures.    

Interesting challenge: What if the old leader becomes disconnected from the cluster but is still running and dispatching jobs?

Consensus alone doesn't prevent an isolated old leader from performing external actions. You can introduce fencing tokens and make workers reject operations from outdated leaders.

This is a very realistic engineering problem.
## Distributed configuration management system
materials:
- [Safeguarding Dynamic Configuration Changes at Scale | by Cosmo W. Q | The Airbnb Tech Blog | Feb, 2026 | Medium](https://images.openai.com/static-rsc-4/YLhuhLBoMLjGy0mI_BPFPTu09CqbD1F8LW_1tSuqdEfOZ7CYoagEbdx0Mk-qFYY2mJZT-TGK1Tp1zKFZR7Ea_90ulCAtVZyd1DeHm7jkyXYPzcg64WMnTHu9XDsI71JibwF4swLL9vAGYDRhyQ6c5WwJZ7fbLU-AJQsCe_z9qZs?purpose=inline)
- [medium.com](https://medium.com/airbnb-engineering/safeguarding-dynamic-configuration-changes-at-scale-5aca5222ed68?utm_source=chatgpt.com)

Build a simplified configuration management platform.

Imagine you have 100 application instances and want to change their configuration:
```
max_connections: 100
request_timeout: 5000
feature_enabled: true
```

You need to ensure that all instances receive a consistent configuration.

What consensus does:
- You maintain configuration state in a replicated cluster.
- When an administrator changes a configuration:
	1. The request reaches the leader.	    
	2. The leader proposes a new configuration version.	    
	3. The change is replicated to followers.	    
	4. Once committed, the configuration becomes authoritative.	    
	5. Application instances receive the new version.    

Concepts you can practice:
- Consensus.    
- Replicated state machines.    
- Versioning.    
- Atomic configuration updates.    
- Configuration watches.    
- Failure recovery.    
- Consistency guarantees.    
- Schema validation.    
- Rollbacks.    

Interesting challenge: Implement configuration transactions where several related settings must change together.

For example, you don't want to update the database connection pool size without simultaneously updating the maximum number of worker threads.

This resembles functionality found in distributed coordination systems such as etcd and Consul.
## Distributed event processing system
Idea: Build a simplified event-processing platform.

For example, an application produces events:
```
UserRegistered
OrderCreated
PaymentCompleted
OrderCancelled
```

Different consumers process these events independently.

Features to implement:

|Feature|Concepts practiced|
|---|---|
|Event producers|Messaging|
|Consumer groups|Parallel processing|
|Partitioning|Scalability|
|Ordering|Event sequencing|
|Consumer offsets|Delivery semantics|
|Retry queues|Fault tolerance|
|Dead-letter queue|Failed message handling|
|Event replay|Event sourcing|
|Backpressure|Flow control|
|Schema evolution|Compatibility|

You could eventually replace your own message queue with Kafka and compare the differences.

An especially interesting exercise is implementing at-least-once delivery and dealing with duplicate events using idempotent consumers.
## Distributed rate limiter and lock manager
Idea: Create a service that controls how frequently clients can access resources and provides distributed locking.

For example:
- Maximum 100 requests per minute per user.    
- Only one worker can process a particular resource at a time.    
- Multiple application instances share the same limits.    

Features to implement:

|Feature|Concepts practiced|
|---|---|
|Token bucket|Rate limiting|
|Leaky bucket|Traffic shaping|
|Sliding window|Time-based algorithms|
|Distributed locks|Coordination|
|Lock expiration|Leases|
|Fencing tokens|Stale lock protection|
|Atomic operations|Redis Lua, transactions|
|Clock differences|Distributed time problems|
|Lock renewal|Failure handling|

**What consensus does**

The lock service maintains authoritative lock ownership across multiple nodes.

You can use Raft to replicate lock acquisition and release operations.

Concepts you can practice
- Consensus.    
- Distributed locks.    
- Leases and expiration.    
- Lock ownership.    
- Fencing tokens.    
- Failure detection.    
- Race conditions.    
- Deadlock prevention.    
- Atomic state transitions.    

Interesting challenge: A client acquires a lock, becomes disconnected, and later continues working after its lease expires.

Another client has already acquired the lock.

How do you prevent the first client from overwriting the second client's work?

This is where fencing tokens become particularly useful.

You can also implement lock renewal and automatic expiration.

One particularly valuable challenge: demonstrate why simply implementing a distributed lock with an expiration timestamp isn't sufficient. Introduce fencing tokens to prevent an old lock holder from performing stale writes.
## Other concepts worth practicing
These don't necessarily need their own projects. You can introduce them into the projects above.

| Concept                   | What you should understand and implement                   |
| ------------------------- | ---------------------------------------------------------- |
| Circuit breaker           | Stop calling failing dependencies temporarily              |
| Bulkhead isolation        | Prevent one overloaded component from affecting everything |
| Retry with jitter         | Avoid synchronized retries                                 |
| Transactional outbox      | Reliably publish events after database transactions        |
| Saga pattern              | Coordinate multi-step distributed transactions             |
| CQRS                      | Separate write and read models                             |
| Event sourcing            | Store changes as events                                    |
| MVCC                      | Concurrent database reads and writes                       |
| Cache invalidation        | Maintain consistency between cache and database            |
| Cache stampede prevention | Avoid simultaneous expensive cache refreshes               |
| Sharding                  | Distribute data across partitions                          |
| Consistent hashing        | Distribute keys across changing node sets                  |
| Backpressure              | Control producers based on consumer capacity               |
| Bulk processing           | Batch operations for throughput                            |
| Observability             | Metrics, logs, distributed tracing                         |
## Technology stack
I'd deliberately keep the technology stack relatively small:

|Technology|Purpose|
|---|---|
|Java|Main programming language|
|Spring Boot|REST APIs and application structure|
|PostgreSQL|Persistent storage and transactions|
|Redis|Distributed coordination and caching|
|RabbitMQ or Kafka|Messaging|
|Docker Compose|Running multiple services/nodes|
|JUnit 5|Automated tests|
|Testcontainers|Integration testing|
|Micrometer + Prometheus|Metrics|
|OpenTelemetry|Distributed tracing|

## Distributed key-value store with consensus
Idea: Build a simplified distributed database consisting of three Java nodes.

Each node stores key-value pairs:
```
user:123 -> Marcin
user:456 -> John
order:123 -> completed
```

The nodes communicate with each other and maintain consistent data.

Features to implement:

|Feature|Concepts practiced|
|---|---|
|Leader election|Consensus, Raft|
|Replicating writes|Distributed coordination|
|Quorum|Distributed consistency|
|Leader failure|Fault tolerance|
|Network partitions|Split-brain prevention|
|Replicated logs|State machine replication|
|Log compaction|Snapshots|
|Node recovery|State synchronization|
|Concurrent writes|Ordering and consistency|

I would specifically recommend implementing a simplified version of the Raft consensus algorithm.

You can start with:
1. Three nodes.    
2. Leader election.    
3. Heartbeats.    
4. Replicating log entries.    
5. Committing entries after majority acknowledgment.    
6. Recovering a failed node.    

You don't need a complete database engine. A simple in-memory key-value store is sufficient.

This is probably the most educational project on the list if you're interested in distributed computing.
## Distributed deployment orchestrator
materials:
- [Kubernetes Architecture - by Neo Kim and Ayaan](https://images.openai.com/static-rsc-4/KwyRddf0Krd_gfEQndmMkrlZ7CNP1rgwMmrAjiwNPU8mG8SCAiPbXd7HNcc_bIdat1mqJJcqfQxAStqUcIO9PRL5aRUgQDEGvxHchN4wMxY_ESSfjGspioO1orZDgfQJpSxIBu-BQLoKNoAU8EV2_zgSJ9p5BBjAqlemushBRRQ?purpose=inline)
- [newsletter.systemdesign.one](https://newsletter.systemdesign.one/p/kubernetes-architecture?utm_source=chatgpt.com)

Build a simplified version of a deployment orchestration system.

Imagine you have 20 application instances running across five machines. You want to deploy a new version.

You submit:
```
application: payment-service
replicas: 5
version: v2
```

Your system must coordinate the deployment.

**What consensus does:**
Maintain a shared, authoritative desired state using a consensus-backed control plane.

Multiple controller instances can monitor the cluster, but you need to coordinate which one performs certain control operations.

For example:
- One controller becomes the leader.    
- It manages deployment decisions.    
- Other controllers replicate the state.    
- If the leader crashes, another takes over.    

Concepts you can practice:
- Leader election.    
- Desired state vs actual state.    
- Reconciliation loops.    
- Distributed coordination.    
- Failure detection.    
- Rolling deployments.    
- Health checks.    
- Automatic recovery.    
- Versioned state.    
- Idempotent operations.    

Interesting challenge: What happens if the controller crashes halfway through a deployment?

The new controller should inspect the actual state, compare it with the desired state, and continue rather than starting everything from scratch.

This is particularly interesting because it introduces the reconciliation pattern used by Kubernetes controllers.
## Distributed stream partition coordinator
- [Consumer Group Protocol: Scalability and Fault Tolerance](https://images.openai.com/static-rsc-4/wzpmp0VTbroCkm6e_QYuVj-HBWJpsO6bTLPDSGtdC3eex9LDiwNYCjWooTZUQ_SdPugbe02w8h__D1qVtDAjnXnge7zKZftbfSRxV19wZ4MolFtA8Rk7aBUh86-o3AjfuAil6zh_98csfZz3_p2naQ7nkp4ucwaDGKGw0hKEQCs?purpose=inline)
- [developer.confluent.io](https://developer.confluent.io/courses/architecture/consumer-group-protocol/?utm_source=chatgpt.com)

Build a simplified distributed message-processing system.

Imagine you have:
- 3 message brokers.    
- 10 consumers.    
- 20 partitions.    

You need to assign partitions to consumers and coordinate changes when consumers join or leave.

For example:

|Consumer|Assigned partitions|
|---|---|
|Consumer 1|1, 2, 3, 4|
|Consumer 2|5, 6, 7, 8|
|Consumer 3|9, 10, 11, 12|

If Consumer 2 crashes, its partitions must be reassigned.

**What consensus does**

You can use a consensus-backed coordinator to maintain authoritative assignment metadata and coordinate changes.

Concepts you can practice
- Leader election.    
- Partition assignment.    
- Consumer groups.    
- Rebalancing.    
- Membership changes.    
- Distributed coordination.    
- Failure recovery.    
- Message ordering.    
- Offset management.    
- Backpressure.    

This is especially relevant because similar problems appear in Kafka and distributed stream-processing platforms.
## Distributed workflow orchestration
materials:
- [Workflow Engine Design Principles with Temporal | Temporal](https://images.openai.com/static-rsc-4/7veNAEcUgBkTT4h8v2gjzEe56yWnP6vg0AHZApnjxmBEqtC6nd3BEiTH25BQu9KCKcjaTi86blAezDUXzzsvE5vrJp2HJbtMvuhoDP3pKHV-MccB4Hd19Ta4XI-G6Bjj3FZ31vx7qDpcxhcdONxYITNQ4GzdbKo_JJmxcCMCU0s?purpose=inline)
- [docs.temporal.io](https://docs.temporal.io/blog/workflow-engine-principles/?utm_source=chatgpt.com)

Build a simplified workflow engine, similar in concept to Temporal.

Users define workflows consisting of multiple steps:
```
1. Receive order
2. Reserve inventory
3. Process payment
4. Arrange shipping
5. Notify customer
```

Each step can execute on a different worker.

**What consensus does**

You maintain a consistent workflow execution state across multiple orchestration nodes.

For example:
- Which workflows are running?    
- Which steps have completed?    
- Which steps need retrying?    
- Which worker owns a particular task?    
- What happens when the orchestrator crashes?    

Concepts you can practice
- Consensus and replicated state.    
- State machines.    
- Distributed scheduling.    
- Worker coordination.    
- Checkpointing.    
- Recovery.    
- Timeouts.    
- Retries.    
- Compensation transactions (Sagas).    
- Idempotency.    

Interesting challenge: Your orchestrator crashes after a payment succeeds but before recording that success. How do you recover without charging the customer twice?

This is a very good exercise in combining distributed coordination with practical application-level reliability.