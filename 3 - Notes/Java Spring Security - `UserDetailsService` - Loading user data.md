Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
`UserDetailsService` is an interface from Spring Security that is used for loading user information during authentication:
```java
public interface UserDetailsService {
    UserDetails loadUserByUsername(String username)
		throws UsernameNotFoundException;
}
```

Its main method is `UserDetails loadUserByUsername(String username)` (required). Despite the method name, `username` does not have to be an actual username. It can be an email, phone number, or another identifier.

Spring Security calls this method when it needs to retrieve a user during authentication.

We can implement it and provide our own implementation of `loadUserByUsername()`:
```java
@Service
public class CustomUserDetailsService implements UserDetailsService {
    ...
    @Override
    public UserDetails loadUserByUsername(String email) {
	    ...
    }
}
```

The method returns `UserDetails` ([[Java Spring Security - `User` (`UserDetails`) class|link]]), another Spring Security interface.
# `AuthenticationManager`
When we use `AuthenticationManager` to login ([[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`|link]]), then it automatically uses the `UserDetailsService`.
# Example
```java
@Service
public class CustomUserDetailsService
        implements UserDetailsService {

    private final UserRepository userRepository;

    public CustomUserDetailsService(
		UserRepository userRepository
	) {
        this.userRepository = userRepository;
    }

    @Override
    public UserDetails loadUserByUsername(String email) {
        AppUser user = userRepository.findByEmail(email)
            .orElseThrow(() ->
                new UsernameNotFoundException("User not found")
			);

        return User.withUsername(user.getEmail())
            .password(user.getPasswordHash())
            .authorities("USER")
            .build();
    }
}
```

This implementation:
1. Receives an email.    
2. Retrieves the corresponding user from the database.    
3. Converts the application-specific `AppUser` object (`user`) into a Spring Security `UserDetails` object (`User`) ([[Java Spring Security - `User` (`UserDetails`) class|link]]).
4. Returns that object to Spring Security.
# Example authentication flow using `UserDetailsService`
Example authentication flow using `UserDetailsService` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].