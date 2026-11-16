Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
What filters are used is defined by what `HttpSecurity` methods we use inside the `SecurityFilterChain` ([[Java Spring Security - Defining security rules (`SecurityFilterChain`)|link]]):
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

For example, if we use the `.cors()` method like in this example, this will add the `CorsFilter`.
# What do filters do
A filter can perform operations such as:
- Inspect HTTP headers (e.g. Authorization).
- Authenticate users.
- Check whether a user has permission to access a resource.
- Prevent certain types of attacks.
- Manage security-related information.
- Reject requests that don't meet security requirements.
- Modify HTTP responses by adding security headers.

Each filter can:
- Perform its operation and pass the request to the next filter.
- Stop the chain and return an error response.
- Potentially modify the request or response.
# What are the different types of filters?
Let's group them by responsibility.
## A. Authentication filters
Their responsibility is to establish the identity of the user.

Examples:

|Filter|Responsibility|
|---|---|
|`UsernamePasswordAuthenticationFilter`|Authenticates using username and password from a login request.|
|`BasicAuthenticationFilter`|Authenticates using HTTP Basic credentials.|
|`BearerTokenAuthenticationFilter`|Authenticates using OAuth2 Bearer tokens.|
|`JwtAuthenticationFilter`|Your custom filter that authenticates using JWT.|
## B. Authorization filters
Their responsibility is to determine whether a request is allowed.

|Filter|Responsibility|
|---|---|
|`AuthorizationFilter`|Checks whether the current user is authorized to access the requested resource.|

For example, it enforces your configuration:
```
.anyRequest().authenticated()
```
## C. Security context management filters
These manage information about the currently authenticated user.

| Filter                          | Responsibility                                                                |
| ------------------------------- | ----------------------------------------------------------------------------- |
| `SecurityContextHolderFilter`   | Loads the security context for the current request and manages its lifecycle. |
| `AnonymousAuthenticationFilter` | Provides an anonymous authentication when no authenticated user is available. |
## D. Security protection filters
These protect against different types of attacks or security problems.

|Filter|Responsibility|
|---|---|
|`CsrfFilter`|Protects against Cross-Site Request Forgery (CSRF).|
|`HeaderWriterFilter`|Adds security-related HTTP headers to responses.|
|`CorsFilter`|Handles Cross-Origin Resource Sharing (CORS).|
## E. Exception handling filters

|Filter|Responsibility|
|---|---|
|`ExceptionTranslationFilter`|Translates authentication and authorization exceptions into appropriate HTTP responses or authentication entry-point handling.|
## F. Other infrastructure filters

|Filter|Responsibility|
|---|---|
|`LogoutFilter`|Processes logout requests.|
|`RequestCacheAwareFilter`|Restores previously saved requests after authentication.|
|`WebAsyncManagerIntegrationFilter`|Integrates Spring Security's context with asynchronous request processing.|
|`SecurityContextHolderAwareRequestFilter`|Wraps servlet requests with security-aware functionality.|
|`DisableEncodeUrlFilter`|Prevents session IDs from being encoded into URLs.|
# Filter ordering and adding a new filter with `addFilterBefore`
We can add our own filter like this:
```java
.addFilterBefore(
    jwtFilter,
    UsernamePasswordAuthenticationFilter.class
)
```

here:
- The first argument is the filter that we want to use
- The second argument is a reference filter - used to define when to execute the first filter. The filter from the first argument will be executed before this one.

This inserts our JWT filter ([[Java Spring Security - Authentication with JWT and a custom filter - JWT filter|link]]) before the standard username/password authentication filter.

Filter ordering matters because authentication must be established before authorization rules are evaluated.

As a reference filter, we can use any filter from a defined filter ordering registry, i.e. from the `FilterOrderRegistration` class defined here - [link](https://github.com/spring-projects/spring-security/blob/main/config/src/main/java/org/springframework/security/config/annotation/web/builders/FilterOrderRegistration.java?utm_source=chatgpt.com). This registry defines orders of filters. The filter that we use as a reference, doesn't have to be used in our app, it just needs to be defined in this ordering registry.