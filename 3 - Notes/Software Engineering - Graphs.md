Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
A **graph** is a data structure that represents **relationships between objects**. It consists of:
- **Nodes (vertices)** → entities
- **Edges** → connections between entities

Example:
```
      A
     / \
    B   C
    |   |
    D---E
```

Here:
- Nodes: `A, B, C, D, E`
- Edges: connections between them
# Types of graphs
## 1. Directed vs undirected
**Undirected graph**
- Relationship works both ways.

Example:
```
Friendship:

Alice ─ Bob
```

**Directed graph**
- Relationship has direction.

Example:
```
Twitter follow:

Alice → Bob
```
## 2. Weighted graphs
Edges have values:
```
A ----5---- B
```

Examples:
- distance between cities
- network latency
- cost
## 3. Cyclic vs acyclic
**Cyclic:**
```
A → B → C → A
```

**Acyclic:**
```
A → B → C
```

A common example is a **DAG (Directed Acyclic Graph)**.

Used in:
- workflow systems
- Airflow pipelines
- build systems

Example:
```
Extract
  ↓
Transform
  ↓
Train model
  ↓
Deploy
```
# Common graph algorithms
## Breadth-First Search (BFS)
Explore level by level:
```
A
|
B
|
C
```

Useful for:
- shortest path in unweighted graphs
- finding nearby connections

Complexity:
```
O(V + E)
```

where:
- `V` = number of nodes
- `E` = number of edges
## Depth-First Search (DFS)
Explore deeply before backtracking:
```
A → B → C
    ↑
    backtrack
```

Useful for:
- detecting cycles
- topological sorting
- traversing structures

Complexity:
```
O(V + E)
```
## Shortest path algorithms
Examples:
- **Dijkstra's algorithm**
    - shortest path with non-negative weights
- **Bellman-Ford**
    - handles negative weights
- **A***
    - used in pathfinding
# Graph vs Tree
A tree is actually a special type of graph.

| |Tree|Graph|
|---|---|---|
|Cycles|❌ No|✅ Possible|
|Root|Usually yes|Not required|
|Parent-child structure|Yes|Not necessarily|
|Connections|Limited|Arbitrary|

Example:
```
Tree:

      A
     / \
    B   C


Graph:

A ─ B
|   |
C ─ D
```
# Graphs in software engineering
Graphs are everywhere:
## Distributed systems
Network topology:
```
Server A ─ Server B ─ Server C
```
## Databases
Graph databases:
```
(Person) ─friend→ (Person)
```

Examples:
- social networks
- recommendation systems
## Build systems
Dependencies:
```
Library A
    ↓
Library B
    ↓
Application
```
## ML / AI
- knowledge graphs
- neural network computation graphs
- graph neural networks (GNNs)
## Data engineering
Airflow DAGs are graphs:
```
Load data
    ↓
Clean data
    ↓
Train model
    ↓
Evaluate
```
# A simple mental model

```
Array      → ordered collection
Hash table → lookup by key
Tree       → hierarchy
Graph      → relationships
```

For backend/distributed systems, graphs are especially important for dependencies, networks, workflows, and data relationships.