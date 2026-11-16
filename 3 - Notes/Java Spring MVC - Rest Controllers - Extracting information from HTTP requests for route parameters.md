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

Annotations we can use:
- `@RequestBody` - [[Java Spring MVC - Rest Controllers - Extracting information from HTTP requests for route parameters - `@RequestBody`|link]]
- `@PathVariable` - [[Java Spring MVC - Rest Controllers - Extracting information from HTTP requests for route parameters - `@PathVariable`|link]]
- `@RequestParam` - [[Java Spring MVC - Rest Controllers - Extracting information from HTTP requests for route parameters - `@RequestParam`|link]]
# Validation with `@Valid`
[[Java Spring MVC - Rest Controllers - Validating a request (`@Valid`)]]