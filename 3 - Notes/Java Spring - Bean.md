Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
A bean is an object managed by the Spring IoC container.
# Creating a bean
To create a bean, there are two options:
## A. Create a class with a proper annotation
Create a class with a proper annotation, for example `@Component`:
```java
@Component
public class UserService {
    public void sayHello() {
        System.out.println("Hello!");
    }
}
```

Then, Spring will create automatically an instance of this class which will be registered as a bean. We don't have to create this instance on our own by writing:
```java
UserService userService = new UserService()
```
## B. Create a method with a proper annotation
Create a method with a proper annotation, for example `@Bean`:
```java
@Configuration
public class AppConfig {
    @Bean
    public UserRepository userRepository() {
        return new UserRepository();
    }
}

public class UserRepository {
    public void findUsers() {
        System.out.println("Finding users...");
    }
}
```

A method with the `@Bean` annotation must return an object of some class. Spring executes this method (`userRepository()`), takes the returned object and registers it as a bean.

Notice that `UserRepository` doesn't need `@Component` because we explicitly register its instance using `@Bean`.

Just like in case of classes, Spring will run this method automatically, we don't need to run this method on our own by writing in code:
```java
UserRepository userRepository = userRepository()
```
# Annotations - creating beans
Annotations that we can use to create beans:
## Classes
Annotations for classes:

|Annotation|Purpose|
|---|---|
|`@Component`|Generic Spring-managed bean.|
|`@Service`|Bean representing a service/business logic layer.|
|`@Repository`|Bean representing a data access layer.|
|`@Controller`|Bean handling MVC web requests.|
|`@RestController`|Controller for REST APIs.|
|`@Configuration`|Class containing Spring bean configuration methods.|
## Methods
Annotations for methods:

|Annotation|Purpose|
|---|---|
|`@Bean`|Registers the object returned by the method as a Spring bean.|
|`@Autowired`|Injects a dependency (can be used on methods, constructors and fields).|
|`@PostConstruct`|Marks a method to execute after bean initialization.|
|`@PreDestroy`|Marks a method to execute before bean destruction.|
# What arguments Spring uses to create beans
When Spring creates a bean and it needs to provide arguments, there are a few options for how it can do this:
## 1. Constructor arguments that are other beans
When arguments are other beans:
```java
@Component
public class AuthService {
    private final UserRepository userRepository;

    public AuthService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}
```

Spring automatically finds a `UserRepository` bean and injects it. This is so called dependency injection - [[Java Spring - Dependency injection|link]].
## **2. Constructor arguments that are not beans**
When arguments are not beans, for example, a `String`, `int`, or other configuration value, there are two options:
### 2.a Use `application.properties` and `@Value`
We can use `application.properties` and `@Value` annotation:
```java
@Component
public class AuthService {
    private final String applicationName;

    public AuthService(
        @Value("${app.name}") String applicationName
    ) {
        this.applicationName = applicationName;
    }
}
```

And in `application.properties`:
```
app.name=MyApplication
```

Here, Spring gets the value from the application configuration rather than from another bean.
### 2.b Create a method that creates an object with specific arguments
If our argument for the `AuthService` class is not a bean, then in order to create the `AuthService` bean, we can create another method that creates an object of this class with specific arguments, registered as a bean.

So we define the `AuthService` class as a normal class (not registered as a bean yet):
```java
public class AuthService {
    private final String applicationName;

    public AuthService(
        String applicationName
    ) {
        this.applicationName = applicationName;
    }
}
```

and then, we create a method that will create an object of the `AuthService` class and register it as a bean:
```java
@Configuration
public class AppConfig {
    @Bean
    public AuthService authService() {
        return new AuthService("MyApplication");
    }
}
```
# Related topics
1. [[Java Spring - `@Service` annotation]]
2. [[Java Spring - Dependency injection]]