Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A **queue** is a data structure that stores elements in a **First-In, First-Out (FIFO)** order.

The first element added is the first one removed.

Example:
```
id="d8p4q1"
Queue:

Front → [A] [B] [C] ← Back

remove() → A
add(D)   → [B] [C] [D]
```

Like a real-world queue: the first person in line is served first.
# Main operations

|Operation|Meaning|Complexity|
|---|---|---|
|`enqueue`|Add element to the back|O(1)|
|`dequeue`|Remove element from the front|O(1)|
|`peek`|Look at first element|O(1)|

Example:
```
id="2ydv5t"
queue.append(task)  # enqueue
task = queue.pop(0) # dequeue
```

(Real implementations use more efficient structures than a normal list.)
# Common queue types

## 1. Simple queue (FIFO)
```
A → B → C
```

Used when tasks should be processed in order.

Example:
- print jobs
- background tasks
## 2. Priority queue
Elements have priorities:
```
High priority:
    Task A

Low priority:
    Task B
```

The highest priority item is removed first.

Used in:
- operating system scheduling
- Dijkstra's algorithm
- job scheduling

Usually implemented using a **heap**.
## 3. Message queue
A queue used for communication between services:
```
Producer
   |
   ↓
Message Queue
   |
   ↓
Consumer
```

Example:
```
Order Service
      |
      ↓
   Kafka / RabbitMQ
      |
      ↓
Payment Service
```

Benefits:
- decoupling services
- asynchronous processing
- handling traffic spikes
# Queue vs Stack

| |Queue|Stack|
|---|---|---|
|Order|FIFO|LIFO|
|Add|End|Top|
|Remove|Front|Top|
|Example|Line at a store|Stack of plates|
# Queues in backend engineering
Queues are fundamental in distributed systems:
## Event-driven architecture
```
User request
     ↓
Message queue
     ↓
Worker processes task
```

Example:
- upload image
- generate thumbnail later
## Kafka
Kafka is essentially a **distributed, persistent message queue/log**:
```
Producer → Kafka topic → Consumer
```
## Operating systems
The OS uses queues for:
- process scheduling
- network packets
- I/O requests

Example:
```
CPU queue:
Process A
Process B
Process C
```
## Relation to other data structures
```
Array       → ordered storage
Hash table  → fast lookup by key
Tree        → hierarchy/order
Graph       → relationships
Queue       → ordered processing of tasks
Stack       → last-in-first-out processing
```

Queues are especially important because they are the foundation of asynchronous processing, Kafka, event-driven architectures, and scalable services.