Tags: [[_Software_Engineering]]
#SoftwareEngineering 

This is a collection of notes related to software engineering.

# Business modelling
[[_IT_Business_Modelling]]
# Software development practices
1. [[Software Engineering - Reproducibility]]
2. [[_Software_Engineering_testing]]

Other topics that might be included:
- Version control
- Dependency management
- Build automation
- CI/CD
# Software architecture
## Software architecture dimensions
1. [[Software Engineering - Software architecture dimensions]]
### Domain-Driven Design (DDD) / Business Modeling
1. [[Software Engineering - Architecture concepts - Domain-Driven Design (DDD)]]
	1. [[Software Engineering - Architecture concepts - Domain]]
	2. [[Software Engineering - Architecture concepts - Business (domain) logic]]
	3. [[Software Engineering - Architecture concepts - Domain objects]]
		1. [[Software Engineering - Architecture concepts - Entity]]
		2. [[Software Engineering - Architecture concepts - Value object]]
		3. [[Software Engineering - Architecture concepts - Aggregate]]
		4. [[Software Engineering - Architecture concepts - Domain Service]]
	4. [[Software Engineering - Architecture concepts - Domain event]]
### Application Design (Use Cases and Workflows)
1. [[Software Engineering - Architecture concepts - Application Design]]
	1. [[Software Engineering - Architecture concepts - Use case]]
	2. [[Software Engineering - Architecture concepts - Application Service]]
	3. [[Software Engineering - Architecture concepts - DTO (Data Transfer Object)]]
	4. [[Software Engineering - Architecture concepts - Command]]
	5. [[Software Engineering - Architecture concepts - Query]]
### Software Structure and Organization
1. [[Software Engineering - Architecture concepts - Software Structure and Organization]]
	1. [[Software Engineering - Architecture concepts - Module]]
	2. [[Software Engineering - Architecture concepts - Component]]
	3. [[Software Engineering - Architecture concepts - Layer]]
	4. [[Software Engineering - Architecture concepts - Service]]
### Communication and Boundaries
1. [[Software Engineering - Architecture concepts - Communication and Boundaries]]
	1. [[Software Engineering - Architecture concepts - Interface]]
	2. [[Software Engineering - Architecture concepts - Repository]]
	3. [[Software Engineering - Architecture concepts - Interface adapters]]
## Architecture styles
1. [[Software Engineering -Software architecture]]
	1. [[Software Engineering - Layered architecture]]
	2. [[Software Engineering - Hexagonal architecture]]
	3. [[Software Engineering - Clean architecture]]
	4. [[Software Engineering - Microservices vs monoliths]]
	5. [[Backend Engineering - Event-driven architecture (EDA)]]
		1. [[Backend Engineering - Event-driven architecture - Benefits and drawbacks]]
		2. [[Backend Engineering - Event-driven architecture - Events and messages]]
		3. [[Backend Engineering - Event-driven architecture - Producer and consumer]]
		4. [[Backend Engineering - Event-driven architecture - Message broker]]
		5. [[Backend Engineering - Event-driven architecture - Queues (point-to-point)]]
		6. [[Backend Engineering - Event-driven architecture - Topics (pub-sub)]]
			1. [[Backend Engineering - Event-driven architecture - Consumer group]]
		7. [[Backend Engineering - Event-driven architecture - Partitioning]]
			1. [[Backend Engineering - Event-driven architecture - Partition replication]]
		8. [[Backend Engineering - Fault tolerance - Event-driven architecture]]
			1. [[Backend Engineering - Event-driven architecture - Dead Letter Queue (DLQ)]]
			2. [[Backend Engineering - Event-driven architecture - Idempotency]]
			3. [[Backend Engineering - Event-driven architecture - Ordering]]
			4. [[Backend Engineering - Event-driven architecture - Delivery Guarantees]]

Other styles:
- Service-oriented architecture (SOA)
- Pipe-and-filter architecture
- Client-server architecture
## System architecture patterns
1. [[Software Engineering - System architecture patterns]]
	1. [[Software Engineering - Architecture patterns - CQRS]]
	2. [[Software Engineering - Architecture patterns - Backend-for-Frontend]]
	3. [[Software Engineering - Architecture patterns - Event sourcing]]
		1. [[Software Engineering - Event sourcing - Event schema evolution]]
		2. [[Software Engineering - Event sourcing - Event replay]]
	4. [[Software Engineering - Architecture patterns - Saga]]
		- [[Software Engineering - Saga pattern - Choreography (event-driven) type]]
		- [[Software Engineering - Saga pattern - Orchestration type]]
## Software composition & modularity
1. [[Software Engineering - Plugins]]
2. [[Software Engineering - Dependency management]]
	1. [[Software Engineering - Dependency injection]]
3. [[Software Engineering - Modularity]]
4. [[Software Engineering - Configuration management]]
# Programming
## Process / program execution
1. [[Software Engineering - Runtime]]
2. [[Software Engineering - Execution unit]]
3. [[Software Engineering - Threads]]
4. [[Software Engineering - Memory leak]]
5. [[Software Engineering - Execution path]]

Other topics that might be included:
- Compilation
- Interpretation
- Virtual Machines
- Memory Management
- Garbage Collection
## Programming design
### Object-oriented design
1. [[Software Engineering - Object-oriented design]]
	1. [[Software Engineering - Object-oriented design - SOLID]]
	2. [[Software Engineering - Object-oriented design - Composition vs inheritance]]
	3. [[Software Engineering - Object-oriented design - Interfaces]]
	4. [[Software Engineering - Object-oriented design - Protocols]]
	5. [[Software Engineering - Object-oriented design - Design patterns]]
		1. [[Software Engineering - Design patterns - Factory]]
		2. [[Software Engineering - Design patterns - Singleton]]
		3. [[Software Engineering - Design patterns - Adapter]]
		4. [[Software Engineering - Design patterns - Decorator]]
		5. [[Software Engineering - Design patterns - Facade]]
		6. [[Software Engineering - Design patterns - Strategy]]
		7. [[Software Engineering - Design patterns - Observer]]
		8. [[Software Engineering - Design patterns - Command]]
### Functional programming
1. [[Software Engineering - Functional programming - Immutability]]
2. [[Software Engineering - Functional programming - Pure Functions]]
3. [[Software Engineering - Functional programming - Side Effects]]
4. [[Software Engineering - Functional programming - Effect Separation]]
5. [[Software Engineering - Functional programming - Higher-Order Functions]]
6. [[Software Engineering - Functional programming - Function Composition]]
7. [[Software Engineering - Functional programming - Option (Maybe) Types]]
8. [[Software Engineering - Functional programming - Result (Either) Types]]
9. [[Software Engineering - Functional programming - Pattern Matching]]
10. [[Software Engineering - Functional programming - Declarative & Imperative Programming]]
11. [[Software Engineering - Functional programming - Monads]]
12. [[Software Engineering - Functional programming - Lazy Evaluation]]
13. [[Software Engineering - Functional programming - Functional Concurrency]]
14. [[Software Engineering - Functional programming - Callbacks]]
# Concurrency and parallelism
1. [[Software Engineering - Concurrency]]
	1. [[Software Engineering - Concurrency - Threads & processes]]
	2. [[Software Engineering - Concurrency - Critical section]]
	3. [[Software Engineering - Concurrency - Shared resources]]
	4. [[Software Engineering - Concurrency - Locks]]
		1. [[Software Engineering - Concurrency - Mutex]]
		2. [[Software Engineering - Concurrency - Read-write lock]]
		3. [[Software Engineering - Concurrency - Distributed lock]]
	5. [[Software Engineering - Concurrency - Condition variables]]
	6. [[Software Engineering - Concurrency - Semaphores]]
	7. [[Software Engineering - Concurrency - Monitors]]
	8. [[Software Engineering - Concurrency - Actor model]]
	9. [[Software Engineering - Concurrency - Synchronization bugs]]
		1. [[Software Engineering - Concurrency - Race conditions]]
		2. [[Software Engineering - Concurrency - Deadlocks]]
	10. [[Software Engineering - Concurrency - Deterministic schedulers]]
## Concurrency patterns
1. [[Software Engineering - Concurrency patterns - Reactor]]
2. Proactor pattern
3. Thread pool pattern
## Asynchronous programming
1. [[Software Engineering - Async programming models]]
	1. [[Software Engineering - Async programming models - Coroutines & tasks]]
	2. [[Software Engineering - Async programming models - Event loops]]
	3. [[Software Engineering - Async programming model vs multiple threads]]
## I/O operations
1. [[Software Engineering - I-O operations]]
	1. [[Software Engineering - I-O resources]]
	2. [[Software Engineering - I-O events]]
	3. [[Software Engineering - Blocking vs non-blocking I-O]]
	4. [[Linux & Bash - Epoll]]
# System reliability
1. [[Software Engineering - Transactions]]
	1. [[Software Engineering - Transaction boundaries]]
	2. [[Software Engineering - ACID transactions]]
	3. [[Software Engineering - Rollback]]
## Fault tolerance
1. [[Software Engineering - Fault tolerance]]
	1. [[Software Engineering - Fault tolerance - Timeouts]]
	2. [[Software Engineering - Fault tolerance - Retries with backoff]]
	3. [[Software Engineering - Fault tolerance - Circuit breakers]]
	4. [[Software Engineering - Fault tolerance - Bulkheads]]
	5. [[Software Engineering - Fault tolerance - Idempotency]]
	6. [[Software Engineering - Fault tolerance - Health checks]]
	7. [[Software Engineering - Fault tolerance - Heartbeats]]
	8. [[Software Engineering - Fault tolerance - Redundancy]]
	9. [[Software Engineering - Fault tolerance - Replication]]
	10. [[Software Engineering - Fault tolerance - Failover]]
	11. [[Backend Engineering - Fault tolerance - Distributed systems]]
		1. [[Backend Engineering - Distributed systems - Partial failures]]
		2. [[Backend Engineering - Distributed systems - Consensus]]
	12. [[Backend Engineering - Fault tolerance - Event-driven architecture]]
		1. [[Backend Engineering - Event-driven architecture - Dead Letter Queue (DLQ)]]
		2. [[Backend Engineering - Event-driven architecture - Idempotency]]
		3. [[Backend Engineering - Event-driven architecture - Ordering]]
		4. [[Backend Engineering - Event-driven architecture - Delivery Guarantees]]
# Data formats and communication
## Serialization
1. [[Software Engineering - Serialization]]
	1. [[Software Engineering - Protocol Buffers]]
	2. [[Software Engineering - Avro]]
## Schema definition / validation formats
1. [[Software Engineering - Schema definition (validation) formats]]
	1. [[Software Engineering - JSON schema]]
## API design
1. [[Backend Engineering - API design principles]]
	1. [[Backend Engineering - Bulk endpoints]]
2. [[Backend Engineering - API architectures]]
	1. [[Backend Engineering - API architectures - REST]]
	2. [[Backend Engineering - API architectures - GraphQL]]
	3. [[Backend Engineering - API architectures - API gateway]]
	4. [[Backend Engineering - API architectures - RPC]]
	5. [[Backend Engineering - Streaming API Architecture]]
		1. [[Backend Engineering - Streaming API Architecture - Implementations comparison]]
		2. [[Networking - Protocols - WebSockets]]
		3. [[Backend Engineering - Streaming API Architecture - Server-Sent Events (SSE)]]
		4. [[Backend Engineering - Streaming API Architecture - Chunked HTTP]]
		5. [[Backend Engineering - Streaming API Architecture - gRPC streaming]]
# Algorithms and data structures
Data structures:
1. [[Software Engineering - Hash tables]]
2. [[Software Engineering - Trees]]
3. [[Software Engineering - Graphs]]
4. [[Software Engineering - Queues]]
5. [[Software Engineering - Heaps]]

Algorithms:
1. [[Software Engineering - Complexity analysis]]
2. [[Software Engineering - Searching]]
3. [[Software Engineering - Sorting]]
4. [[Software Engineering - Two pointers]]
5. [[Software Engineering - Sliding window]]
6. [[Software Engineering - Divide and conquer]]
7. [[Software Engineering - Greedy algorithms]]
8. [[Software Engineering - Dynamic programming]]
9. [[Software Engineering - Backtracking]]
# Operating systems and hardware
## Hardware
1. [[_Computer_hardware]]
2. [[_Hardware_abstraction]]
## Operating systems
1. [[_Linux & bash]]
2. [[__Operating_systems]]
### Containers
1. [[_Containers]]
# Tools
- Version control:
	- [[_Git]]
- Containers:
	- [[_Docker]]
- Event-driven systems:
	- [[_Kafka]]
- Programming languages
	1. [[_Python]]
# Projects to do
- [[Software Engineering - Projects to do]]
	- [[Software Engineering - Projects to do - Data and ML platform]]
		- [[Software Engineering - Projects to do - Data and ML platform - Python SDK]]
	- [[Software Engineering - Projects to do - RAG system]]
	- [[Software Engineering - Projects to do - Data governance app]]
# Topics to learn
## Topics to explore more
- (done) **Software architecture**
- (done) **Distributed systems**
- (done) **Object-oriented design**
- **Concurrency and asynchronous programming**
- **Networking and communication protocols**
- **Data storage and databases**
- **System reliability and fault tolerance**
- **API design**
- **Software engineering practices**
- **Event-driven architecture**
- **Security**
- **Operating systems and Linux**
- **Containers and infrastructure**
- **Algorithms and data structures**
- **Serialization and data formats**
- **Monitoring and observability**
- **Hardware fundamentals**
## Others
- search and recommendation systems (search indexing, ElasticSearch, OpenSearch)
- real-time systems
- System architecture patterns - [[Software Engineering - System architecture patterns|link]] 
## CI/CD
## Observability
- distributed tracing
- dashboards
- alerts
## Theoretical fields
- Algorithms and data structures
- Theory of computation
- programming language theory
- software engineering theory
- formal methods
- concurrent and distributed computing theory
- database theory
- computer systems theory
- information theory
- systems theory
### Deep theoretical, mathematical topics
- program semantics, especially denotational semantics - describing the meaning of programs mathematically
- Lambda calculus
- Type theory
- Formal verification