Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Lambda expressions in Java provide a concise way to define implementations of functional interfaces without creating a separate class or using an anonymous class.

They are particularly useful when working with collections, streams, callbacks, event handlers, and asynchronous operations.

A lambda expression has this general structure:
```java
(parameters) -> {
    // Code to execute
}
```

or, if it only returns a value:
```java
Calculator addition = (a, b) -> a + b;
```
# Anonymous class
Lambda expression can be used to define an anonymous class like described here - [[Java - Anonymous classes]]. 
# Functional interfaces
[[Java - Functional interface]]
# Using lambdas with collections
This is where lambda expressions become particularly useful.

Imagine you have a list of users:
```java
List<String> users = List.of(
    "John",
    "Alice",
    "Robert",
    "Anna"
);
```

You can iterate through the list using a lambda:
```java
users.forEach(user -> System.out.println(user));
```

Instead of:
```java
for (String user : users) {
    System.out.println(user);
}
```

Both approaches work.

You can also filter collections using streams.

For example, getting users whose names start with `A`:
```java
List<String> filteredUsers = users.stream()
    .filter(user -> user.startsWith("A"))
    .toList();
```

Result:
```
[Alice, Anna]
```

Here:
- `stream()` creates a stream from the collection.    
- `filter()` accepts a Predicate, implemented using a lambda.    
- `toList()` collects the results into a list.    

You can also transform values:
```java
List<Integer> lengths = users.stream()
    .map(user -> user.length())
    .toList();
```

Result:
```
[4, 5, 6, 4]
```
# Method references
There is an even shorter syntax related to lambdas called method references.

For example:
```java
users.forEach(user -> System.out.println(user));
```

Can be simplified to:
```java
users.forEach(System.out::println);
```

The `::` operator references an existing method instead of explicitly defining a lambda.

Another example:
```java
Function<String, Integer> getLength = text -> text.length();
```

Can become:
```java
Function<String, Integer> getLength = String::length;
```

This works when the referenced method matches the expected functional interface method.
# Variable scope
Lambdas can access variables from their surrounding scope.
```java
String message = "Hello";

Runnable task = () -> System.out.println(message);
```

As with anonymous classes, local variables accessed by a lambda must be `final` or effectively final.

There is also an important difference regarding `this`:
- In an anonymous class, `this` refers to the anonymous class instance.    
- In a lambda, `this` refers to the surrounding object.    

This distinction matters when working with object fields and methods.