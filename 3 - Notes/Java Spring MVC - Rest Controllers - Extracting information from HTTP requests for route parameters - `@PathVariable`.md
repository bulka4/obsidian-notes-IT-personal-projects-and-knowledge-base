Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
The `@PathVariable` annotation is used in REST controller methods ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]) with method's parameters to specify where to get those parameters from.

It specifies to extract parameters from the URL.
```java
@PatchMapping("/{id}")
public TaskDtos.TaskResponse updateStatus(
        @PathVariable Long id,
        ...
)
```

Suppose the client sends:
```
PATCH /api/tasks/123
```

Spring extracts `123` from the URL and converts it into a Java `Long`.

The method effectively receives:
```
id = 123L;
```

You can have multiple path variables, too:
```java
@GetMapping("/{taskId}/comments/{commentId}")
public void getComment(
        @PathVariable Long taskId,
        @PathVariable Long commentId
) {
    // ...
}
```
