Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
Instead of manually creating an object of a class and using it as an argument for a constructor in another class:
```java
public class UserController {
    private final UserService userService;
    private final UserRepository userRepository;

    public UserController(
        UserService userService,
        UserRepository userRepository
    ) {
        this.userService = userService;
        this.userRepository = userRepository;
    }
}

UserService userService = new UserService();
UserRepository userRepository = new UserRepository();
UserController userController = new UserController(
	userService,
	userRepository
);
```

We can register those objects as beans ([[Java Spring - Bean|link]]):
```java
// Register `UserController` as a bean by using the `@Component` annotation
@Component
public class UserController {...}

// Register the `UserService` bean
@Component
public class UserService {
    public void sayHello() {
        System.out.println("Hello!");
    }
}

// Register the `UserRepository` bean (created by the `userRepository` method)
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

and then, Spring will automatically create objects of the `UserRepository` and `UserService` classes, and use them to create an object of the `UserController` class.