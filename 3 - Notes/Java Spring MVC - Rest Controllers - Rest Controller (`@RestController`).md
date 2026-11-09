Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
Spring REST controller is a class which job is to receive HTTP requests from clients, extract information from those requests, call the appropriate business logic, and return HTTP responses.

The important thing to understand is that Spring does a lot of work automatically. You don't manually create an HTTP server, parse request URLs, extract JSON, or construct HTTP responses.
# REST controller
```java
@RestController
@RequestMapping("/api/tasks")
public class TaskController {
    ...
}
```

`@RestController` - This is a Spring annotation that tells Spring:
- This class handles HTTP requests.    
- Its methods can be mapped to HTTP endpoints.    
- Return values from its methods should generally be serialized into HTTP response bodies.

For example, if a method returns:
```java
return List.of("Task 1", "Task 2");
```

Spring will automatically convert the list into JSON:
```json
["Task 1", "Task 2"]
```

This conversion is normally handled by Spring's HTTP message converters, commonly using the Jackson JSON library.

An important detail: `@RestController` is effectively a combination of two annotations:
- `@Controller` — identifies a Spring MVC controller.    
- `@ResponseBody` — tells Spring to put method return values into the HTTP response body rather than treating them as view names.

`@RequestMapping("/api/tasks")` - This defines the base URL for all endpoints in a controller. For example:
- `GET /api/tasks`    
- `POST /api/tasks`    
- `PATCH /api/tasks/123`    
- `DELETE /api/tasks/123`    

You can think of it as a common URL prefix.