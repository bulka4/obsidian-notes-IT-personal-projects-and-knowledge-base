Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
Before authentication can happen, your application needs to store user information.

Your example:
```java
@Entity
@Table(name = "app_users")
public class AppUser {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, unique = true, length = 254)
    private String email;

    @Column(nullable = false)
    private String passwordHash;
}
```

The application stores:
- User ID.    
- Email.    
- Password hash.    

The repository provides access to user records in a database:
```java
public interface UserRepository extends JpaRepository<AppUser, Long> {
    Optional<AppUser> findByEmail(String email);
    boolean existsByEmail(String email);
}
```

These are Spring Data JPA derived query methods ([[Java Spring Data - Query Method Derivation|link]]).

Spring generates their implementations based on method names.

They are used by:
- Registration: checking whether an email already exists.    
- Login: retrieving a user by email.    
- Authentication: loading user information through `UserDetailsService`.

`UserRepository` is registered as a bean ([[Java Spring - Bean|link]]) because it extends the `JpaRepository` class so Spring will automatically use it for dependency injection ([[Java Spring - Dependency injection|link]]).
# Example authentication flow using `UserRepository`
Example authentication flow using `UserRepository` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].