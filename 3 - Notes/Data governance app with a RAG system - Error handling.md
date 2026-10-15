Tags: [[__My_projects]]
#MyProjects 

# Introduction
Ideas for error handling, not implemented yet.
# Embeddings data inconsistency
We might encounter data inconsistency when a table description gets updated and the embedding ingestion pipeline fails. Then, embeddings used for semantic search are not up to date so semantic search uses old documentation.

To deal with this, we could save information about document and embedding versions. Each time a document gets updated we increase its version number. When a version number for embeddings is smaller than for a corresponding document, that means that embeddings are not up to date.

So in the database documentation database ([[Data governance app with a RAG system - Databases - Database documentation|link]]) we would save information:
```
{
	tableID: ...
	version: ...
	description: ...
}
```

and in the vector store ([[Data governance app with a RAG system - Databases - Vector database for semantic search|link]]) we would save similarly:
```
{
	vector: ...
	object_id: ... # Corresponding to the tableID
	version: ...
}
```

When embeddings are not up to date, we could for example show in the Data Governance UI ([[Data governance app with a RAG system - Data governance backend|link]]) a warning that the new documentation has not been processed yet when using the semantic search engine and it will use the old documentation.

Another problem is when embeddings for some chunks for a document has been updated but not for all the chunks. This is covered in the embedding ingestion pipeline document > Error handling section > Atomicity ([[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service#Error handling|link]]).
# Metrics
We can calculate and store metrics using Prometheus like shown in sections below. More information about how this works is here - [[Prometheus - Gathering metrics]].
## Embedding ingestion success/failure rate
```python
from prometheus_client import Counter

embedding_ingestion = Counter(
    "embedding_ingestion_total",
    "Embedding ingestion attempts",
    ["status"],
)

try:
    create_embeddings(...)
    embedding_ingestion.labels(status="success").inc()
except Exception:
    embedding_ingestion.labels(status="failure").inc()
    raise
```

This creates a metric called `embedding_ingestion_total` which contains two counters:
```
embedding_ingestion_total{status="success"}  count_1
embedding_ingestion_total{status="failure"}  count_2
```
## Embedding ingestion duration
```python
from prometheus_client import Histogram

embedding_ingestion_duration = Histogram(
    "embedding_ingestion_duration_seconds",
    "Time spent ingesting embeddings",
)

with embedding_ingestion_duration.time():
    create_embeddings(document)
    save_embeddings(document)
```
## Others
Other metrics we can calculate and store with Prometheus:
- number of documents waiting for embeddings
- number of stale documents
- embedding generation latency
- semantic-search latency
# Logs
## What logs to collect
Logs that we could collect:
- When embedding ingestion starts, completes and fails
- API requests - what requests are made and with which parameters
- External-service failures - for example when Milvus search or using MCP tool fails
- Kafka events - event sent, received, processed, failures
## How to gather and store logs
We could use for that the `logging` module:
```python
import logging

logger = logging.getLogger(__name__)

logger.info("Embedding ingestion started")

try:
    ingest_embeddings()

except Exception:
    logger.exception("Embedding ingestion failed")
    raise
```

Logs could be saved like that:
- The `logging` module sends them to `stdout / stderr`
- container runtime collects logs from `stdout / stderr` and saves them in container logs (e.g. JSON files)
- Fluent Bit collects container logs and it can enrich them
- Fluent Bit sends enriched logs over HTTP to Loki which stores them
- Grafana can query Loki to read logs from it for dashboards
## Tracing
We could use the `OpenTelemetry` library to collect tracing data ([[Backend Engineering - Monitoring - Tracing|link]]). This data would include:
- How much time each service (RAG API, Semantic search API, MCP tool, Milvus search, etc.) took to perform all its operations
- What parameters were used in requests
- Errors

We can send a request with the trace data included like this:
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

and read the trace data included in the received request like this:
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

Gathering tracing data for execution of different functions (e.g. reading data from Milvus):
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
# Embedding ingestion pipeline
Error handling in the embedding ingestion pipeline - [[Data governance app with a RAG system - Embedding Ingestion Pipeline and Service#Error handling]].