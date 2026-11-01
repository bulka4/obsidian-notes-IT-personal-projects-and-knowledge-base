Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Tracing is a monitoring technique used to understand what happens to a single request as it travels through:
- Multiple services in a distributed system (that's a distributed tracing)
- Different functions within a single application (that's a monolithic tracing)

We say:
- perform / implement tracing
- collect traces / tracing data
# Monolithic vs distributed tracing
## Monolithic
In a monolithic application, one request usually goes through one process:
```
User → Application → Database
```

Tracing will show us how much time different functions within a single application took:
```
Request
 ├─ authenticateUser()     10 ms
 ├─ calculatePrice()       50 ms
 ├─ queryDatabase()       200 ms  ← bottleneck
 └─ generateResponse()     20 ms
```
## Distributed
In a microservices system, the same request may travel through many services and tracing will show us how much time each service took to process the request:
```
User
 |
API Gateway        <- 10ms
 |
Auth Service       <- 20ms
 |
Order Service      <- 50ms
 |
Payment Service    <- 1000ms
 |
Inventory Service  <- 30ms
 |
Database           <- 10ms
```
# Why it is needed
Thanks to tracing we know why the system is slow, which components exactly are slow.
# Trace
A trace represents the entire lifecycle of one request.

Example:
```
Trace ID: abc123

User request: "Buy product"

API Gateway       20 ms
   |
Order Service     50 ms
   |
Payment Service  800 ms   <-- bottleneck
   |
Inventory         30 ms
```

The trace tells us:
- which services were called
- in what order
- how long each step took
- where failures happened
# Span
A span represents one operation inside a trace.

Example:
```
Span 1: API Gateway        20 ms
Span 2: Order Service      50 ms
Span 3: Payment Service   800 ms
Span 4: Database query     40 ms
```

A trace is made of many spans.

A span contains information like:
- service name
- operation name
- start time
- end time
- duration
- errors
- metadata (tags)
# How tracing works
When we have multiple services making calls to each other:
```
API Gateway -> Order Service -> Payment Service
```

then each service creates a span object:
```json
{
	"trace_id":       "abc123"
	"span_id":        "S2"
	"parent_span_id": "S1"
	"name":           "service 2"
	
	"start_time":     20:00:01.100
	"end_time":       20:00:01.350
	
	"attributes":
	    "attr_1" = 3
}
```

and sends it:
- to a common database
- and to another service to which it makes a call

The span object has fields:
- `trace_id` - indicating that this is the same trace
- `span_id` - each span has a unique ID
- `parent_span_id` - when one service passes a span to another service, the received `span_id` is interpreted as the `parent_span_id`. It is used to build a tree showing how requests were travelling between services.
- `start / end time` - indicating how long the operation for one service took
- additional metadata created by us

So the workflow looks like this:
```
						            trace_id = T1
						                 │
		|--------------------------------|---------------|
		│                                │               │
        ▼                                ▼               ▼
	 Service A  ----------------->   Service B   ->  Service C
		|		each service passes      |               |
		|			  its span           |               |
		|		to another service       |               |
        │                                │               │
     creates                          creates         creates
      spans                            spans           spans
        |                                |               |
        |--------------------------------|---------------|
		                                 │
		                                 ▼
		                              backend
		                                 │
		                                 ▼
		                            reconstructs
		                              trace T1
```

So each service sends a span to a common database and this way we create records like this representing one trace and indicating how requests were travelling between services:
```
S_A: trace=T1, span=S_A, parent=none
S_B: trace=T1, span=S_B, parent=S_A
S_C: trace=T1, span=S_C, parent=S_B
```
## How to collect and forward span data
To send span data to a common database and forward it with a request to another service, we can use for example the `OpenTelemetry` Python library.

It can automatically include trace data in a request and read it when receiving a request.

Sending a request with the trace data included:
```python
import httpx

from opentelemetry import trace
from opentelemetry.instrumentation.httpx import HTTPXClientInstrumentor

HTTPXClientInstrumentor().instrument()

tracer = trace.get_tracer(__name__)

async def call_service():
    with tracer.start_as_current_span("service_A") as span:
        span.set_attribute("attr_A", 3)

        async with httpx.AsyncClient() as client:
            response = await client.get(
                "http://service-B/search",
                params={"attr_A": 3},
            )

        return response.json()
```

Receiving a request and reading the included trace data:
```python
from fastapi import FastAPI
from opentelemetry import trace
from opentelemetry.instrumentation.fastapi import FastAPIInstrumentor

app = FastAPI()

# Get a tracer
tracer = trace.get_tracer(__name__)

# Instrument FastAPI
FastAPIInstrumentor.instrument_app(app)


@app.get("/search")
async def search():
    # OpenTelemetry has already:
    #
    # 1. Read the `traceparent` HTTP header
    # 2. Extracted the incoming trace context
    # 3. Created a new server span
    # 4. Set the incoming span as its parent
    #
    # So this endpoint executes inside the new span.

    current_span = trace.get_current_span()

    context = current_span.get_span_context()

    print("Trace ID:", format(context.trace_id, "032x"))
    print("Span ID:", format(context.span_id, "016x"))

    return {"result": "some documents"}
```
## Tracing data for different functions (not just making HTTP requests)
We can also gather tracing data for any function, not just those making HTTP requests.

For example, when we read data from the Milvus vector database:
```python
from opentelemetry import trace

tracer = trace.get_tracer(__name__)

client = MilvusClient(
	uri=f"http://{host}:19530"
)

def search(embedding, top_k):
    with tracer.start_as_current_span("milvus.search") as span:
        span.set_attribute("top_k", top_k)

        results = client.search(
            collection_name=self.collection,
            data=[embedding],
            limit=top_k,
        )

        return results
```
# Questions
- 