Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A **heap** is a specialized tree-based data structure designed for **quick access to the smallest or largest element**.

It is usually implemented as a **complete binary tree** stored in an array.
# Types of heaps
## Min-heap
The smallest element is always at the root:
```
        1
       / \
      3   5
     / \
    7   9
```

Property:
```
Parent ≤ children
```
## Max-heap
The largest element is always at the root:
```
        9
       / \
      5   7
     / \
    1   3
```

Property:
```
Parent ≥ children
```
# Main operations

|Operation|Complexity|
|---|---|
|Get min/max|O(1)|
|Insert|O(log n)|
|Remove min/max|O(log n)|
|Build heap|O(n)|

When inserting:
1. Add element at the end.
2. Move it upward ("bubble up") until the heap property is restored.

When removing:
1. Remove root.
2. Move last element to root.
3. Move it downward ("heapify").
# Heap vs sorted tree
A heap only guarantees:
```
Parent is smaller/larger than children
```

It does **not** keep all elements sorted.

Example min-heap:
```
        1
       / \
      10  5
     /
    20
```

You know `1` is smallest, but you do not know whether `5` or `10` comes next.

A balanced search tree gives ordered traversal, while a heap gives fast min/max access.
# Priority queues
The most common use of heaps is implementing **priority queues**.

Example:
```
Tasks:

(High priority)    Fix production bug
(Medium priority)  Train model
(Low priority)     Generate report
```

A heap allows:
```
remove highest priority task → O(log n)
```
# Algorithms using heaps

## Dijkstra's shortest path
Find the next closest node efficiently:
```
Pick smallest distance node
        ↓
Update neighbors
        ↓
Repeat
```

The heap provides:
```
get smallest distance → O(log n)
```
## Heap sort
Sorting algorithm:
1. Build a heap.
2. Repeatedly remove the smallest/largest element.

Complexity:
```
O(n log n)
```
# Heaps in software engineering
Common uses:
- **Operating systems**
    - scheduling tasks by priority
- **Databases**
    - query execution strategies
- **Distributed systems**
    - priority task queues
- **Networking**
    - scheduling packets
- **Applications**
    - job schedulers
    - timers

Example:
```
Event loop timer queue:

10:00:01 → send heartbeat
10:00:05 → retry request
10:00:10 → clean cache
```

A heap efficiently finds the next event to execute.
# A simple mental model

```
Hash table → find by key quickly
Tree       → maintain order/hierarchy
Queue      → process in arrival order
Heap       → process by priority
Graph      → represent relationships
```

For backend engineering, **heaps are especially important because priority queues appear in schedulers, distributed systems, networking, and database engines.**