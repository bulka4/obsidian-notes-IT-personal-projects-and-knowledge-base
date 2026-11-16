Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
Using the `@AuthenticationPrincipal` ([[Java Spring Security - `@AuthenticationPrincipal`|link]]) annotation we can access user data from the Security Context in a route:
```java
@RestController
@RequestMapping("/api/tasks")
public class TaskController {
	@GetMapping
    public List<TaskDtos.TaskResponse> getTasks(
		@AuthenticationPrincipal AuthenticatedUser currentUser
    )
}
```

The `currentUser` is the `AuthenticatedUser(userId, email)` object that we saved in the Security Context in the JWT filter ([[Java Spring Security - Authentication with JWT and a custom filter - JWT filter|link]]).