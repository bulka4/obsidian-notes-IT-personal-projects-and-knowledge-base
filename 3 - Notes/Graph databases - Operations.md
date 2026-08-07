Tags: [[_Databases]] [[_Graph_databases]]
#Databases #GraphDatabases 

# Typical operations
Some basic operations, typical for a graph database include:
# Fixed-depth traversal
Find all the nodes within a specific number of hops ([[Graph databases - Hops|link]]) connected by a specific types of edges (edges representing a specific relation).
## Recursive traversal
Like a fixed-depth traversal but for any number of hops (find all nodes in all hops).
## Path finding
Find a path between two nodes. For example: `Customers → Orders → Sales → Dashboard`
# Shortest path
If multiple paths exist:
```
A → B → D
 \      ↑
  → C ──┘
```

find the shortest one: `A → B → D`.
# Reachability
Can one node reach another?
