Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
`@Service` is a Spring annotation that marks a class as a service component, typically containing business logic.

It does two main things:
1. Registers the class as a Spring bean ([[Java Spring - Bean|link]]), so Spring can manage its lifecycle and inject it into other classes.    
2. Communicates the architectural role of the class: it belongs to the service/business-logic layer. 

Technically, `@Service` is a specialization of `@Component`. It doesn't automatically add transactions, security, or other business behavior.

Example:
```java
@Service
public class TaskService {
    public void createTask(...) {
        // Business logic
    }
}
```

You can inject it into a controller:
```java
@RestController
public class TaskController {
    private final TaskService taskService;

    public TaskController(TaskService taskService) {
        this.taskService = taskService;
    }
}
```

In short: `@Service` registers a Spring bean and identifies it as part of the business-logic layer.