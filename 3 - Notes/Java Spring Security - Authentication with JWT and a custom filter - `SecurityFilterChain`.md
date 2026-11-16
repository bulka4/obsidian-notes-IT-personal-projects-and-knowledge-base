Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
The `SecurityFilterChain` ([[Java Spring Security - Defining security rules (`SecurityFilterChain`)|link]]) defines how every HTTP request is handled before it reaches a route (i.e. REST controller method ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]), a logic for handling a specific HTTP method for a specific endpoint).

For example:
```java
@Bean
SecurityFilterChain securityFilterChain(
	HttpSecurity http,
	JwtAuthenticationFilter jwtFilter
) throws Exception {
	return http
		.authorizeHttpRequests(auth -> auth
			.requestMatchers(
				"/api/auth/**", 
				"/h2-console/**"
			)
			.permitAll()
			.anyRequest()
			.authenticated()
		)
		.addFilterBefore(
			jwtFilter, 
			UsernamePasswordAuthenticationFilter.class
		)
		.build();
}
```

For example, it configures:
- Which endpoints require authentication (`/api/auth/` and `/h2-console/` doesn't require, the rest do require)
- Which filters are included and their order (include `jwtFilter` ([[Java Spring Security - Authentication with JWT and a custom filter - JWT filter|link]])).
# Where to define it
We can define it inside a security config ([[Java Spring Security - Security configuration|link]]).