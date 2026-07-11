Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Split by ranges, for example:
```
Shard 1:
IDs 1 - 1M

Shard 2:
IDs 1M - 2M

Shard 3:
IDs 2M - 3M
```

Advantages
- simple
- efficient range queries, like `SELECT * FROM users WHERE id BETWEEN 1000 AND 2000;`

Problems:
- The last shard might get overloaded (all writes go to it).