Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
The `@RequestBody` annotation is used in REST controller methods ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]) with method's parameters to specify where to get those parameters from.

It specifies to extract a parameter from the request body.
```java
@PatchMapping("/{id}")
public TaskDtos.TaskResponse updateStatus(
	@RequestBody TaskDtos.UpdateTaskStatusRequest request
) {
	...
}
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