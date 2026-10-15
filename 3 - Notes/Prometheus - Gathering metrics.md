Tags: [[_Monitoring_applications_and_infrastructure]] [[_Prometheus]] [[__Infrastructure_Engineering]]
#MonitoringAppsInfra #Prometheus #InfrastructureEngineering 

# Introduction
This document contains examples of how we can use Prometheus to collect metrics in Python.
# How an app exposes metrics
Using Prometheus libraries, we can make our app exposing metrics through HTTP which Prometheus can then load using the `GET /metrics` route.
## Our Python code creates a metric object
For example:
```python
from prometheus_client import Histogram

embedding_ingestion_duration = Histogram(
    "embedding_ingestion_duration_seconds",
    "Time spent ingesting embeddings",
)
```

This creates a Python object in your application's memory. It contains data that will be exposed through a HTTP endpoint.

When we do:
```python
with embedding_ingestion_duration.time():
    ingest_embeddings()
```

the Prometheus Python client updates that object's internal state.

For example, internally it might now know approximately:
```
count = 5
sum = 1.15

bucket <= 0.1  → 2
bucket <= 0.25 → 4
bucket <= 0.5  → 4
bucket <= 1.0  → 5
```

At this point, Prometheus has not received anything yet.
## Our application exposes `/metrics` route
We need to expose the Prometheus metrics through HTTP.

For a simple Python application, you might use:
```Python
from prometheus_client import start_http_server

start_http_server(8000)
```

This starts an HTTP server on port `8000`.

So in our app we start the HTTP server and collect metrics:
```python
import time
import random

from prometheus_client import Histogram, start_http_server

# --------------------------------------------------
# Metrics
# --------------------------------------------------
embedding_ingestion_duration = Histogram(
    "embedding_ingestion_duration_seconds",
    "Time spent ingesting embeddings",
)

# --------------------------------------------------
# Application logic
# --------------------------------------------------
def ingest_embeddings():
    # Simulate embedding generation + saving
    duration = random.uniform(0.05, 1.5)
    time.sleep(duration)


def process_document():
	with embedding_ingestion_duration.time():
		ingest_embeddings()

# --------------------------------------------------
# Start metrics HTTP server
# --------------------------------------------------
if __name__ == "__main__":

    # Starts HTTP server exposing /metrics
    start_http_server(8000)

    print("Application running")
    print("Metrics available at http://localhost:8000/metrics")

    while True:
        process_document()
        time.sleep(2)
```

Your application now has:
```
http://your-app:8000/metrics
```

The Prometheus client library handles this endpoint.

If Prometheus sends:
```
GET /metrics
```

your application responds with something roughly like:
```
# HELP embedding_ingestion_duration_seconds Time spent ingesting embeddings
# TYPE embedding_ingestion_duration_seconds histogram

embedding_ingestion_duration_seconds_bucket{le="0.1"} 2
embedding_ingestion_duration_seconds_bucket{le="0.25"} 4
embedding_ingestion_duration_seconds_bucket{le="0.5"} 4
embedding_ingestion_duration_seconds_bucket{le="1.0"} 5

embedding_ingestion_duration_seconds_count 5
embedding_ingestion_duration_seconds_sum 1.15
```

This is just text sent over HTTP.

This HTTP server sends data from memory, from the app's Python object `embedding_ingestion_duration`.
## Prometheus periodically asks for it
Prometheus is configured with a **scrape target**.

For example:
```yaml
scrape_configs:
  - job_name: "embedding-service"
    static_configs:
      - targets: ["embedding-service:8000"]
```

Prometheus might be configured to scrape every 15 seconds.

So every 15 seconds it effectively does:
```
GET http://embedding-service:8000/metrics
```

Your application responds with the current metrics.

Prometheus then stores those values.
# Process success/failure rate
Calculate how many times a process succeeded / failed:
```python
from prometheus_client import Counter

process = Counter(
    "process_total",
    "Embedding ingestion attempts",
    ["status"],
)

try:
    run_a_process(...)
    process.labels(status="success").inc()
except Exception:
    process.labels(status="failure").inc()
    raise
```

This creates a metric called `embedding_ingestion_total` which contains two counters:
```
embedding_ingestion_total{status="success"}  count_1
embedding_ingestion_total{status="failure"}  count_2
```
# Embedding ingestion duration
Calculate how much time running a process was taking:
```python
from prometheus_client import Histogram

process_duration = Histogram(
    "process_duration_seconds",
    "Time spent on a process",
)

with process_duration.time():
    run_a_process(...)
```

This will expose several series such as:
```
embedding_ingestion_duration_seconds_bucket{le="0.1"} ...
embedding_ingestion_duration_seconds_bucket{le="0.5"} ...
embedding_ingestion_duration_seconds_bucket{le="1"} ...
embedding_ingestion_duration_seconds_bucket{le="5"} ...
embedding_ingestion_duration_seconds_count ...
embedding_ingestion_duration_seconds_sum ...
```

which mean:
- `embedding_ingestion_duration_seconds_bucket{le="x"}` - number of process runs that took `x` seconds or less
- `embedding_ingestion_duration_seconds_count` - number of process runs
- `embedding_ingestion_duration_seconds_sum` - total time taken by all runs
