Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
The `@RequestParam` annotation is used in REST controller methods ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]) with method's parameters to specify where to get those parameters from.

It specifies to extract query parameters from URLs.

For example:
```
GET /api/tasks?status=TODO&page=2
```

You could handle this with:
```java
@GetMapping
public List<TaskDtos.TaskResponse> getTasks(
        @RequestParam String status,
        @RequestParam int page
) {
    // ...
}
```

Spring would pass `"TODO"` and `2` to the method.