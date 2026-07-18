Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Greedy algorithms** solve problems by repeatedly making the **best local choice at the current moment**, hoping that these choices lead to the globally optimal solution.

The idea:
> "Choose what looks best now, and don't reconsider past decisions."
# Example: Making change
Coins:
```
[1, 5, 10, 25]
```

Amount:
```
41
```

Greedy approach:
```
Take 25
Remaining: 16

Take 10
Remaining: 6

Take 5
Remaining: 1

Take 1
```

Result:
```
25 + 10 + 5 + 1 = 41
```
# Example: Scheduling tasks
Suppose tasks have deadlines and rewards:
```
Task A → high reward, short duration
Task B → low reward, long duration
```

A greedy algorithm might:
> Always choose the highest reward task available.
# Common greedy algorithms

## Dijkstra's algorithm
Find shortest paths:
```
Always choose the node with the smallest known distance.
```

Uses a **priority queue (heap)**.
## Minimum spanning tree
Connect all nodes with minimum total cost:
- **Kruskal's algorithm**
- **Prim's algorithm**
## Huffman coding
Compression algorithm:
```
Repeatedly combine least frequent symbols.
```

Used in data compression.
# Characteristics of greedy algorithms
A greedy algorithm works when:
1. **Greedy choice property**
    - A locally optimal choice can lead to a global optimum.
2. **Optimal substructure**
    - The optimal solution contains optimal solutions to smaller problems.
# Greedy vs Dynamic Programming
Example: choosing investments.

**Greedy:**
```
Pick best investment now.
Never reconsider.
```

Fast, but may fail.

**Dynamic programming:**
```
Explore possible choices.
Store previous results.
Guarantee optimal solution.
```

More expensive.
# Complexity
Greedy algorithms are often efficient:
- Dijkstra: `O((V+E) log V)` with a heap
- Kruskal: `O(E log E)`
# In software engineering
Greedy ideas appear in:
- task scheduling
- network routing
- resource allocation
- compression
- caching strategies
- load balancing

For example, a distributed scheduler might use a greedy rule:
```
"Assign the next job to the worker with the most free capacity."
```

This is fast and often good enough, even if it is not mathematically perfect.

Mental model:
```
Greedy:
make the best immediate choice

Divide & conquer:
split → solve → combine

Dynamic programming:
remember previous solutions
```

The important skill is not memorizing greedy algorithms, but recognizing **when a problem allows a greedy choice without needing to explore all possibilities**.