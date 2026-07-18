Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Monolith
A **monolith** is an application where all functionality is built and deployed as one unit.

Example:
```
                Application
        ┌─────────────────────┐
        │ Users                │
        │ Payments             │
        │ Orders               │
        │ Recommendations      │
        └─────────────────────┘
                |
             Database
```

Characteristics:
- One codebase
- One deployment
- Usually one database
- Components communicate through function calls

Pros:
- Simple to develop and deploy
- Easier debugging
- Less infrastructure complexity

Cons:
- Harder to scale parts independently
- Large codebase can become difficult to maintain
- One change may require redeploying everything
# Microservices
A **microservices architecture** splits an application into independent services.

Example:
```
User Service       → User DB
Order Service      → Order DB
Payment Service    → Payment DB
Recommendation     → ML system
```

Services communicate through:
- HTTP/gRPC
- Message brokers (Kafka, RabbitMQ)

Characteristics:
- Separate codebases
- Independent deployments
- Often separate databases
- Each service owns a business capability

Pros:
- Scale services independently
- Teams can work independently
- Failures can be isolated
- Different technologies can be used

Cons:
- Much more operational complexity
- Network failures
- Harder debugging
- Data consistency becomes harder
- Requires good DevOps/infrastructure