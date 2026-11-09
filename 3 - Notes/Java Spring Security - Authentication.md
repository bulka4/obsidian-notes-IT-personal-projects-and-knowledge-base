Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
Spring provides the `@AuthenticationPrincipal` annotation ([[Java - Methods|link]]):
```java
@AuthenticationPrincipal AuthenticatedUser currentUser
```

that is used in an endpoint definition ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]), for example:
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

and it is used to prepare the `currentUser` argument with information about the currently authenticated user.

Here's the general process:
1. A client sends a request with authentication credentials, for example a session cookie or JWT.   
2. Spring Security processes the request and authenticates the user.    
3. Spring Security stores the authentication information in its `SecurityContext`.    
4. The controller receives the authenticated principal by executing instructions defined by the `@AuthenticationPrincipal`. 
	1. The `@AuthenticationPrincipal` instruction prepares the `currentUser` parameter ([[Java - Methods|link]])

In this case, the principal is expected to be an instance of your custom class:
```java
AuthenticatedUser
```

For example, that class might contain:
```java
public class AuthenticatedUser {
    private Long id;
    private String email;
}
```

Then you can use:
```java
currentUser.getId()
```

to identify the user who made the request.
# Why is this useful?
Consider a to-do application where we create tasks to do. You don't want users to retrieve or modify other people's tasks.

Instead of accepting a user ID from the frontend:
```
GET /api/tasks?userId=123
```

you obtain the user identity from the authenticated security context.

This is safer because the client cannot simply change the user ID in the request to impersonate someone else.

One important distinction: `@AuthenticationPrincipal` retrieves the authenticated principal; it doesn't itself enforce authentication. Whether unauthenticated requests are rejected is determined by your Spring Security configuration. Also, the principal can be null in some configurations.