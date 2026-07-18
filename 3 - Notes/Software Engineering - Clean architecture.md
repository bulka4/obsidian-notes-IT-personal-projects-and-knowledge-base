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

Dependencies always point inward.
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
- [[Software Engineering - Architecture concepts - Interface adapters]]
- [[Software Engineering - Architecture concepts - Use case]]
- [[Software Engineering - Architecture concepts - Entity]]
## Frameworks & Drivers
Technical details:
```
FastAPI
PostgreSQL
Kafka
OpenAI SDK
```
# Dependency rule
The core should not know about what frameworks we use, so we should avoid doing something like:
```python
import fastapi
import sqlalchemy
import openai
```

Instead, the outer layers depend on the inner layers.
# Relationship to Hexagonal Architecture
They are very similar:
- Hexagonal Architecture focuses on ports and adapters.
- Clean Architecture formalizes the layers more explicitly (`Entities`, `Use Cases`, `Interface Adapters`, `Frameworks`).

In practice, many projects use a combination of both.

For your RAG project, a Clean Architecture structure could look like:
```
domain/
    Table
    Documentation

application/
    CreateTableUseCase
    AnswerQuestionUseCase

adapters/
    PostgresRepository
    OpenAiClient
    KafkaPublisher

framework/
    FastAPI
```

The main benefit is that your core business logic can remain unchanged even if you replace:
```
PostgreSQL → MongoDB
OpenAI → Ollama
FastAPI → gRPC
Kafka → RabbitMQ
```

because only the outer layers need to change.