Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Layered architecture** (also called **n-tier architecture**) is a way of organizing an application into layers, where each layer has a specific responsibility and usually communicates only with adjacent layers.

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
Contains application use cases and coordinates business operations. For example, functions for:
- Creating user
- Generating invoice
- Training model
- Sending notification

It usually:
- orchestrates workflows,
- manages transactions,
- calls domain objects and repositories.

Example:
```
CreateUserService
```

might:
1. Validate business rules
2. Create domain objects
3. Save them
4. Send an email
# 3. Domain Layer
Contains the core business logic and business rules. For example:
- Classes:
	```
	User
	Order
	Invoice
	RecommendationModel
	```
- Entities (objects in a business domain, e.g. table, document)
- Value objects (objects defined only by its value, e.g. address, table name)
- Business rules
- Domain services (business logic that depends on multiple entities)
- Domain events (e.g. document created, model promoted)

This layer should ideally be independent of:
- databases,
- frameworks,
- HTTP,
- UI.

Example business rule:
```
An order cannot be shipped before payment.
```

This belongs in the domain layer.
# 4. Infrastructure Layer
Responsible for technical details:

Examples:
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