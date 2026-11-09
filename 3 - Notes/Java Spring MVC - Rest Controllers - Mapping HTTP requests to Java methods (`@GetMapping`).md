Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_MVC–REST_Controllers]]
#Java #ProgrammingLanguages #JavaSpring  #JavaSpringMVC-RESTControllers 

# Introduction
Spring MVC provides annotations that connect HTTP methods and URL patterns to controller ([[Java Spring MVC - Rest Controllers - Rest Controller (`@RestController`)|link]]) methods.

For example:
```java
@RestController
@RequestMapping("/api/tasks")
public class TaskController {
	@GetMapping
	public List<TaskDtos.TaskResponse> getTasks(...) {
	    return taskService.getTasks(currentUser);
	}
}
```

`@GetMapping` - This tells Spring to execute this method when it receives a `GET` request matching the controller's URL.

Because the class has:
```java
@RequestMapping("/api/tasks")
```

the resulting endpoint is:
```
GET /api/tasks
```

We can also add additional paths, such as:
```java
@PatchMapping("/{id}")
```

and this will give the `PATCH /api/tasks/{id}` endpoint.