Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
Registration and login routes ([[Java Spring Security - Authentication with JWT and a custom filter - Registration & login routes|link]]) use the `userRepository` ([[Java Spring Security - User entity and repository|link]]) to work with user data in the database. It is an extension of the `JpaRepository` class:
```java
public interface UserRepository extends JpaRepository<AppUser, Long> {
    Optional<AppUser> findByEmail(String email);
    boolean existsByEmail(String email);
}
```

It will be registered as a bean by Spring Data because it extends the `JpaRepository` class, so we don't have to define it inside the `SecurityConfig` ([[Java Spring Security - Authentication with JWT and a custom filter - `SecurityConfig`|link]]).