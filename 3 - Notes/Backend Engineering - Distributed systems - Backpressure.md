Tags: [[__Backend_Engineering]]
#BackendEngineering 

# Introduction
Backpressure is a mechanism used when we have a producer that sends requests to a consumer to process. It prevents a fast producer (sending a lot of requests) from overwhelming a slower consumer.

How it is implemented depends on whether we use an asynchronous or a direct (synchronous) communication:
- direct (synchronous) communication - when a consumer cannot process data fast enough, then it tells the sender to slow down or stop sending temporarily
- asynchronous communication - prevent the consumer from processing too much at once (and the producer keeps sending )

For example, when producer generates 1000 messages/second and consumer can process only 100 messages/second, then messages pile up in memory, queues grow, and eventually the system may run out of memory or become very slow.
# How to implement it 
## Asynchronous communication (Kafka example)
To implement a backpressure when we use an asynchronous communication (for example in Kafka), what we can do is:
### 1. Limit consumer concurrency
Set up a limit for how many messages can be processed simultaneously by a consumer without setting up a limit for how many messages are fetched by a consumer.

For example, here only 10 messages can be processed concurrently using semaphores ([[Software Engineering - Concurrency - Semaphores|link]]):
```python
semaphore = asyncio.Semaphore(10)

async def process(message):
    async with semaphore:
        await process_message(message)
```
### 2. Limit how many messages the consumer fetches
Kafka consumers have configuration such as `max.poll.records`, which limits how many records are returned by a poll.

For example:
```
max.poll.records = 100
```

This prevents your application from pulling huge batches into memory.
### 3. Control downstream concurrency
When a consumer reads messages and based on them it submits tasks for other workers, we can limit how many concurrent jobs a consumer can submit.

The consumer can continue receiving messages while the concurrency limit is reached, buffering or queueing messages until capacity becomes available:
```
Kafka → Consumer → bounded worker pool → worker
                         ↑
                    backpressure
```
### 4. Slow/pause consumption when overloaded
Your application can temporarily stop fetching/processing messages when its internal queue is full, then resume when capacity becomes available.

Conceptually:
```
if worker_queue_full:
    pause consumption
else:
    consume messages
```

Kafka clients provide mechanisms such as `pause()` / `resume()` for this.
## Direct communication
With direct (synchronous) communication, backpressure is usually implemented through flow control: the consumer tells the producer when it can accept more work.
### Option 1: Blocking
The producer sends a request and waits for a response from a consumer before sending another request.

Because the producer can't submit unlimited work concurrently, the consumer naturally limits the producer.
### Option 2: Explicit rejection / throttling
The consumer maintains a limit, e.g. using semaphores ([[Software Engineering - Concurrency - Semaphores|link]]):
```python
semaphore = Semaphore(10)
```

When consumer can't process more requests, it sends a response to the producer informing about it.

The producer then waits and retries, ideally with backoff:
```
request
   ↓
429
   ↓
wait 100 ms
   ↓
retry
   ↓
429
   ↓
wait 200 ms
   ↓
retry
```
### Option 3: Explicit flow-control protocol
For streaming systems, the consumer can explicitly advertise capacity:
```
Consumer → Producer:
    "I can accept 10 more messages"

Producer sends 10

Consumer → Producer:
    "I can accept 5 more"

Producer sends 5
```

This is often called credit-based flow control.