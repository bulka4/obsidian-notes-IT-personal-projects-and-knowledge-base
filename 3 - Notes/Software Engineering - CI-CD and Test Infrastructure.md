Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**CI/CD and test infrastructure** refers to the automated systems and processes that run tests continuously as part of software development and delivery.

The idea:
> "Automatically verify code quality and correctness every time code changes."

It is not a type of testing itself; it is the **automation platform that enables testing to happen consistently and repeatedly**.
# CI (Continuous Integration)
Checks code when developers make changes.

Example:
```
Developer commits code
        ↓
CI pipeline starts
        ↓
Build application
        ↓
Run tests
        ↓
Report results
```

Typical CI checks:
- unit tests
- integration tests
- security scans
- code quality checks
- dependency vulnerability scans
# CD (Continuous Delivery/Deployment)
Automates releasing software.

Example:
```
Tests pass
     ↓
Build Docker image
     ↓
Deploy to staging
     ↓
Deploy to production
```
# Test infrastructure
The systems needed to run tests reliably.

Examples:
- test environments
- test databases
- containers
- Kubernetes test clusters
- mock services
- test data generation
- monitoring/logging systems

Example:
```
CI Pipeline

        Code
         |
         v
   Build container
         |
         v
 Start test environment
         |
         v
 Run tests
         |
         v
 Destroy environment
```
# Test examples
For backend systems, CI/CD + test infrastructure often includes:
- automated unit/integration tests
- Docker-based test environments
- database migration tests
- API tests
- performance tests
- security scans