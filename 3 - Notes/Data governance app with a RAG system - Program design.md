Tags: [[__My_projects]]
#MyProjects 

# Contracts
## API contracts
### Defining request and response schemas using data classes
We use data classes to define what fields are expected in the request for a REST API route and what fields are in the response:
```python
# A result of searching through a vector store
@dataclass
class SearchResult:
    # ID of the document (taken from the database documentation database)
    object_id: int
    # One text chunk from the document          
    text_chunk: str
    # Similarity score for this text chunk and the given query
    similarity_score: float

@dataclass
class AskRequest:
    query: str
    top_k: int = 3

@dataclass
class AskResponse:
    answer: str
    retrieved_docs: list[SearchResult]

@app.post("/ask", response_model=AskResponse)
    async def ask(self, request: AskRequest) -> AskResponse:
	    ...
```
### OpenAPI specification
FastAPI can expose an OpenAPI specification describing our HTTP API, things like available endpoints, HTTP methods, request parameters, request body, etc.. 

It is in the JSON format, generated automatically by FastAPI and available through the `/openapi.json` endpoint, so clients can send a request to this endpoint and receive the JSON specification.

You can then generate:
- client libraries
- API documentation
- validation
- tests

This is particularly useful when another service/team consumes your API.
### Web pages with a visual API documentation
FastAPI also automatically generates API documentation available at Swagger UI (the `/docs` endpoint) and ReDoc (the `/redoc` endpoint).
### Generating clients for making request
We can use the `/openapi.json` endpoint and a client generator tool, e.g. OpenAPI Generator:
```shell
openapi-generator-cli generate \
  -i openapi.json \
  -g python \
  -o generated/rag_client
```
to generate a dictionary with Python classes that can be used for using the API.

Instead of manually doing:
```python
import requests

response = requests.post(
    "http://rag-api:8000/ask",
    json={"question": "What is a data warehouse?"}
)
```

we can use the generated API client. Conceptually it becomes something like:
```python
from rag_client import ApiClient
from rag_client.api.default_api import DefaultApi
from rag_client.models.ask_request import AskRequest

with ApiClient() as client:
    api = DefaultApi(client)

    request = AskRequest(
        question="What is a data warehouse?"
    )

    response = api.ask(request)
```

The generated code handles things such as:
- constructing the URL
- HTTP method
- serialization
- deserialization
- request/response models
- validation
- etc.
### Testing using contracts
We can use the `/openapi.json` specification to test whether the API is compatible with what the client, which will be using this API, expects.

For the client, we can prepare a OpenAPI YAML document which is a contract representing what API the client expects.

Then, we can generate the `/openapi.json` specification for an API and compare it with the contract to check whether it is compatible.
## Kafka message contracts
For Kafka messages we could define a schema using a JSON file, for example:
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "DocumentationUpdated.v1",
  "type": "object",
  "required": [
    "event_type",
    "document_id",
    "version",
    "updated_at"
  ],
  "properties": {
    "event_type": {
      "type": "string",
      "const": "DocumentationUpdated"
    },
    "document_id": {
      "type": "integer"
    },
    "version": {
      "type": "integer",
      "minimum": 1
    },
    "updated_at": {
      "type": "string",
      "format": "date-time"
    }
  },
  "additionalProperties": false
}
```

this specifies what fields must exists in every `DocumentationUpdated.v1` event.

The producer can validate messages against the schema when emitting an event and also the consumer can validate it when processing an event.
### Versioning
We could create different versions of message schemas. When we want to change a message schema, for example change `document_id: integer` into `document_id: string`, we can keep both schemas as different versions, to keep track of changes.

If we have different schemas for different messages, with different offsets:
```
offset 100 → DocumentationUpdated v1
offset 101 → DocumentationUpdated v2
offset 102 → DocumentationUpdated v2
```
then having saved different schema versions allows us to verify schema of all those messages.
### Schema registry
We could use a schema registry to manage schema files. The registry stores schemas and can enforce compatibility rules.
### Testing a producer and consumer
When we have a contract defined, we can test a producer and consumer independently.

We can:
- check whether the event emitted by the producer satisfies the contract, without a consumer processing it
- check whether the consumer can process a message that satisfies the contract, without emitting that message by the producer
# Questions
- What is the application / core layer which you mentioned?
- what do you mean by application abstraction? why the AskRequest object shouldnt be there?
- what to improve?