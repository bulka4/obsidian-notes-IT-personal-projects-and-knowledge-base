Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Sliding window** is an algorithmic technique where you maintain a **contiguous range (window) of elements** and move it through a data structure (usually an array or string) to avoid repeated calculations.

It is often used to reduce `O(n²)` solutions to `O(n)`.
# Example: maximum sum of `k` consecutive elements
Array:
```
[2, 5, 1, 8, 3, 4]
```

Find the maximum sum of 3 elements.

Naive approach:
```
[2,5,1] → sum
[5,1,8] → sum
[1,8,3] → sum
...
```

Repeatedly recalculates sums → `O(n*k)`.

Sliding window:
```
Window:
[2, 5, 1]  = 8
    ↓ move
[5, 1, 8]  = 14
    ↓ move
[1, 8, 3]  = 12
```

Instead of recalculating:
```
new sum = old sum - removed element + added element
```

Complexity:
```
O(n)
```
# Types of sliding windows

## 1. Fixed-size window
Window size stays constant:
```
[ A B C ] D E F
  ↓
A [ B C D ] E F
```

Examples:
- maximum sum of `k` elements
- moving averages
## 2. Variable-size window
Window expands and shrinks depending on a condition:

Example:
> Find the longest substring without repeating characters.

String:
```
abcabcbb
```

Window:
```
[a b c] a b c b b
```

When a duplicate appears:
- move left pointer
- shrink the window
# Relation to two pointers
Sliding window is usually a **special case of two pointers**:
```
Two pointers:
left, right indices

Sliding window:
left, right define a moving range
```

Example:
```
left → [ elements inside window ] ← right
```
# Common uses
- string processing
    - longest substring problems
    - pattern matching
- data streams
    - last N seconds of events
    - rolling metrics

Example:
```
Kafka stream:

10:00:00 - 10:01:00
        ↓
count requests in this window
```

- monitoring systems
    - requests per minute
    - moving averages

Mental model:
```
Brute force:
try every possible range → O(n²)

Sliding window:
move one range through data → O(n)
```

For backend/data engineering, sliding windows are especially important for stream processing, monitoring, analytics, and systems like Kafka Streams/Flink/Spark Streaming.