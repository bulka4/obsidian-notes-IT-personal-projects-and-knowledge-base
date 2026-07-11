Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Tracing is a monitoring technique used to understand what happens to a single request as it travels through:
- Multiple services in a distributed system (that's a distributed tracing)
- Different functions within a single application (that's a monolithic tracing)
# Monolithic vs distributed tracing
## Monolithic
In a monolithic application, one request usually goes through one process:
```
User → Application → Database
```

Tracing will show us how much time different functions within a single application took:
```
Request
 ├─ authenticateUser()     10 ms
 ├─ calculatePrice()       50 ms
 ├─ queryDatabase()       200 ms  ← bottleneck
 └─ generateResponse()     20 ms
```
## Distributed
In a microservices system, the same request may travel through many services and tracing will show us how much time each service took to process the request:
```
User
 |
API Gateway        <- 10ms
 |
Auth Service       <- 20ms
 |
Order Service      <- 50ms
 |
Payment Service    <- 1000ms
 |
Inventory Service  <- 30ms
 |
Database           <- 10ms
```
# Why it is needed
Thanks to tracing we know why the system is slow, which components exactly are slow.
# Trace
A trace represents the entire lifecycle of one request.

Example:
```
Trace ID: abc123

User request: "Buy product"

API Gateway       20 ms
   |
Order Service     50 ms
   |
Payment Service  800 ms   <-- bottleneck
   |
Inventory         30 ms
```

The trace tells us:
- which services were called
- in what order
- how long each step took
- where failures happened
# Span
A span represents one operation inside a trace.

Example:
```
Span 1: API Gateway        20 ms
Span 2: Order Service      50 ms
Span 3: Payment Service   800 ms
Span 4: Database query     40 ms
```

A trace is made of many spans.

A span contains information like:
- service name
- operation name
- start time
- end time
- duration
- errors
- metadata (tags)
# How tracing works
A request receives a unique Trace ID:
```
Trace-ID: 12345
```

Each service / function passes it along:
```
API Gateway
Trace-ID: 12345
      |
      v
Order Service
Trace-ID: 12345
      |
      v
Payment Service
Trace-ID: 12345
```

Each service / function creates spans - calculates on its own how much time it took to process the request:
```
Trace 12345

Span A: API Gateway
Span B: Order Service
Span C: Payment Service
```

The tracing backend then reconstructs the whole request path.