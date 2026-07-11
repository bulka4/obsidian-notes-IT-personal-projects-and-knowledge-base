Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
We use a hash function that converts an input into a number with a fixed number of digits and we take the rest of dividing the output of the hash function by a number of shards, so for 4 shards that is:
```
shard = hash(user_id) % 4
```

```
user 100 → shard 0
user 101 → shard 1
user 102 → shard 2
```

Data becomes more evenly distributed.

Advantages
- good load balancing
- avoids hot shards

Problems:
- Range queries become expensive, it might require querying every shard, like `SELECT * FROM users WHERE id BETWEEN 1000 AND 2000;`
- When we add a new server, then how data is distributed changes. For example, instead of using `hash(user_id) % 4`, we now use `hash(user_id) % 5`. Because of that, we need to move data between servers.