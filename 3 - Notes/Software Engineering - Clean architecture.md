Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Clean Architecture is an architecture that aims to make the business logic independent of frameworks, databases, UI, and external services.
# The main idea
```
Frameworks / UI / Database / External APIs
                    ↓
            Application Layer
                    ↓
               Domain Layer
```

Dependencies always point inward - i.e. the inner layers (lower in the graph) should not depend on outer layers.
# Typical layers
```
┌─────────────────────┐
│ Frameworks & Drivers│
├─────────────────────┤
│ Interface Adapters  │
├─────────────────────┤
│ Use Cases           │
├─────────────────────┤
│ Entities            │
└─────────────────────┘
```
## Entities
This layer contain entities ([[Software Engineering - Architecture concepts - Entity|link]]) with business rules. For example, a class:
```python
class Order:

    def confirm(self):
        if self.status != "PENDING":
            raise Exception()

        self.status = "CONFIRMED"
```

It doesn't have to contain only interfaces ([[Software Engineering - Architecture concepts - Interface|link]]).
## Use cases (Application layer)
This layer contain use cases ([[Software Engineering - Architecture concepts - Use case|link]]), i.e. application logic - additional operations not defined in entities, for example:
```python
class ConfirmOrderUseCase:

    def execute(self, order_id):
        order = self.repository.get(order_id)
        order.confirm()
        self.repository.save(order)
```

Use cases perform operations on entities. This layer doesn't have to contain only interfaces ([[Software Engineering - Architecture concepts - Interface|link]]).
## Interface adapters
The Interface adapters layer contains:
- Controllers - take HTTP requests and uses them to perform use case calls (call functions)
- Presenters - convert use case ([[Software Engineering - Architecture concepts - Use case|link]]) results (function outputs) into a different format which is used by  UI
- Repositories - interfaces ([[Software Engineering - Architecture concepts - Interface|link]]) for reading / saving domain objects ([[Software Engineering - Architecture concepts - Domain objects|link]]) in a database.
- Gateways/adapters
- Event adapters

It converts data between the outside world and the core.

More info here - [[Software Engineering - Architecture concepts - Interface adapters]].
## Frameworks & Drivers
This layer contain logic for functions / methods which is related and dependent on technical details, like:
```
FastAPI
PostgreSQL
Kafka
OpenAI SDK
```

For example, it can contain a function for reading data from a specific database.
# Dependency rule
The core (i.e. inner layers, entities and use cases) should not know about what frameworks we use, so we should avoid doing something like:
```python
import fastapi
import sqlalchemy
import openai
```

Instead, the outer layers depend on the inner layers, i.e. the code in an outer layer uses code from an inner layer.
# Example
In an e-commerce app, we could have such code in different layers:
## Entities
The entity knows only business rules. We could have here such code as:
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

The domain knows nothing about:
- HTTP
- databases
- FastAPI
- repositories
- SQLAlchemy

It only knows:
> "An order can be confirmed if it is pending."
## Use cases (Application layer)
Contains use cases, operations on entities. For example, we could have here a code like this:
```python
class ConfirmOrderUseCase:

    def __init__(
        self,
        order_repository
    ):
        self.order_repository = order_repository


    def execute(self, order_id):
		# Load and order, confirm it and save
        order = self.order_repository.get(
            order_id
        )

        order.confirm()

        self.order_repository.save(
            order
        )
```

The application layer depends on the domain because it uses the `order` object which is an object of the `Order` class:
```python
order.confirm()
```

The dependency is:
```
ConfirmOrderUseCase
          |
          v
        Order
```
## Interface adapters
Contains things that translate between the outside world and the core.
### Controller
A controller can convert the output of the `confirm_order_use_case.execute` use case into a different format:
```python
class OrderController:

    def __init__(
        self,
        confirm_order_use_case
    ):
        self.confirm_order_use_case = (
            confirm_order_use_case
        )


    def confirm(self, order_id):

        self.confirm_order_use_case.execute(
            order_id
        )

        return {
            "status": "OK"
        }
```

So the controller depends on the `confirm_order_use_case.execute()` use case:
```
OrderController
        |
        v
ConfirmOrderUseCase
```

but the use case does not know the controller exists.
### Repository implementation
A repository can for example implement functions for interacting with a database.

The `SqlOrderRepository` repository shown below will be used as the `order_repository` attribute in the `ConfirmOrderUseCase` use case:
```python
class SqlOrderRepository:

    def __init__(self, db):
        self.db = db


    def get(self, order_id):

        row = self.db.query(
            "SELECT id, status FROM orders"
        )

        return Order(
            row["id"],
            row["status"]
        )


    def save(self, order):

        self.db.execute(
            "UPDATE orders SET status=?",
            order.status
        )
```

The repository implementation depends on the domain entity - it uses the `Order` entity, so the dependency is like this:
```
SqlOrderRepository
        |
        v
      Order
```
## Frameworks & Drivers layer
Contains external technology.

Example:
```python
from fastapi import FastAPI

app = FastAPI()
```

or:
```python
database = PostgreSQLConnection()
```
### Dependency injection
In the Frameworks & Drivers layer we perform a dependency injection:
```python
database = PostgreSQLConnection()

repository = SqlOrderRepository(
    database
)

use_case = ConfirmOrderUseCase(
    repository
)

controller = OrderController(
    use_case
)
```
## Full dependency picture
```
                 FastAPI
                    |
                    v
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
               PostgreSQL
```

Notice the direction:
```
Outer → Inner
```

Examples:
```
Controller → UseCase
UseCase → Order
Repository → Order
```
# Relationship to Hexagonal Architecture
In the clean architecture:
- Entities and use cases have separate layers while in the hexagonal architecture they are included in the Core
- Interface adapters are the same as adapters in the hexagonal architecture
- Interfaces in inner layers (entities and use cases) used for communication with external systems are the same as ports in the hexagonal architecture
- Frameworks & drivers are the same as external systems in the hexagonal architecture
