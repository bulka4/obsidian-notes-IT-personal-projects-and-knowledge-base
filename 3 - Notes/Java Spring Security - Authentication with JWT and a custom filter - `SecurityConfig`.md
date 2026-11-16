Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
We create a central configuration ([[Java Spring Security - Security configuration|link]]) class annotated with `@Configuration` ([[Java Spring - Configuration|link]]) that defines how Spring Security should process HTTP requests:
```java
@Configuration
public class SecurityConfig {
    // securityFilterChain specifies how to process each HTTP request
    @Bean
    SecurityFilterChain securityFilterChain(
        HttpSecurity http,
        JwtAuthenticationFilter jwtFilter
    ) throws Exception {
        return http
            .csrf(csrf -> csrf.disable())
            .cors(cors -> {})
            // don't create a session (we will use JWT token for authentication)
            .sessionManagement(session ->
                session.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            )
            .authorizeHttpRequests(auth -> auth
                // Login and registration endpoints doesn't require authentication
                .requestMatchers("/api/auth/**", "/h2-console/**")
                .permitAll()
                // all other endpoints require authentication
                .anyRequest()
                .authenticated()
            )
            .headers(headers -> headers.frameOptions(frame -> frame.sameOrigin()))
            // Use the jwtFilter before UsernamePasswordAuthenticationFilter 
            // UsernamePasswordAuthenticationFilter will not be used in this app
            .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class)
            .build();
    }

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

    @Bean
    CorsConfigurationSource corsConfigurationSource(
        @Value("${app.cors.allowed-origin}") String allowedOrigin
    ) {
        CorsConfiguration config = new CorsConfiguration();
        config.setAllowedOrigins(List.of(allowedOrigin));
        config.setAllowedMethods(List.of("GET", "POST", "PATCH", "DELETE", "OPTIONS"));
        config.setAllowedHeaders(List.of("Authorization", "Content-Type"));
        config.setExposedHeaders(List.of("Authorization"));
        config.setAllowCredentials(false);

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", config);
        return source;
    }
}
```

`@Configuration` marks the class as a source of Spring bean definitions that can be automatically injected as dependencies to other classes ([[Java Spring - Dependency injection|link]]).

We create there methods that create objects (beans) that will be used by Spring Security automatically whenever needed, for example:
- `SecurityFilterChain` - [[Java Spring Security - Authentication with JWT and a custom filter - `SecurityFilterChain`|link]] 
- `PasswordEncoder` and `AuthenticationManager` - [[Java Spring Security - Authentication with JWT and a custom filter - Registration & login routes|link]] 
# Dependency injection - Example
For example, when we create the `AuthenticationManager` bean like in the example above, we can then use it in another class, for example in a REST controller ([[Java Spring Security - Authentication with JWT and a custom filter - Registration & login routes|link]]):
```java
@RestController
@RequestMapping("/api/auth")
public class AuthController {
	private final AuthenticationManager authenticationManager;
	
	public AuthController(
		AuthenticationManager authenticationManager
	) {
		// Spring will create and provide the `authenticationManager` instance
		// of the `AuthenticationManager` class
		this.authenticationManager = authenticationManager;
	}
}
```

and because `authenticationManager` is a bean, Spring will perform automatic dependency injection ([[Java Spring - Dependency injection|link]]), i.e. we don't have to create an object of `authenticationManager`.