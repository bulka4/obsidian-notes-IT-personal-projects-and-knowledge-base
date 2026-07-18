Tags: [[_Software_Engineering]]
#SoftwareEngineering 

This is a collection of notes related to software engineering.

# Software development practices
1. [[Software Engineering - Reproducibility]]
2. [[_Software_Engineering_testing]]

Other topics that might be included:
- Version control
- Dependency management
- Build automation
- CI/CD
# Software architecture
## Architecture concepts
1. [[Software Engineering - Architecture concepts]]
	1. [[Software Engineering - Architecture concepts - Domain]]
	2. [[Software Engineering - Architecture concepts - Business (domain) logic]]
	3. [[Software Engineering - Architecture concepts - Domain objects]]
		1. [[Software Engineering - Architecture concepts - Entity]]
		2. [[Software Engineering - Architecture concepts - Value object]]
		3. [[Software Engineering - Architecture concepts - Aggregate]]
		4. [[Software Engineering - Architecture concepts - Domain Service]]
	4. [[Software Engineering - Architecture concepts - Domain event]]
	5. [[Software Engineering - Architecture concepts - Use case]]
	6. [[Software Engineering - Architecture concepts - Application Service]]
	7. [[Software Engineering - Architecture concepts - DTO (Data Transfer Object)]]
	8. [[Software Engineering - Architecture concepts - Command]]
	9. [[Software Engineering - Architecture concepts - Query]]
	10. [[Software Engineering - Architecture concepts - Module]]
	11. [[Software Engineering - Architecture concepts - Component]]
	12. [[Software Engineering - Architecture concepts - Layer]]
	13. [[Software Engineering - Architecture concepts - Service]]
	14. [[Software Engineering - Architecture concepts - Repository]]
	15. [[Software Engineering - Architecture concepts - Interface adapters]]
## Architecture styles
1. [[Software Engineering -Software architecture]]
	1. [[Software Engineering - Layered architecture]]
	2. [[Software Engineering - Hexagonal architecture]]
	3. [[Software Engineering - Clean architecture]]
	4. [[Software Engineering - Microservices vs monoliths]]
	5. [[Backend Engineering - Event-driven architecture]]
		1. [[Backend Engineering - Event-driven architecture - Benefits and drawbacks]]
		2. [[Backend Engineering - Event-driven architecture - Events and messages]]
		3. [[Backend Engineering - Event-driven architecture - Producer and consumer]]
		4. [[Backend Engineering - Event-driven architecture - Message broker]]
		5. [[Backend Engineering - Event-driven architecture - Delivery Guarantees]]
		6. [[Backend Engineering - Event-driven architecture - Queues (point-to-point)]]
		7. [[Backend Engineering - Event-driven architecture - Topics (pub-sub)]]
			1. [[Backend Engineering - Event-driven architecture - Consumer group]]
		8. [[Backend Engineering - Event-driven architecture - Idempotency]]
		9. [[Backend Engineering - Event-driven architecture - Ordering]]
		10. [[Backend Engineering - Event-driven architecture - Partitioning]]
			1. [[Backend Engineering - Event-driven architecture - Partition replication]]
		11. [[Backend Engineering - Event-driven architecture - Dead Letter Queue (DLQ)]]
## System architecture patterns
1. [[Backend Engineering - System architecture patterns]]
	1. [[Backend Engineering - CQRS system architecture]]
	2. [[Backend Engineering - Software architecture - Backend-for-Frontend]]
	3. [[Backend Engineering - Data storage - Event sourcing]]
	4. [[Backend Engineering - Data Consistency Patterns - Saga pattern]]
## Cross-cutting architecture
1. [[Software Engineering - Plugins]]
2. [[Software Engineering - Dependency injection]]

Other topics:
- modularity
- Dependency management
- Configuration management
- State management
- Transaction boundaries
- Consistency boundaries
- Idempotency
# Programming
## Process / program execution
1. [[Software Engineering - Runtime]]
2. [[Software Engineering - Threads]]
3. [[Software Engineering - Memory leak]]
4. [[Software Engineering - Execution path]]

Other topics that might be included:
- Compilation
- Interpretation
- Virtual Machines
- Memory Management
- Garbage Collection
## Programming design
### Object-oriented design
1. [[Software Engineering - Object-oriented design]]
2. [[Software Engineering - Object-oriented design - SOLID]]
3. [[Software Engineering - Object-oriented design - composition vs inheritance]]
4. [[Software Engineering - Object-oriented design - Interfaces]]
5. [[Software Engineering - Object-oriented design - Protocols]]
6. [[Software Engineering - Object-oriented design - Design patterns]]
### Functional programming
notes to add
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
	1. [[Backend Engineering - Bulk endpoints
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
# Concurrency and parallelism
1. [[Software Engineering - Concurrency]]
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
## I/O and asynchronous programming
1. [[Software Engineering - Concurrency - Async programming models]]
	1. [[Software Engineering - Async programming models - Event loops]]
2. [[Software Engineering - Async programming models - Blocking vs non-blocking I-O]]
3. [[Linux & Bash - Epoll]]
4. [[Software Engineering - Async programming models - Reactor pattern]]
# System reliability
1. [[Software Engineering - Transactions]]
	1. [[Software Engineering - ACID transactions]]
	2. [[Software Engineering - Rollback]]
## Handling failures
1. [[Software Engineering - Handling failures]]
	1. [[Software Engineering - Handling failures - Fault tolerance]]
	2. [[Software Engineering - Handling failures - Timeouts]]
	3. [[Software Engineering - Handling failures - Retries with backoff]]
	4. [[Software Engineering - Handling failures - Circuit breakers]]
	5. [[Software Engineering - Handling failures - Bulkheads]]
	6. [[Software Engineering - Handling failures - Idempotency]]
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
- **Software architecture**
- **Distributed systems**
- **Object-oriented design**
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
- System architecture patterns - [[Backend Engineering - System architecture patterns|link]] 
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