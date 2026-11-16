Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
A record is a special kind of class designed primarily to hold data:
```java
public record CreateTaskRequest(
    @NotBlank @Size(max = 200) String title
) {}

// set request.title = "Learn Java"
CreateTaskRequest request = new CreateTaskRequest("Learn Java");
```

This declares a class named `CreateTaskRequest` with one component: `title`, of type `String`.

Java automatically generates:
- A constructor ([[Java - Class constructors|link]])
- A `title()` accessor method.    
- `equals()` and `hashCode()`.    
- `toString()`.
# Immutability
Records are shallowly immutable: you cannot reassign their components after construction.

For example:
```java
CreateTaskRequest request = new CreateTaskRequest("Learn Java");

request.title = "Something else"; // Not allowed
```

This makes records particularly useful for DTOs (Data Transfer Objects), such as: