Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Materials to learn from
1. [[Backend Engineering - Materials to learn from]]
# Application communication
1. [[Backend Engineering - Application communication]]
## Application communication concepts
1. [[Backend Engineering - Latency and throughput]]
	1. [[Backend Engineering - Latency metrics]]
## Synchronous and asynchronous communication
1. [[Backend Engineering - Synchronous vs asynchronous communication]]
### Asynchronous request processing
1. [[Backend Engineering - Asynchronous request processing]]
	1. [[Backend Engineering - Asynchronous request processing - Benefits and drawbacks]]
	2. [[Backend Engineering - Asynchronous request processing - Message queue]]
	3. [[Software Engineering - Event-driven architecture (EDA)]]
	4. [[Backend Engineering - Asynchronous request processing - Sending back a response]]
		1. [[Backend Engineering - Asynchronous request processing - Sending back a response using pooling]]
		2. [[Backend Engineering - Asynchronous request processing - Sending back a response using webhook (callback)]]
		3. [[Backend Engineering - Asynchronous request processing - Sending back a response using WebSockets]]
		4. [[Backend Engineering - Asynchronous request processing - Sending back a response via shared storage]]
## Networking
[[_Networking]]
### Protocols
1. [[Networking - Protocols]]
   Protocols for the application layer:
	1. [[Networking - Protocols - HTTP]]
	2. [[Networking - Protocols - gRPC]]
	3. [[Networking - Protocols - WebSockets]]
	4. [[Networking - Protocols - SOAP (Simple Object Access Protocol)]]

	Protocols for the transport layer:
	5. [[Networking - Protocols - TCP]]
	6. [[Networking - Protocols - UDP]]
## Performance optimization
1. [[Backend Engineering - Application communication - Performance optimization]]
	1. [[Backend Engineering - Request batching]]
	2. [[Backend Engineering - Caching]]
# APIs
## API concepts
1. [[Backend Engineering - API]]
	1. [[Backend Engineering - Running an API]]
	2. [[Backend Engineering - API endpoint, route and handler]]
	3. [[Backend Engineering - API (HTTP, gRPC, etc.) server]]
## API design
1. [[Backend Engineering - API design principles]]
	1. [[Backend Engineering - Bulk endpoints]]
	2. [[Backend Engineering - API versioning]]
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
# Security
1. [[Backend Engineering - Security]]
	1. Secure protocols:
		1. [[Networking - Security - TLS]]
		2. [[Networking - Security - HTTPS]]
	2. [[Backend Engineering - Security - Authorization vs authentication]]
	3. Authentication:
		1. [[Backend Engineering - Security - Token-based authentication]]
			1. [[Backend Engineering - Security - JWT access token format]]
			2. [[Backend Engineering - Security - API key]]
		2. [[Backend Engineering - Security - SASL (Simple Authentication and Security Layer)]]
	4. Authorization:
		1. [[Backend Engineering - Security - OAuth2]]
		2. [[Backend Engineering - Security - RBAC authorization]]
		3. [[Backend Engineering - Security - ABAC authorization]]
		4. [[Backend Engineering - Security - Policy engine]]
		5. [[Backend Engineering - Security - ACL (Access Control List)]]
	5. Others:
		1. [[Backend Engineering - API architectures - API gateway]]
		2. [[Backend Engineering - Rate limiting]]
			1. [[Backend Engineering - Token bucket]]
			2. [[Software Engineering - Fault tolerance - Circuit breakers]]
# Distributed systems
1. [[Backend Engineering - Distributed systems]]
	1. [[Backend Engineering - Fault tolerance - Distributed systems]]
		1. [[Backend Engineering - Distributed systems - Partial failures]]
		2. [[Backend Engineering - Distributed systems - Consensus]]
			1. [[Backend Engineering - Distributed systems - FLP impossibility]]
	2. [[Backend Engineering - Distributed systems - Service discovery]]
	3. [[Backend Engineering - Distributed systems - CAP theorem]]
	4. [[Backend Engineering - Distributed systems - Backpressure]]
	5. [[Backend Engineering - Distributed systems - Load balancing]]
	6. [[Backend Engineering - Distributed systems - Clock (time) synchronization]]
	7. [[Backend Engineering - Distributed systems - Logical clocks (timestamps)]]
		1. [[Backend Engineering - Distributed systems - Lamport logical clock]]
		2. [[Backend Engineering - Distributed systems - Vector clocks]]
	8. [[Backend Engineering - Distributed systems - Conflict resolution]]
		1. [[Backend Engineering - Conflict resolution - Last Write Wins (LWW)]]
		2. [[Backend Engineering - Conflict resolution - CRDTs (Conflict-free Replicated Data Types)]]
## Data Consistency Patterns
1. [[Backend Engineering - Distributed systems - Data Consistency Patterns (distributed transactions)]]
	1. [[Backend Engineering - Data Consistency Patterns - Consistency boundaries]]
	2. [[Software Engineering - Architecture patterns - Saga]]
		- [[Software Engineering - Saga pattern - Choreography (event-driven) type]]
		- [[Software Engineering - Saga pattern - Orchestration type]]
	3. [[Backend Engineering - Data Consistency Patterns - 2PC]]
	4. [[Backend Engineering - Data Consistency Patterns - TCC]]
	5. [[Backend Engineering - Data Consistency Patterns - Outbox pattern]]
## Consistency models
1. [[Backend Engineering - Distributed systems - Consistency models]]
	1. [[Backend Engineering - Consistency models - Strong consistency]]
	2. [[Backend Engineering - Consistency models - Sequential consistency]]
	3. [[Backend Engineering - Consistency models - Causal consistency]]
	4. [[Backend Engineering - Consistency models - Eventual consistency]]
	5. [[Backend Engineering - Consistency models - Weak consistency]]
	6. [[Backend Engineering - Consistency models - Read-your-writes  consistency]]
	7. [[Backend Engineering - Consistency models - Monotonic reads consistency]]
	8. [[Backend Engineering - Consistency models - Session consistency]]
# Monitoring
1. [[Backend Engineering - Monitoring]]
	1. [[Backend Engineering - Monitoring - Tracing]]
	2. [[Backend Engineering - Monitoring - Traces vs metrics vs logs]]
	3. [[Backend Engineering - Monitoring - Correlation ID]]
	4. [[Backend Engineering - Monitoring - service-level indicators (SLIs) and service-level objectives (SLOs)]]
	5. [[Backend Engineering - Monitoring - Tools for logging]]
		1. [[Python - Tools - Monitoring - The logging module]]
		2. [[Containers - Monitoring - Container log files]]
# Data storage
1. [[Backend Engineering - Data storage - Replication]]
2. [[Backend Engineering - Data storage - Sharding (partitioning)]]
	1. [[Backend Engineering - Sharding (partitioning) - Range partitioning]]
	2. [[Backend Engineering - Sharding (partitioning) - Hash partitioning]]
	3. [[Backend Engineering - Sharding (partitioning) - Directory-based partitioning]]
	4. [[Backend Engineering - Sharding (partitioning) - Consistent hashing]]
## Databases
[[_Databases]]
# Backend infrastructure
1. [[Backend Engineering - Infrastructure - Serverless API]]
# Tools
1. [[Backend Engineering - Tools - Backend frameworks]]