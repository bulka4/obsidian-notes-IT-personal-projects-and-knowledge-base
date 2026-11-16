Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
`@Configuration` tells Spring that a class contains bean definitions and configuration instructions that Spring should process when starting the application.

For example:
```java
@Configuration
public class SecurityConfig {
    @Bean
    PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    AuthenticationManager authenticationManager(
            AuthenticationConfiguration configuration
    ) throws Exception {
        return configuration.getAuthenticationManager();
    }
}
```
# What happens internally?
1. Spring scans your application for configuration classes.    
2. It discovers `SecurityConfig` because it has `@Configuration`.    
3. Spring processes the class and discovers its `@Bean` methods.    
4. It invokes those methods and registers their returned objects in the IoC container.    
5. Other components can request those beans through dependency injection.