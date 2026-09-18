Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Interface adapters is a layer ([[Software Engineering - Architecture concepts - Layer|link]]) used in the Clean Architecture ([[Software Engineering - Clean architecture|link]]) that converts data between the outside world and the application's core.

The purpose is to keep the core independent of frameworks and technologies. The core does not know whether the adapter uses PostgreSQL, MongoDB, REST, Kafka, etc.

They sit between external systems and use cases / entities ([[Software Engineering - Architecture concepts - Use case|link]] / [[Software Engineering - Architecture concepts - Entity|link]]):
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
- Converts a value returned by a use case into a proper format and returns it
	- converting is usually done using a presenter, another concept explained further in this document
	- this format is required by other parts of the system that will use this controller

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
Repository ([[Software Engineering - Architecture concepts - Repository|link]]) is a code for reading / saving domain objects ([[Software Engineering - Architecture concepts - Domain objects|link]]) in a database.

So it converts domain objects into database operations (e.g. a SQL query).

For example, this can be a class like this:
```python
class OrderRepository():
    @abstractmethod
    def get(self, order_id: int):
        """Retrieve an Order aggregate by its ID."""
        ...

    @abstractmethod
    def save(self, order):
        """Persist an Order aggregate."""
        ...
```

So we don't provide here any specific implementation of the methods `get` and `save`.
## Gateways/Adapters
An adapter interacts with an external technology and prepares an output that is used by the application. 

For example, it can call an API, transform its result and return it in a proper form that will be used by the application:
```python
@dataclass 
class SearchResult:
	productID: str
	productName: str
	
def search(query):
	api_result = api.call(query)
	
	return SearchResult(
		productID=api_result["product_id"]
		productName=api_result["name"]
	)
```

Common examples include:
- API adapter - calls an API
- Database adapter - reads / writes data to a database
- Model adapter - uses a ML model
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
# Inbound vs outbound adapters
Usually we have inbound and outbound adapters:
- Inbound adapters takes requests from external systems and call use cases to prepare a response
- Outbound adapters are used by use cases to interact with external technologies

For example, we can have a use case for semantic search:
```python
class SemanticSearch:
    """Use case."""
    def __init__(...):
        ...

    def execute(...):
	    # generate an embedding
        embedding = self.embedding_model.embed(query)
        # find similar documents in a vector store
        return self.vector_store.search(embedding, top_k)
```

For example, we can have a use case for placing an order:
```python
class PlaceOrder:
    def __init__(self, repository: OrderRepository):
        self.repository = repository

    def execute(self, product_id: int, quantity: int) -> Order:
        if quantity <= 0:
            raise ValueError("Quantity must be positive")

        order = Order(product_id, quantity)
        self.repository.save(order)

        return order
```

an outbound adapter for saving order data in a PostgreSQL database:
```python
class PostgresOrderRepository:
    def save(self, order: Order) -> None:
        # PostgreSQL-specific code would go here
        print(f"Saving order to PostgreSQL: {order}")
```

and an inbound adapter for handling an order that uses the use case for placing an order:
```python
class OrderController:
    def __init__(self, place_order: PlaceOrder):
        self.place_order = place_order

    def handle(self, product_id: int, quantity: int):
        order = self.place_order.execute(product_id, quantity)

        # Convert application result to HTTP/API response
        return {
            "product_id": order.product_id,
            "quantity": order.quantity,
        }
```

How they are used together:
```python
repository = PostgresOrderRepository()
use_case = PlaceOrder(repository)
controller = OrderController(use_case)

response = controller.handle(product_id=123, quantity=2)
```