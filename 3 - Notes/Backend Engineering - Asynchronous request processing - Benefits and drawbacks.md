Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Benefits and drawbacks of asynchronous request processing ([[Backend Engineering - Asynchronous request processing|link]]).
# Benefits
## Better user experience (fast response)
- User does NOT wait for heavy work
- Immediate acknowledgment (`200 OK` or `202 Accepted`)

Example:  
Uploading a video doesn’t block the UI.
## Better handling long-running tasks
System can continue receiving new requests while the previous requests haven't been processed yet.
## Decouples request from execution time
- API Gateway stays fast
- heavy work happens separately
- Both services can be scaled separately
## Better scalability for spikes
We can:
- queue work
- process it at controlled rate

Prevents system overload (we don't have to process all the requests at once).
## Fault isolation (to some extent)
If background processing fails:
- request is already accepted
- retry can happen later
# Drawbacks
## More system complexity
We need:
- job queue
- worker system
- retry logic
- monitoring
- failure handling
## Harder debugging
Failures are not visible immediately:
- request succeeded
- background job failed later
## State management required
You must track:
- job status (pending / running / done / failed)

This adds storage and logic overhead.
## Risk of backlog
If workers are slower than incoming requests:
- queue grows
- latency increases
- system can lag heavily
# Questions
- What do you mean by Handles long-running tasks? Is this not the same as better user experience?