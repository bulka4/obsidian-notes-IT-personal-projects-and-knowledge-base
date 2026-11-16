Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
Normally, in Java, you create objects yourself using `new`:
```java
TaskService taskService = new TaskService();
TaskController controller = new TaskController(taskService);
```

With Spring, you can delegate object creation and dependency management to Spring.

This is called Inversion of Control (IoC): instead of your code controlling object creation and wiring, the Spring container does it.

The Spring container:
- Creates objects.    
- Manages their lifecycle.    
- Injects dependencies into other objects.    
- Makes objects available to other parts of the application.
# Registering objects in the IoC container and dependency injection
Instead of creating objects and using them in other classes:
```java
MyRepository repository = new MyRepository();

MyService service = new MyService(repository);
```

we can register objects in the IoC container using `@Repository` and `@Service` annotations ([[Java - Annotations|link]]):
```java
@Repository
public class MyRepository {
}

@Service
public class MyService {
    private final MyRepository repository;

    public MyService(MyRepository repository) {
        this.repository = repository;
    }
}
```

What happens?
1. Spring scans your application and discovers `MyRepository` and `MyService`.
2. Spring creates instances of these classes.
3. Spring registers those instances in its IoC container.
4. When creating `MyService`, Spring sees that its constructor requires `MyRepository`.
5. Spring finds the registered `MyRepository` bean and passes it to the constructor (performs a dependency injection).

You don't have to write new `MyRepository()` or new `MyService()` yourself.
# Implementing method's logic
Spring Data can also automatically implement a method's logic based on its name. More info can be found here - [[Java Spring Data - Query Method Derivation]].
# Annotation-based behavior
Spring examines annotations and applies predefined behavior.

For example:
```java
@Service
public class TaskService {

    @Transactional
    public void createTask(Task task) {
        taskRepository.save(task);
    }
}
```

Spring recognizes `@Transactional` and wraps the method invocation with transaction management.

You don't implement an interface or write transaction-handling code yourself.

Other examples:

|Annotation|Behavior|
|---|---|
|`@Transactional`|Transaction management|
|`@Async`|Asynchronous method execution|
|`@PreAuthorize`|Method-level authorization|
|`@Cacheable`|Caching method results|
|`@Scheduled`|Scheduled method execution|

These annotations are processed by infrastructure provided by the corresponding Spring modules.

For example, `@Transactional` uses proxy-based AOP in the usual configuration.
# Callback interfaces
Another pattern is when you implement an interface and Spring calls its methods at specific moments.

For example:
```java
@Component
public class StartupHandler implements ApplicationRunner {
    @Override
    public void run(ApplicationArguments args) {
        System.out.println("Application started!");
    }
}
```

You implement `ApplicationRunner`, and Spring Boot automatically calls `run()` when the application starts.

You provide the logic; Spring determines when to execute it.

Other examples:
- `CommandLineRunner` – execute code at application startup.    
- `InitializingBean` – execute logic after bean initialization.    
- `DisposableBean` – execute logic when a bean is destroyed.    
- `ApplicationListener` – react to application events.    

Documentation: [Spring Boot – Application Startup](https://docs.spring.io/spring-boot/reference/features/spring-application.html?utm_source=chatgpt.com).
# Related topics
1. [[Java Spring - Bean]]
	1. [[Java Spring - `@Service` annotation]]
2. [[Java Spring - Dependency injection]]