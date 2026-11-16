Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
The `securityFilterChain` defines how every HTTP request is handled before it reaches a route (i.e. REST controller method ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]), a logic for handling a specific HTTP method for a specific endpoint).

For example:
```java
@Bean
SecurityFilterChain securityFilterChain(
	HttpSecurity http,
	JwtAuthenticationFilter jwtFilter
) throws Exception {
	return http
		.csrf(csrf -> csrf.disable())
		.cors(cors -> {})
		.sessionManagement(session ->
			session.sessionCreationPolicy(
				SessionCreationPolicy.STATELESS)
			)
		.authorizeHttpRequests(auth -> auth
			.requestMatchers(
				"/api/auth/**", 
				"/h2-console/**"
			)
			.permitAll()
			.anyRequest()
			.authenticated()
		)
		.headers(headers -> headers.frameOptions(
			frame -> frame.sameOrigin()
		))
		.addFilterBefore(
			jwtFilter, 
			UsernamePasswordAuthenticationFilter.class
		)
		.build();
}
```

For example, it configures:
- Which filters are included and their order.
- Authentication mechanisms.
- Authorization rules (`permitAll()`, `authenticated()`, etc.).
- Session management (STATELESS, etc.).
- CSRF and CORS handling.
- Security headers.
# Where to define it
We can define it inside a security config ([[Java Spring Security - Security configuration|link]]). It needs to be registered as a bean ([[Java Spring - Bean|link]]) so that Spring Security can use it.
# Filters
The `SecurityFilterChain` defines what filters to use. More about filters - [[Java Spring Security - `SecurityFilterChain` - Filters]].
# Example authentication flow using `SecurityFilterChain`
Example authentication flow using `SecurityFilterChain` is described here - [[Java Spring Security - Authentication with JWT and a custom filter]].
# Configuration methods
## CSRF
```java
.csrf(csrf -> csrf.disable())
```

CSRF stands for Cross-Site Request Forgery.

It is an attack where a malicious website attempts to make a user's browser perform an unwanted operation on another website where the user is authenticated.

Your application disables CSRF because it uses stateless Bearer-token authentication.

This is appropriate for a typical API where authentication tokens are explicitly supplied in the Authorization header and are not automatically attached by the browser.

However, disabling CSRF is not universally safe for every JWT application. For example, if authentication tokens are stored in cookies and automatically sent by browsers, CSRF protection may still be necessary.
## CORS
```java
.cors(cors -> {})
```

CORS stands for Cross-Origin Resource Sharing.

It controls which external origins are allowed to make requests to your backend from browsers.

For example, your React frontend and Spring backend might run on different ports or domains.

Your CORS configuration is defined separately using `CorsConfigurationSource`.
## Session management
```java
.sessionManagement(session ->
    session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
```

This tells Spring Security not to create or use HTTP sessions to maintain authentication state.

Each request must carry its own authentication information.

This is an important part of the JWT architecture.
## Authorization rules
This defines which HTTP requests require authentication. For example:
```java
.authorizeHttpRequests(auth -> auth
    .requestMatchers("/api/auth/**", "/h2-console/**")
    .permitAll()
    .anyRequest()
    .authenticated()
)
```

This example means:
- Authentication endpoints are publicly accessible.    
- H2 console is publicly accessible.    
- All other endpoints require authentication.   

Useful methods:

|Method|Purpose|
|---|---|
|`permitAll()`|Allows everyone|
|`authenticated()`|Requires an authenticated user|
|`hasAuthority()`|Requires a specific authority|
|`hasAnyAuthority()`|Requires at least one specified authority|
|`hasRole()`|Requires a specific role|
|`denyAll()`|Denies everyone|

You can also match particular HTTP methods:
```java
.authorizeHttpRequests(auth -> auth
    .requestMatchers(HttpMethod.GET, "/api/public/**")
        .permitAll()
    .requestMatchers("/api/admin/**")
        .hasRole("ADMIN")
    .anyRequest()
        .authenticated())
```
