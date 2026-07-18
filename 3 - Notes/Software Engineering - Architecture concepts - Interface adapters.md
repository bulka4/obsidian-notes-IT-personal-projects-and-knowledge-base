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

They include:
# Controllers
Convert HTTP requests into use case calls. For example, a REST API controller which takes a request:
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
# Presenters
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
# Repositories
Repositories ([[Software Engineering - Architecture concepts - Repository|link]]) convert domain objects ([[Software Engineering - Architecture concepts - Domain objects|link]]) into database operations.

The core defines:
```python
class TableRepository:

    def save(self, table):
        pass
```

Infrastructure implements:
```python
class PostgresTableRepository(TableRepository):

    def save(self, table):
        sql = """
        INSERT INTO tables ...
        """

        database.execute(sql)
```

Translation:
```
Domain object → SQL query
```
# Gateways/Adapters
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
# Event Adapters
Example: publishing domain events.

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