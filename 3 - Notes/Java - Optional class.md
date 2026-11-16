Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
`Optional<T>` is a Java class that represents a value that may or may not be present.

It is primarily used to avoid returning `null` and to make the possibility of a missing value explicit.

It belongs to the Java standard library (`java.util.Optional`), not Spring.
# 1. Why does Optional exist?
Consider a method that searches for a user:
```java
public User findUser(Long id) {
    // Search database
    // Return user if found, otherwise null
}
```

The problem is that the caller doesn't necessarily know that the method might return `null`.

If you try to use the returned value without checking it, you might get a `NullPointerException`.

For example:
```java
User user = findUser(123L);
System.out.println(user.getName()); // Could throw NullPointerException
```

Instead, you can return an `Optional<User>`:
```java
public Optional<User> findUser(Long id) {
    // Search database
    // Return Optional containing user or an empty Optional
}
```

Now the return type explicitly communicates that the result might be missing.
# useful Optional methods
|Method|Purpose|
|---|---|
|`isPresent()`|Checks whether a value exists|
|`isEmpty()`|Checks whether a value is absent|
|`get()`|Retrieves the value; throws if absent|
|`orElse(value)`|Returns value or a fallback|
|`orElseGet(supplier)`|Returns value or lazily calculates a fallback|
|`orElseThrow()`|Returns value or throws an exception|
|`ifPresent(action)`|Executes an action if a value exists|
|`map(function)`|Transforms the value if present|
# Creating an Optional
There are three commonly used methods:

1. `Optional.of(value)` - Creates an Optional containing a non-null value.
```java
Optional<String> name = Optional.of("John");
```

Passing `null` throws a `NullPointerException`.

2. `Optional.ofNullable(value)` - Creates an Optional containing a value, or an empty Optional if the value is `null`.
```java
String name = null;

Optional<String> optionalName = Optional.ofNullable(name);
```

3. `Optional.empty()` - Creates an empty Optional.
```java
Optional<String> name = Optional.empty();
```
