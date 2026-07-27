Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Layered architecture (also called n-tier architecture) is a way of organizing an application into layers ([[Software Engineering - Architecture concepts - Layer|link]]), where each layer has a specific responsibility and usually communicates only with adjacent layers.

A typical backend application looks like:
```
Presentation Layer
        ↓
Application / Service Layer
        ↓
Domain Layer
        ↓
Infrastructure / Data Access Layer
        ↓
Database
```
# 1. Presentation Layer
Responsible for interacting with users or external systems.

Examples:
- REST controllers
- GraphQL endpoints
- Web pages
- API request validation
- Authentication handling

Example:
```python
@app.post("/tables")
def create_table(request: CreateTableRequest):
    service.create_table(request)
```

The controller receives the request and calls the service layer.
# 2. Application (Service) Layer
Contains:
- Use cases ([[Software Engineering - Architecture concepts - Use case|link]]) 
- Application services ([[Software Engineering - Architecture concepts - Application Service|link]])
- Commands / Queries ([[Software Engineering - Architecture concepts - Command|link]], [[Software Engineering - Architecture concepts - Query|link]])
- DTOs ([[Software Engineering - Architecture concepts - DTO (Data Transfer Object)|link]])
- coordinates business operations. 

For example, functions for:
- Creating user
- Load and save order
- Publish events ([[Backend Engineering - Event-driven architecture (EDA)|link]]), send emails, etc.

It usually:
- orchestrates workflows,
- manages transactions,
- calls domain objects ([[Software Engineering - Architecture concepts - Domain objects|link]]) and repositories ([[Software Engineering - Architecture concepts - Repository|link]]).

Example:
```
CreateUserService
```

might:
1. Validate business rules
2. Create domain objects
3. Save them
4. Send an email

It might use interfaces ([[Software Engineering - Architecture concepts - Interface|link]]) to specify what operations are available but not how they are implemented (e.g. those interfaces can be classes with specified methods for payments, sending emails, reading data from a database but methods logic is not defined).
# 3. Domain Layer
Contains the core business logic and business rules. For example:
- Classes:
	```
	User
	Order
	Invoice
	RecommendationModel
	```
- Entities ([[Software Engineering - Architecture concepts - Entity|link]])
- Value objects ([[Software Engineering - Architecture concepts - Value object|link]])
- Aggregates ([[Software Engineering - Architecture concepts - Aggregate|link]])
- Business rules
- Domain services ([[Software Engineering - Architecture concepts - Domain Service|link]])
- Domain events ([[Software Engineering - Architecture concepts - Domain event|link]])

This layer should ideally be independent of:
- databases,
- frameworks,
- HTTP,
- UI.
So it should use interfaces instead of specific implementations of those interfaces ([[Software Engineering - Architecture concepts - Interface|link]]).

For example:
```python
class Order:
    def confirm(self):
        if self.status != "PENDING":
            raise Exception(
                "Only pending orders can be confirmed"
            )

        self.status = "CONFIRMED"
```

This belongs in the domain layer.
# 4. Infrastructure Layer
Responsible for technical details:

For example, it can contain code which interacts with:
- SQL databases
- Kafka producers
- Redis
- Email clients
- External APIs
- File storage

Code examples:

Repositories:
```python
class SqlTableRepository:
    def save(table):
        session.add(table)

    def get(id):
        return session.query(...)
```

Vector DB:
```python
class ChromaRepository:
    def search(question):
        ...
```

LLM client:
```python
class OpenAIClient:
    def generate(question, docs):
        ...
```

Kafka:
```python
class KafkaPublisher:
    def publish(event):
        ...
```
# Dependency injection
Usually in the Presentation layer we perform a dependency injection ([[Software Engineering - Dependency injection|link]]), i.e. we specify which classes we want to use (e.g. as interface implementations) by providing them as arguments.

Usually, those are classes for interacting with infrastructure we want to use.
# Advantages
- Separation of responsibilities.
- Easier maintenance.
- Easier testing.
- Teams can work on different layers independently.
- Business logic is easier to locate.
# Disadvantages
- Can become overly rigid.
- Changes sometimes require touching many layers.
- Risk of creating "pass-through layers":
	```
	Controller → Service → Repository
	```
	
	where each layer only forwards calls.
- Large systems may become difficult to evolve if all logic accumulates in services.
# Example
For example, in an e-commerce app for making orders, those four layers could look like this:
## 1. Presentation layer
Receives HTTP requests and returns HTTP responses.
```python
class OrderController:
    def __init__(self, confirm_order_use_case: ConfirmOrderUseCase):
        self.confirm_order_use_case = confirm_order_use_case

    def confirm_order(self, order_id):

        self.confirm_order_use_case.execute(
            order_id
        )

        return {
            "status": "OK"
        }
```

This layer knows about:
- HTTP
- JSON
- API endpoints

It does not know business rules.
## 2. Application layer
Coordinates the workflow.
```python
class ConfirmOrderUseCase:
    def __init__(
        self,
        order_repository: OrderRepository
    ):
        # Repository for handling orders
        self.order_repository = order_repository

    def execute(self, order_id):
	    # Confirm the order
        order = self.order_repository.get(
            order_id
        )

        order.confirm()

        self.order_repository.save(
            order
        )
```

Responsibilities:
```
1. Load order
2. Call business logic
3. Save order
```

No SQL and no HTTP.
## 3. Domain layer
Contains business rules.
```python
class Order:
    def __init__(
        self,
        order_id,
        status
    ):
        self.id = order_id
        self.status = status

    def confirm(self):

        if self.status != "PENDING":
            raise Exception(
                "Only pending orders can be confirmed"
            )

        self.status = "CONFIRMED"
```

This layer contains a business rule:
```
Only pending orders can be confirmed.
```

and knows nothing about:
- databases
- APIs
- HTTP
- repositories

Repository interface also belongs here (or sometimes between domain/application depending on architecture):
```python
class OrderRepository:
    def get(self, order_id):
        pass

    def save(self, order):
        pass
```
## 4. Infrastructure layer
Actual database implementation.
```python
class SqlOrderRepository(
    OrderRepository
):
    def __init__(self, db):
        self.db = db

    def get(self, order_id):
        row = self.db.query(
            """
            SELECT id, status
            FROM orders
            WHERE id = ?
            """,
            order_id
        )

        return Order(
            row["id"],
            row["status"]
        )

    def save(self, order):
        self.db.execute(
            """
            UPDATE orders
            SET status = ?
            WHERE id = ?
            """,
            order.status,
            order.id
        )
```

Infrastructure contains:
- SQL
- ORM
- external APIs
- file systems
- message brokers
## Dependency injection
In the presentation layer, we can perform a dependency injection ([[Software Engineering - Dependency injection|link]]), i.e. to specify which class to use for interacting with the infrastructure (the `SqlOrderRepository` class):
```python
# Infrastructure
db = DatabaseConnection()

repository = SqlOrderRepository(db)

# Application
confirm_order_use_case = ConfirmOrderUseCase(
    repository
)

# Presentation
controller = OrderController(
    confirm_order_use_case
)
```
## Full dependency picture
```
          OrderController
                    |
                    v
       ConfirmOrderUseCase
                    |
                    v
                  Order
                    ^
                    |
        SqlOrderRepository
                    |
                    v
		   DatabaseConnection
```