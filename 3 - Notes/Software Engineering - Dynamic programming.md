Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Dynamic programming (DP)** is an algorithmic technique for solving problems by **breaking them into smaller overlapping subproblems and storing their solutions so they are not computed again**.

The main idea:
> Solve smaller problems once, remember the results, and reuse them.
# Example: Fibonacci numbers
Naive recursion:
```
F(5)
├── F(4)
│   ├── F(3)
│   └── F(2)
└── F(3)
```

`F(3)` is calculated multiple times.

Complexity:
```
O(2ⁿ)
```

With dynamic programming:
```
F(0) = 0
F(1) = 1
F(2) = F(1)+F(0)
F(3) = F(2)+F(1)
...
```

Store results:
```
F(0), F(1), F(2), F(3), ...
```

Complexity:
```
O(n)
```
# Two common approaches
## 1. Memoization (top-down)
Start with recursion and cache results:
```
def fib(n):
    if n <= 1:
        return n

    if n not in cache:
        cache[n] = fib(n-1) + fib(n-2)

    return cache[n]
```

Flow:
```
Solve big problem
        ↓
Need smaller problem
        ↓
Check if already solved
        ↓
Reuse result
```
## 2. Tabulation (bottom-up)
Build solutions from smaller cases:
```
F(0)
 ↓
F(1)
 ↓
F(2)
 ↓
F(3)
 ↓
F(4)
```

Usually uses iterative loops.
# When is DP useful?
A problem usually has two properties:
## 1. Overlapping subproblems
The same smaller problems appear repeatedly.

Example:
```
Solve A:
  need B and C

Solve D:
  need B and E
```

Both need `B`.
## 2. Optimal substructure
The optimal solution can be built from optimal solutions of smaller problems.

Example:

Shortest path:
```
Best route A → C
depends on:
Best route A → B
+
Best route B → C
```
# Common DP problems

## Knapsack
Question:
> What is the maximum value I can carry with limited capacity?

Used for:
- resource allocation
- optimization problems
## Longest Common Subsequence (LCS)
Find similarity between sequences:

```
String A: ABCD
String B: ACBD

Answer: ABD
```

Used in:
- diff tools
- DNA analysis
## Shortest paths
Examples:
- Bellman-Ford
- Floyd-Warshall
## Coin change
Question:
> Minimum number of coins needed to make amount X?
# DP vs other patterns

| Technique           | Idea                        |
| ------------------- | --------------------------- |
| Divide & conquer    | Split independent problems  |
| Greedy              | Make best immediate choice  |
| Dynamic programming | Reuse overlapping solutions |

Example:

**Finding shortest route**
- Greedy → choose closest next step
- DP → remember previous shortest solutions
- Divide & conquer → split problem into parts
# In software engineering
Dynamic programming appears in:
- optimization algorithms
- scheduling
- resource allocation
- bioinformatics
- AI planning
- compilers

For backend/data engineering, DP is less common in daily application code than data structures, but the ideas appear in:
- query optimization
- caching
- planning algorithms
- distributed optimization

A good mental model:
```
Recursion:
"I solve smaller problems repeatedly."

Dynamic programming:
"I solve smaller problems once and remember them."

Greedy:
"I make the best decision now and move on."
```