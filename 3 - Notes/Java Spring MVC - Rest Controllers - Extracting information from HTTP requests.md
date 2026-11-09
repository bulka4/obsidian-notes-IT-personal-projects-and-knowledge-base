Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
Spring provides annotations ([[Java - Methods|link]]) that tell it where to get method parameters from.

We use them inside in an endpoint definition ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]), for example here we use `@RequestBody` annotation:
```java
@RestController
@RequestMapping("/api/tasks")
public class TaskController {
	@PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public TaskDtos.TaskResponse createTask(
            @Valid @RequestBody TaskDtos.CreateTaskRequest request
    ) {
        return taskService.createTask(request, currentUser);
    }
}
```
# `@RequestBody`
The `@RequestBody` annotation prepares the `request` parameter by extracting data from the request body:
```java
@Valid @RequestBody TaskDtos.CreateTaskRequest request
```

Suppose your frontend sends this HTTP request:
```
POST /api/tasks
Content-Type: application/json
```

With this JSON body:
```json
{
    "title": "Learn Spring",
    "description": "Understand REST controllers"
}
```

Spring automatically:
1. Reads the HTTP request body.    
2. Deserializes the JSON.    
3. Creates a `TaskDtos.CreateTaskRequest` Java object.    
4. Passes that object as the `request` argument.    

You don't need to manually parse JSON.

For example, the DTO might look something like this:
```java
public class CreateTaskRequest {
    private String title;
    private String description;

    // Getters and setters
}
```

DTO stands for Data Transfer Object. It's an object used to transfer data between different parts of an application or between the client and server.

Here, the frontend sends a request DTO, and the backend returns a response DTO.
# `@PathVariable`
```java
@PatchMapping("/{id}")
public TaskDtos.TaskResponse updateStatus(
        @PathVariable Long id,
        ...
)
```

Suppose the frontend sends:
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
### `@RequestParam` (another useful annotation)
It extracts query parameters from URLs.

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

The distinction:

|Annotation|Extracts data from|
|---|---|
|`@RequestBody`|HTTP request body, usually JSON|
|`@PathVariable`|URL path|
|`@RequestParam`|URL query parameters|
# Validation with `@Valid`
```java
@Valid @RequestBody TaskDtos.CreateTaskRequest request
```

This annotation tells Spring to validate the deserialized request object before executing the controller method.

For example, your DTO could contain:
```java
public class CreateTaskRequest {
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
