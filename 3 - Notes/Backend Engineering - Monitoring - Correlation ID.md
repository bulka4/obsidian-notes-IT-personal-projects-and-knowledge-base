Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
A correlation ID is a unique identifier attached to a request so that we can find and connect all logs related to that request across different components.

For example, a user makes a request:
```
Correlation ID: abc-123
```

The request goes through multiple services:
```
User
 |
API Gateway
 |
Order Service
 |
Payment Service
 |
Database
```

Each service includes the same ID in its logs:
```
API Gateway:
[abc-123] Received checkout request

Order Service:
[abc-123] Created order #456

Payment Service:
[abc-123] Payment failed: timeout

Database:
[abc-123] Transaction rolled back
```

Now each services stores its logs with attached correlation ID and we can search for that ID (`abc-123`) and see the complete story.
