Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Hexagonal architecture (also called Ports and Adapters) is an evolution of layered architecture that tries to solve one major problem:
> The business logic should not depend on technical details like databases, Kafka, REST APIs, OpenAI SDKs, etc.

The key idea is:
```
        REST API
            |
        Controller
            |
      +-------------+
      |             |
DB <--| Application |--> Kafka
      |   Domain    |
LLM <-|             |--> Email
      +-------------+
```

The application/core is in the middle, and everything external connects through ports.
# Components
## 1. Core (Domain + Application)
Contains:
- entities ([[Software Engineering - Architecture concepts - Entity|link]])
- business rules
- use cases ([[Software Engineering - Architecture concepts - Use case|link]])
- interfaces ([[Software Engineering - Architecture concepts - Interface|link]])

We don't make imports like:
```python
# BAD
import sqlalchemy
import kafka
import openai
```

because the core should not know anything about frameworks and other technical details (which technologies are used).
## 2. Ports
Ports are interfaces ([[Software Engineering - Architecture concepts - Interface|link]]).

Example: Repository port
```python
class TableRepository:

    def save(self, table):
        pass

    def get(self, id):
        pass
```

The application depends on this interface.

Example: LLM port
```python
class LlmClient:

    def generate(self, question, docs):
        pass
```

Example: Event Publisher port
```python
class EventPublisher:

    def publish(self, event):
        pass
```
## 3. Adapters
Adapters implement the ports (they are interface implementations ([[Software Engineering - Architecture concepts - Interface|link]])).

PostgreSQL adapter
```python
class SqlTableRepository(TableRepository):

    def save(self, table):
        session.add(table)
```

OpenAI adapter
```python
class OpenAiClient(LlmClient):

    def generate(self, question, docs):
        ...
```

Kafka adapter
```python
class KafkaPublisher(EventPublisher):

    def publish(self, event):
        ...
```
# Input and Output ports
Usually we distinguish:
## Input port
Interface for calling the application:
```python
class AnswerQuestionUseCase:
    def execute(question)
```

Controller calls it.
## Output port
Interface used by the application:
```python
class LlmClient:
```

Implemented by adapters.
# Example
In an e-commerce app, we could have such code in different layers:
## Core (Application + Domain)
The core contains the business logic and use cases. It does not know about external dependencies, like databases used.

A domain object (entity) with business rules could be:
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

The business rule: Only pending orders can be confirmed.

Application use case that coordinates the workflow could be:
```python
class ConfirmOrderUseCase:

    def __init__(
        self,
        order_repository
    ):
        self.order_repository = order_repository


    def execute(self, order_id):

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
2. Call domain logic
3. Save changes
```
## Ports
Ports define how the Core communicates with the outside world.

For example, the use case needs to store orders.

It defines a port:
```python
class OrderRepository:

    def get(self, order_id):
        pass

    def save(self, order):
        pass
```

The Core says:
> "I need something that can save and load orders."

It does not say which specific technology to use (e.g. PostgreSQL).
## Adapters
We could have an input adapter which prepares a response for a HTTP request like this:
```python
class OrderController:

    def __init__(
        self,
        confirm_order_use_case
    ):
        self.confirm_order_use_case = (
            confirm_order_use_case
        )


    def confirm_order(self, request):

        self.confirm_order_use_case.execute(
            request.order_id
        )

        return {
            "status": "OK"
        }
```

and output adapter that implements the port (it defines methods for reading and saving data):
```python
class SqlOrderRepository(
    OrderRepository
):
    def __init__(self, db):
        self.db = db

    def get(self, order_id):
        row = self.db.query(...)

        return Order(row["id"], row["status"])

    def save(self, order):
        self.db.execute(...)
```
## Dependency injection
In Hexagonal Architecture, dependency injection connects adapters to ports.

Example:
```python
# External system
db = DatabaseConnection()

# Output adapter
repository = SqlOrderRepository(
    db
)

# Core
confirm_order_use_case = ConfirmOrderUseCase(
    repository
)

# Input adapter
controller = OrderController(
    confirm_order_use_case
)
```

The wiring happens outside the core.
## Full dependency flow
```
                 HTTP Request
                      |
                      v
            +----------------+
            | HTTP Adapter   |
            | Controller     |
            +----------------+
                      |
                      |
                      v
              +---------------+
              |               |
              |     CORE      |
              |               |
              | ConfirmOrder  |
              | Use Case      |
              |               |
              | Order Entity  |
              |               |
              +---------------+
                      |
                      |
                 OrderRepository
                    (PORT)
                      ^
                      |
                      |
          +-----------------------+
          | SQL Adapter            |
          | SqlOrderRepository     |
          +-----------------------+
                      |
                      v
              Database
```
# Comparison to other architectures
## Layered architecture
Hexagonal architecture looks like the layered architecture ([[Software Engineering - Layered architecture|link]]) where:
- Application and domain layers are combined 
	- It is like the Core component in the hexagonal architecture (those layers can still be separated but they are both considered the Core)
- The domain and application layers contain interfaces ([[Software Engineering - Architecture concepts - Interface|link]]), so they only describes what operations are available but not how they are implemented
	- It is like ports in the hexagonal architecture
- Infrastructure layer contains implementations of interfaces from the domain and application layers
	- It is like adapters in the hexagonal architecture
- A presentation layer (HTTP controllers, CLI, message consumers, etc.) in the layered architecture can be input (driving/primary) adapters in the hexagonal architecture
# Advantages
- Easier testing (mock ports).
- Easier swapping technologies.
- Better separation between business logic and infrastructure.
- Core remains framework-independent.
# Disadvantages
- More abstractions.
- More interfaces and classes.
- Can be overkill for simple CRUD applications.