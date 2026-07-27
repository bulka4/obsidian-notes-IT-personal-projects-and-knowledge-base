Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
In software, dependencies are components that another component requires in order to work.

A dependency can be:
- another class/object
- a module/library
- a service
- a database connection
- a configuration object
- a file
- an API client
- a function
# Examples
## Class / object dependency
One class can depend on another class, for example here the `OrderService` class depends on the `repository` object (which is an object of some class):
```python
class OrderService:
    def __init__(self, repository):
        self.repository = repository
        
    def get(self, order_id):
	    return self.repository.get(order_id)
```

`OrderService` cannot work without the `repository` object - we can't use `OrderService.get` if the `repository` object doesn't provide it.
# What is dependency management?
Dependency management is the process of controlling how dependencies are:
- added
- discovered
- configured
- updated
- versioned
- removed
- shared between components

The goal is to keep dependencies:
- stable
- compatible
- maintainable
- easy to replace
# Types of dependencies
## 1. Internal dependencies
Dependencies between parts of the same application.

Example:
```
Order module
      ↓
Payment module
```

The Order module depends on the Payment module within the same application.
## 2. External dependencies
Dependencies provided by external systems or libraries.

Example: 
- Importing libraries
- Using external APIs
## 3. Runtime dependencies
Dependencies required while the application is running.

Examples:
- database
- Redis
- message queue
- external API
## 4. Development dependencies
Dependencies only needed during development.

Examples:
- testing frameworks
- linters
- code formatters
# Dependency problems
## 1. Tight coupling
When a component directly depends on a specific implementation:
```python
class OrderService:
    def __init__(self):
        self.repository = PostgreSQLRepository()
```

Now `OrderService` is coupled to PostgreSQL.

Changing to MongoDB requires changing the code.
## 2. Dependency conflicts
Different components may require different versions:
```
Application
 |
 ├── Library A → requests 2.31
 |
 └── Library B → requests 2.25
```

The application must resolve the conflict.
## 3. Dependency explosion
Large applications can accumulate many dependencies:
```
Application
 |
 ├── Library A
 │      |
 │      └── Library C
 |
 └── Library B
        |
        └── Library D
```

This increases:
- security risks
- update complexity
- maintenance cost
# Dependency management techniques
## 1. Package managers
Tools that download and manage external dependencies.

Examples:
- Python: pip, poetry, conda
- Java: Maven, Gradle
- .NET: NuGet

They manage:
- installation
- versions
- transitive dependencies
## 2. Version management
Dependencies should use controlled versions (i.e. when we use a dependency, we should provide a specific version that we use, not a default, unknown one).

Example:
```
numpy==2.0.0
```

or:
```
numpy>=2.0,<3.0
```

This prevents unexpected breaking changes.
## 3. Dependency isolation
Different applications should have isolated environments, i.e. they should run in environments with separate dependencies.

For example, in Python we can use virtual environment or run different applications in different containers ([[Software Engineering - Containers|link]]).
## 4. Dependency inversion
High-level business logic should depend on abstractions instead of concrete implementations (i.e. to use interfaces ([[Software Engineering - Architecture concepts - Interface|link]]).
# Dependency Injection
Dependency Injection ([[Software Engineering - Dependency injection|link]]) is a technique for providing dependencies from outside instead of creating them inside a component.

Without DI:
```python
class OrderService:
    def __init__(self):
        self.repository = PostgreSQLRepository()
```

With DI:
```python
class OrderService:
    def __init__(self, repository):
        self.repository = repository
```

The dependency is provided externally, as an argument (which we can easily change):
```python
service = OrderService(PostgreSQLRepository())
```

Benefits:
- easier testing
- easier replacement of implementations
- lower coupling
# Dependency graph
Applications can be represented as dependency graphs (components at the top depends on components at the bottom):
```
UserController
       ↓
UserService
       ↓
UserRepository
       ↓
Database
```

Managing this graph is an important part of software architecture.