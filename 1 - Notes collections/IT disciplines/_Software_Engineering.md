Tags: [[_Software_Engineering]]
#SoftwareEngineering 

This is a collection of notes related to software engineering.

# Processes
1. [[Software Engineering - Threads]]
2. [[Software Engineering - Memory leak]]
# Software practices
1. [[Software Engineering - Plugins]]
2. [[Software Engineering - Transactions]]
	1. [[Software Engineering - ACID transactions]]
# Data formats
1. [[Software Engineering - Protocol Buffers]]
# Testing
1. [[Software Engineering - Testing]]
2. [[Software Engineering - Test pyramid]]
3. [[Software Engineering - Test doubles]]
4. [[Software Engineering - Deterministic tests]]
5. [[Software Engineering - Test isolation]]
6. [[Software Engineering - Test coverage and its limitations]]
7. [[Software Engineering - Arrange-Act-Assert pattern]]
8. [[Software Engineering - FAST testing principles]]
## Unit testing
1. [[Software Engineering - Unit test frameworks]]
2. [[Software Engineering - Assertions]]
3. [[Software Engineering - Parameterized tests]]
4. [[Software Engineering - Fixtures, setup, teardown]]
5. [[Software Engineering - Testing exceptions and failures]]
6. [[Software Engineering - Table-driven tests]]
## Integration testing
1. [[Software Engineering - Database integration tests]]
2. [[Software Engineering - ]]
3. [[Software Engineering - ]]
4. [[Software Engineering - ]]
5. [[Software Engineering - ]]
6. [[Software Engineering - ]]
7. [[Software Engineering - ]]
8. [[Software Engineering - ]]
9. [[Software Engineering - ]]
10. [[Software Engineering - ]]
11. [[Software Engineering - ]]
12. [[Software Engineering - Linting]]
# Query languages
1. [[_MS_SQL]]
2. [[Backend Engineering - API architectures - GraphQL]]
# Python
[[_Python]]
# Projects to do
- [[Software Engineering - Projects to do]]
	- [[Software Engineering - Projects to do - Data and ML platform]]
		- [[Software Engineering - Projects to do - Data and ML platform - Python SDK]]
	- [[Software Engineering - Projects to do - RAG system]]
	- [[Software Engineering - Projects to do - Data governance app]]
# Topics to learn
### Integration Testing
Testing multiple components together:
- Database integration tests
- API integration tests
- Message broker integration tests
- Testing with containers
- Test environments
- Dependency injection
### End-to-End (E2E) Testing
Testing the entire system:
- Full user workflows
- Black-box testing
- Environment management
- Test data preparation
- Flaky tests
### API Testing
Very important for backend engineers:
- REST API testing
- gRPC testing
- Contract testing
- Schema validation
- Authentication testing
- Error handling testing
### Database Testing
Topics:
- Migration testing
- Transaction testing
- Repository testing
- Data consistency tests
- Query testing
- Performance of queries
### Distributed Systems Testing
This is where advanced backend engineering becomes interesting:
- Failure testing
- Network partition testing
- Retry testing
- Timeout testing
- Eventual consistency testing
- Idempotency testing
- Concurrency testing
- Chaos engineering
### Concurrent Code Testing
Topics:
- Race conditions
- Deadlocks
- Synchronization bugs
- Deterministic schedulers
- Thread testing
- Stress testing
### Property-Based Testing
Very valuable for systems code:
- Invariants
- Random input generation
- Fuzz testing
- State machine testing
### Performance Testing
Topics:
- Benchmarking
- Microbenchmarks
- Load testing
- Stress testing
- Scalability testing
- Latency percentiles (P50/P95/P99)

Tools:
- JMH (Java)
- Google Benchmark (C++)
- k6
- JMeter
### Reliability Testing
Topics:
- Resilience testing
- Soak testing
- Recovery testing
- Failover testing
- Disaster recovery testing
### Security Testing
Topics:
- Authentication tests
- Authorization tests
- Input validation
- SQL injection tests
- Fuzzing
- Dependency vulnerability scanning
### CI/CD and Test Infrastructure
Topics:
- Running tests in pipelines
- Test reports
- Coverage reports
- Test containers
- Test environments
- Regression testing
- Continuous testing
### Testing Data Pipelines and ML Systems
Topics:
- Data quality tests
- Schema validation
- Pipeline testing
- Feature tests
- Model validation tests
- Reproducibility tests
- Drift tests

Tools:
- Great Expectations
- Deequ
- MLflow validation pipelines
## Others
- How kafka and other message systems work in more detail, where are events stored, how they are processed
- search and recommendation systems (search indexing, ElasticSearch, OpenSearch)
- real-time systems
- monitoring
- concurrency models
- System architecture patterns - [[Backend Engineering - System architecture patterns|link]] 
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
## Concurrency theory
- threads vs processes
- locks
- mutexes
- semaphores
- monitors
- actor model
- async programming models
- race conditions
- deadlocks
## Operating system concepts
- system calls
- memory management
- filesystems
- networking stack
- containers
- virtualization
## Algorithms and data structures
- complexity analysis
- hash tables
- trees
- graphs
- queues
- heaps
- sorting/searching
## Python
- generators
- decorators
- context managers
- dependency injection
- packaging
- logging
- configuration
- exceptions
- multiprocessing
- profiling
- performance optimization
## Object-oriented design
- SOLID
- composition vs inheritance
- interfaces / protocols
- design patterns
- abstraction
## Testing
- unit tests
- integration tests
- mocking
- fixtures
- property testing
- CI testing
## APIs
- REST
- gRPC
- authentication
- JWT
- OAuth basics
- OpenAPI
## Databases
- transactions
- indexing
- query optimization
- isolation levels
- migrations
- ORM vs raw SQL
## Git
- rebasing
- squash
- cherry-pick
- bisect
- resolving merge conflicts
- trunk-based development
## CI/CD
## Observability
- logs
- metrics
- traces
- distributed tracing
- dashboards
- alerts
## System design
- queues
- caching
- distributed systems
- scaling
- CAP theorem
- consistency
- load balancing
- service discovery
- sharding / replication
## Software architecture
- layered architecture
- hexagonal architecture
- clean architecture
- microservices vs monoliths
- event-driven systems
## Data management
- databases (SQL / NoSQL)
- caching (Redis, CDNs)
- data modeling
- consistency, transactions
## Performance & optimization
- batching
- caching
- indexing
- reducing latency
## Reliability & correctness
- retries
- idempotency
- fault tolerance
- circuit breakers
- bulkheads
## Security
- authentication (JWT, OAuth)
- authorization
- encryption
- rate limiting