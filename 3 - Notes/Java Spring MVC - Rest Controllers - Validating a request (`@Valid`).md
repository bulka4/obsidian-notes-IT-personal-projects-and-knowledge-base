Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
The `@Valid` annotation is used in REST controller methods ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]) with method's parameters to specify how those parameters should be validated:
```java
@PatchMapping("/{id}")
public TaskDtos.TaskResponse updateStatus(
	@Valid @RequestBody TaskDtos.UpdateTaskStatusRequest request
) {
	...
}
```

For example, our DTO could contain:
```java
public class UpdateTaskStatusRequest {
    @NotBlank
    @Size(max = 100)
    private String title;

    private String description;

    // Getters and setters
}
```

The validation annotations come from Jakarta Bean Validation.
- `@NotBlank` — the title cannot be null, empty, or only whitespace.    
- `@Size(max = 100)` — the title cannot exceed 100 characters.    

When Spring receives the request, it checks these constraints.

If validation fails, Spring normally returns HTTP `400 Bad Request` without executing the method.

You need a validation implementation on the classpath, commonly provided by Spring Boot's validation starter.
