Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
An API contract is the agreed specification of how one software component can communicate with another. It describes how the input and output looks like (it is defined by the API itself, not by a program that uses this API).
# What an API contract can define
**1. Endpoint**
```
POST /ask
GET /search
```

**2. Inputs**
- path parameters
- query parameters
- headers
- request body

**3. Data types and structure**
```
{
  "query": "string",
  "top_k": "integer"
}
```

**4. Required vs optional fields**
```
query → required
top_k → optional, default = 3
```

**5. Outputs**
```
200 → AskResponse
400 → invalid request
500 → server error
```

**6. Semantics**  
For example:
> `top_k` specifies the maximum number of documents returned.

This is important because a contract isn't merely a schema. It also describes what the fields and operations mean.
# Defining request and response schemas using data classes
We can use data classes to define what fields are expected in the request for a REST API route and what fields are in the response:
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
# OpenAPI specification
FastAPI can expose an OpenAPI specification describing our HTTP API, things like available endpoints, HTTP methods, request parameters, request body, etc.. 

It is in the JSON format, generated automatically by FastAPI and available through the `/openapi.json` endpoint, so clients can send a request to this endpoint and receive the JSON specification.

We can then generate:
- client libraries
- API documentation
- validation
- tests

This is particularly useful when another service/team consumes our API.
## Generating clients for making request
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
## Testing using contracts
We can use the `/openapi.json` specification to test whether the API is compatible with what the client, which will be using this API, expects.

For the client, we can prepare a OpenAPI YAML document which is a contract representing what API the client expects.

Then, we can generate the `/openapi.json` specification for an API and compare it with the contract to check whether it is compatible.
# Web pages with a visual API documentation
FastAPI also automatically generates API documentation available at Swagger UI (the `/docs` endpoint) and ReDoc (the `/redoc` endpoint).