Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
A HashMap in Java is a data structure that stores data as key-value pairs. It allows you to efficiently retrieve a value using its key, rather than searching through all elements.
```java
import java.util.HashMap;
import java.util.Map;

Map<String, Integer> ages = new HashMap<>();

// Adding elements
ages.put("John", 25);
ages.put("Alice", 30);
ages.put("Bob", 22);

// Retrieving values
int johnAge = ages.get("John"); // 25

// Checking whether a key exists
boolean exists = ages.containsKey("Alice");

// Removing elements
ages.remove("Bob");

// Updating a value
ages.put("John", 26);
```
- `String` is the key type.    
- `Integer` is the value type.    
- Each key must be unique.    
- Values don't have to be unique.
# How does a HashMap work internally?
A HashMap uses a concept called hashing to find values efficiently ([[Software Engineering - Data structures - Hash tables|link]]).

Imagine you insert:
```java
ages.put("John", 25);
```

Java approximately does the following:
1. Calls `"John".hashCode()` to calculate a hash value.    
2. Uses that hash to determine where to store the entry in its internal array (a bucket).    
3. Stores the key-value pair there.    

When you retrieve:
```java
ages.get("John");
```

Java:
1. Calculates the hash of `"John"` again.    
2. Uses it to locate the relevant bucket.    
3. Compares keys to find the matching entry.    
4. Returns its value.
# What are hash collisions?
Different keys can produce the same bucket location. This is called a hash collision.

For example:
```
Key A ── hash ──┐
                ├── Bucket 3
Key B ── hash ──┘
```

Java handles collisions by storing multiple entries in the same bucket.

In Java 8+, buckets can use:
- Linked lists for smaller numbers of colliding entries.    
- Balanced trees (red-black trees) when collisions become sufficiently numerous and certain conditions are met.    

You don't need to implement collision handling yourself.
# Important HashMap characteristics

|Characteristic|Behaviour|
|---|---|
|Key uniqueness|Keys must be unique|
|Value uniqueness|Values can repeat|
|Null keys|One allowed|
|Null values|Multiple allowed|
|Ordering|No guaranteed iteration order|
|Thread safety|Not thread-safe|
|Lookup complexity|Average O(1)|

The O(1) lookup complexity means that retrieval generally takes constant time, regardless of how many entries the map contains. In pathological collision cases, performance can be worse.
# Iterating through a HashMap
You can iterate through its entries:
```java
for (Map.Entry<String, Integer> entry : ages.entrySet()) {
    System.out.println(entry.getKey());
    System.out.println(entry.getValue());
}
```

Or just keys:
```java
for (String name : ages.keySet()) {
    System.out.println(name);
}
```

Or just values:
```java
for (Integer age : ages.values()) {
    System.out.println(age);
}
```
# `equals()` and `hashCode()`
This is particularly important when creating your own classes as HashMap keys.

Java relies on two methods:
- `hashCode()` — helps determine which bucket to search.    
- `equals()` — determines whether two keys represent the same key.    

If you create a custom class and want to use its objects as keys, you should implement both consistently (or use a record, which generates them automatically).

For example:
```java
Map<User, String> users = new HashMap<>();

User user1 = new User(1);
User user2 = new User(1);

users.put(user1, "Administrator");

System.out.println(users.get(user2));
```

With both methods correctly implemented, this returns `"Administrator"`.

The HashMap:
1. Calculates the hash code of `user2`.
2. Finds the appropriate bucket.
3. Compares `user2` with keys in that bucket using `equals()`.
4. Finds `user1`, because they are logically equal.
5. Returns the associated value.

Without a proper `hashCode()` implementation, the HashMap might search a different bucket and fail to find an equal key.
# Why mutable objects are dangerous as HashMap keys
A mutable object is an object whose fields can change after creation.

Consider this class:
```java
class User {
    int id;

    User(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {
        if (!(obj instanceof User other)) return false;
        return this.id == other.id;
    }

    @Override
    public int hashCode() {
        return Integer.hashCode(id);
    }
}
```

Now let's use it as a HashMap key:
```java
Map<User, String> users = new HashMap<>();

User user = new User(1);

users.put(user, "Administrator");
```

When we insert the user, Java calculates its hash code based on `id = 1` and stores the entry in the corresponding bucket.

But what happens if we modify the object?
```java
user.id = 2;

System.out.println(users.get(user)); // May return null!
```

Why?
1. When we inserted the user, its hash code was calculated using `id = 1`.    
2. The entry was stored in the bucket corresponding to that hash.    
3. We changed `id` to `2`.    
4. When retrieving the value, Java calculates the new hash code.    
5. It searches the bucket corresponding to the new hash, not the original one.    

The entry is still physically stored in the original bucket, so the lookup may fail.

Even this can fail:
```java
users.remove(user); // May also fail!
```

The object is still in the map, but the map can no longer reliably find it using its changed key.

The solution: Don't modify fields that participate in `equals()` and `hashCode()` while an object is being used as a HashMap key.

This is one reason immutable objects make particularly good keys.

For example, Java records are useful:
```java
record User(int id, String name) {}

Map<User, String> users = new HashMap<>();
```

Records are shallowly immutable: their component references cannot be reassigned, although referenced mutable objects can still change.
# 3. Why HashMap isn't thread-safe
First, what does thread safety mean?

Imagine a backend application handling multiple HTTP requests simultaneously.

Each request may execute on a different thread. Suppose they all access the same HashMap.
```java
Map<String, Integer> counters = new HashMap<>();
```

Two threads might try to modify it simultaneously:
```java
// Thread A
counters.put("visits", 100);

// Thread B
counters.put("visits", 200);
```

The problem is that `HashMap` does not coordinate concurrent access.

Possible consequences include:
- Lost updates.    
- Inconsistent observations of the map's state.    
- Race conditions when multiple operations interact.    

Even a seemingly simple operation can be problematic:
```java
counters.put("visits", counters.get("visits") + 1);
```

Imagine the current value is `10`.
1. Thread A reads `10`.    
2. Thread B reads `10`.    
3. Thread A calculates `11` and writes it.    
4. Thread B calculates `11` and writes it.    

The expected result was `12`, but the actual result is `11`.

This is a classic race condition.
## 3.1. ConcurrentHashMap
Java provides `ConcurrentHashMap` specifically for concurrent access.
```java
Map<String, Integer> counters = new ConcurrentHashMap<>();
```

It allows multiple threads to access and modify the map safely.

For example, you can use:
```java
counters.put("visits", 100);

counters.get("visits");

counters.remove("visits");
```

But what about the increment operation?

Simply using `ConcurrentHashMap` doesn't automatically make a sequence of multiple operations atomic.

Instead, use its atomic methods:
```java
counters.merge("visits", 1, Integer::sum);
```

This atomically:
- Inserts `1` if the key doesn't exist.    
- Otherwise, adds `1` to its existing value.    

You can also use:
```java
counters.putIfAbsent("visits", 0);
counters.compute("visits", (key, value) -> value + 1);
counters.computeIfAbsent("visits", key -> 0);
```

These methods perform their respective map operations atomically.
## 3.2. HashMap vs ConcurrentHashMap

|Feature|HashMap|ConcurrentHashMap|
|---|---|---|
|Thread-safe|No|Yes|
|Concurrent reads|No thread-safety guarantee|Supported|
|Concurrent writes|Not safe|Supported|
|Atomic operations|No|Yes, through methods like `compute` and `merge`|
|Null keys|One allowed|Not allowed|
|Null values|Allowed|Not allowed|
|Performance|Usually less overhead|Some coordination overhead|

`ConcurrentHashMap` uses internal concurrency mechanisms to allow multiple threads to work with the map without requiring one global lock for every operation.

It is generally preferable to synchronizing every access to a regular `HashMap` when you need a shared concurrent map.
## 3.3. When should you use each?

- `HashMap`: when the map is used by one thread, or when access is otherwise properly synchronized.    
- `ConcurrentHashMap`: when multiple threads share and modify the same map.    
- `Collections.synchronizedMap()`: another option when you want to synchronize access to an ordinary map, although compound operations and iteration need additional care.    

One important distinction: `ConcurrentHashMap` makes individual operations and its documented atomic methods thread-safe. It does not automatically make an entire sequence of unrelated operations atomic.