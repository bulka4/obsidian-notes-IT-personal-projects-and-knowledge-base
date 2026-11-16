Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
To create `AuthenticationManager`, we can define in a configuration ([[Java Spring Security - Security configuration|link]]) a bean ([[Java Spring - Bean|link]]) like this:
```java
@Configuration
public class SecurityConfig {
	@Bean
    AuthenticationManager authenticationManager(
            AuthenticationConfiguration configuration
    ) throws Exception {
        return configuration.getAuthenticationManager();
    }
}
```

`AuthenticationConfiguration` provides access to Spring Security's configured authentication manager.

We generally don't implement `AuthenticationManager` ourself for a standard username/password authentication setup.

Spring Security coordinates the configured authentication providers and user lookup mechanisms.
# Example authentication flow using `AuthenticationManager`
Example authentication flow using `AuthenticationManager` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].