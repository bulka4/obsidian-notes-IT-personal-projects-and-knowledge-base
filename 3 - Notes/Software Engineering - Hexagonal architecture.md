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
- entities (objects in a business domain, e.g. table, document)
- business rules
- use cases (actions that users or systems perform, e.g. create / delete a document)
- interfaces (ports)

We don't make imports like:
```python
# BAD
import sqlalchemy
import kafka
import openai
```

because the core should not know anything about frameworks.
## 2. Ports
Ports are interfaces ([[Software Engineering - Object-oriented design - Interfaces|link]]).

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
Adapters implement the ports.

PostgreSQL adapter
```
class SqlTableRepository(TableRepository):

    def save(self, table):
        session.add(table)
```

OpenAI adapter
```
class OpenAiClient(LlmClient):

    def generate(self, question, docs):
        ...
```

Kafka adapter
```
class KafkaPublisher(EventPublisher):

    def publish(self, event):
        ...
```
# Example flow
User:
```
POST /chat
```
↓
Controller Adapter:
```
chat_controller.answer()
```
↓
Core:
```
AnswerQuestionUseCase.execute()
```
↓
Port:
```
llm.generate(...)
```
↓
Adapter:
```
OpenAiClient.generate(...)
```
# Dependency direction
Layered architecture:
```
Controller
    ↓
Service
    ↓
Repository
    ↓
Database
```

Dependencies point downward.

Hexagonal architecture:
```
Database ----\
Kafka --------\
REST ----------> Core
OpenAI -------/
CLI ----------/
```

All dependencies point **towards the core**.

The core does not know whether:
- PostgreSQL is used
- MongoDB is used
- OpenAI is used
- Anthropic is used
- Kafka is used
# Example directory structure
```
src/

core/
├── domain/
├── use_cases/
├── ports/

adapters/
├── rest/
├── postgres/
├── kafka/
├── openai/
├── chromadb/
```
# Input and Output ports
Usually we distinguish:
## Input port
Interface for calling the application:
```
class AnswerQuestionUseCase:
    def execute(question)
```

Controller calls it.
## Output port
Interface used by the application:
```
class LlmClient:
```

Implemented by adapters.
# Comparison
## Layered
```
Service
    ↓
Repository
    ↓
PostgreSQL
```

The service often directly knows the repository implementation.
## Hexagonal
```
Service
    ↓
Repository Interface (Port)
    ↓
PostgreSQL Adapter
```

The service only knows the interface.
# Advantages
- Easier testing (mock ports).
- Easier swapping technologies.
- Better separation between business logic and infrastructure.
- Core remains framework-independent.
# Disadvantages
- More abstractions.
- More interfaces and classes.
- Can be overkill for simple CRUD applications.
# Questions
- what are those classes in ports? is this some special kind? looks like a protocol