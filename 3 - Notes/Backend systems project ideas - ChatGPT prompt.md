Tags: [[__My_projects]]
#MyProjects 

# Introduction
I want to build a backend system in java, as simple and fast to do as possible, yet to learn as many useful techniques and tools as possible. 

I don't want to learn some super advanced fancy things that very little people work on but something what is popular on the market, what a lot of people use, so it is very likely that I could use this in my job (and find a job thanks to this knowledge).

I would like to use the following tools and techniques (as much as possible but only those that are likely to be useful when searching for a job. If some of those are very unpopular in jobs on the market, skip them):
- Java and Spring
- Dealing with too many incoming requests - avoiding processing too many requests at once when they come, e.g. using thread pools, backpressure
- concurrency - semaphores, locks, race conditions, deadlocks, async programming
- distributed systems - consensus, partial failures, clock synchronization and logical clocks, conflict resolution, reconciliation
- running multiple threads
- CQRS, backend for frontend, event sourcing, saga, 
- dependency management (e.g. dependency injection)
- monitoring and logging
- fault tolerance
- api design - graphQL, api gateway, streaming API
- data consistency

Give me for now one project idea and focus on describing what problems I would fix and what techniques / tools I would use. 

I already done the projects described below so I would like to do now something where I could learn different things:
# Database documentation with a RAG system
Developed:
- A web application that allows for documenting a SQL database, automatically generating data lineage graphs and provides a semantic search engine.    
- Data lineage graphs are in the form of workflow charts, generated using a custom code that processes SQL queries and calculates coordinates of the chart nodes used to position them on the screen.    
- A RAG system that answers user questions based on the documentation from this application using LangGraph and MCP tools.    

Implemented:
- The microservice architecture - Web app API, semantic search API, MCP server and RAG system are deployed separately.    
- The event-driven architecture - Document update emits an event that triggers asynchronous embedding update.    
- Clean Architecture concepts - Separate business logic from technology-specific implementations.    

Deployed on Azure Kubernetes using Helm with infrastructure provisioned with Terraform.

Designed (but not implemented) how to:
- Collect metrics, logs and traces using Prometheus, Grafana, logging module, Fluent Bit, Loki, OpenTelemetry    
- Handle data inconsistency issues (outdated vector embeddings, making the operation of updating embeddings for all chunks for a document atomic)    
- Make vector embedding ingestion idempotent in case an event is processed twice

Technologies: LangGraph, FastAPI, Ray Serve, Milvus (vector db), MongoDB, [N](http://node.js)ode.j[s](http://node.js), JavaScript, Express, EJS, Kubernetes, Helm, Terraform
# Data and ML platform
Built an end-to-end platform for distributed data processing, experiment tracking, model versioning and automated model retraining workflows.

Set up on this platform a workflow which:
- Is orchestrated using Airflow 
	- Each task runs in a separate Kubernetes pod    
	- Created custom Airflow operators for creating Kubernetes pods, running Spark jobs using Spark Operator and deciding whether or not to continue with downstream tasks based on logs from completed pods
- Ingests incrementally data from a SQL database into Iceberg tables in Azure Data Lake using custom Python code and Azure SDK    
- Transforms data in Data Lake in a distributed way using Spark and dbt    
- Automatically retrains a ML model using a custom logic:
	- Evaluates performance of the current ML model on new data     
	- If performance drops, then it automatically trains multiple new models (using MLflow experiments)     
	- The best new model is deployed into production (saved in the MLflow artifact store)    

Deployed platform services on Kubernetes using Helm and infrastructure provisioned with Terraform.

Technologies: Kubernetes, Helm, Terraform, Airflow, Spark, dbt, MLflow
# To do app
This is in progress.

Create one app using different tech stacks:
- Frontend - React + TypeScript
- Backend:
	- Java + Spring
	- C# + .NET

This is an app allowing users to create a to do list with tasks and adding statuses to those tasks (to do, in progress, completed).

## Further development planned
### Backend operations to implement
1. Authentication and Authorization (users can only access their own tasks))
2. User management
3. Task management (CRUD)
4. Additional operations (filter, search, sort tasks, etc.)
5. Backend infrastructure
	- Input validation
	- Error handling (fault tolerance)
	- Logging
	- API documentation (OpenAPI/Swagger)
6. use async programming to allow executing multiple operations concurrently, for example:
	- loading multiple datasets using `Promise.all()` (e.g. user tasks, profile, notification count)
	- allow users to perform multiple operations at the same time (e.g. Add a task, Update  task's status, Delete a task). Each operation could make an independent API request which are async `async function updateTask() {await fetch("/api/tasks/${id}", ...}`.
7. Develop some plugins
8. Dependency management (e.g. dependency injection)
### Problems
- What if the task list becomes huge?
	- we need to prevent somehow:
		- loading all the data at once because that would take too much time
		- displaying all the tasks at once because that would take too much space and there would be too much scrolling
- Concurrency - what if:
	- user A loads an app
	- user B updates task X
	- user A wants to update task X (but doesn't see the update made by the user B because didn't refresh the app)
	- if user A completed the update, then update made by the user B is lost
	
	try to use OCC ([[Software Engineering - Concurrency patterns - Optimistic Concurrency Control (OCC)|link]])
### Other things to implement
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