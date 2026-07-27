Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Interface adapters are the layer ([[Software Engineering - Architecture concepts - Layer|link]]) that converts data between the outside world and the application's core.

The purpose is to keep the core independent of frameworks and technologies. The core does not know whether the adapter uses PostgreSQL, MongoDB, REST, Kafka, etc.

They sit between external systems and use cases / entities ([[Software Engineering - Architecture concepts - Entity|link]], [[Software Engineering - Architecture concepts - Use case|link]]):
```
Frameworks / External systems
          ↓
Interface Adapters
          ↓
Use Cases / Entities
```
# What interface adapters include
Interface adapters include:
## Controllers
A controller:
- Takes an input from any source (e.g. a HTTP request)
- Calls a function (usually a use case) using data from the input
- Converts a value returned by a use case into a proper format (required by other parts of the system that will use this controller) and returns it

For example, a controller can be a REST API controller which takes a request:
```
POST /tables

{
  "name": "customers"
}
```

and performs some action using data from this request:
```python
class TableController:

    def create_table(self, request):
        command = CreateTableCommand(
            name=request["name"]
        )

        self.create_table_use_case.execute(command)
```
## Presenters
Presenters convert use case ([[Software Engineering - Architecture concepts - Use case|link]]) results (function outputs) into a different format which is used by  UI. Presenter's output is an API response.

For example, a use case after creating a table returns a domain object ([[Software Engineering - Architecture concepts - Domain objects|link]]):
```python
Table(
    id=1,
    name="customers"
)
```

Presenter converts it into a response model (API response):
```python
class TablePresenter:

    def present(self, table):
        return {
            "tableId": table.id,
            "tableName": table.name
        }
```

Translation:
```
Domain object → API response
```
## Repositories
Repository ([[Software Engineering - Architecture concepts - Repository|link]]) is an interface ([[Software Engineering - Architecture concepts - Interface|link]]) for reading / saving domain objects ([[Software Engineering - Architecture concepts - Domain objects|link]]) in a database.

So it converts domain objects into database operations (e.g. a SQL query).

For example, this can be a class like this:
```python
from abc import ABC, abstractmethod

# Repository interface
class OrderRepository(ABC):

    @abstractmethod
    def get(self, order_id: int):
        """Retrieve an Order aggregate by its ID."""
        pass

    @abstractmethod
    def save(self, order):
        """Persist an Order aggregate."""
        pass
```

So we don't provide here any specific implementation of the methods `get` and `save`.
## Gateways/Adapters
Convert calls to external services (hide external APIs).

Core interface:
```python
class LLMClient:

    def generate(self, prompt):
        pass
```

Adapter:
```python
class OpenAIAdapter(LLMClient):

    def generate(self, prompt):
        return openai.chat.completions.create(
            model="gpt-5",
            messages=prompt
        )
```

Translation:
```
Application request → OpenAI API call
```
## Event Adapters
Example: publishing domain events in event-driven systems ([[Backend Engineering - Event-driven architecture (EDA)|link]]).

Core:
```python
class EventPublisher:

    def publish(self, event):
        pass
```

Adapter:
```python
class KafkaEventPublisher(EventPublisher):

    def publish(self, event):
        kafka.send(event)
```

Translation:
```
Domain event → Kafka message
```