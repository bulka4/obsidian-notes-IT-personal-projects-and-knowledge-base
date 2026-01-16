Tags: [[__Machine_Learning_Engineering]]
#MLEngineering 

# Introduction
A single Ray Serve deployment replica ([[Ray Serve - Replica|link]]) can handle many requests concurrently. This is controlled by:
- `max_ongoing_requests` parameter
- Whether the handler is `async`
- Internal batching configuration

Incoming requests are queued per replica. The replica processes:
- Requests sequentially (sync code), or
- Requests concurrently (async code / concurrency groups)

If there are many requests in a queue, they can be batched and processed together (passed together to an ML model).

Batching can help with GPU utilization and speed up model inference.
