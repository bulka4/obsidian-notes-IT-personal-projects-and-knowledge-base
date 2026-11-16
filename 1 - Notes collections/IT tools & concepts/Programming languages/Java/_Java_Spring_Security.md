Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
1. [[Java Spring Security - `Authentication` interface]]
	1. [[Java Spring Security - `UsernamePasswordAuthenticationToken` class]]
2. [[Java Spring Security - `AuthenticationManager` interface]]
	1. [[Java Spring Security - Creating the `authenticationManager`]]
	2. [[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`]]
3. [[Java Spring Security - Generating a JWT token]]
4. [[Java Spring Security - Parsing and validating a JWT token]]
5. [[Java Spring Security - SecurityContextHolder]]
6. [[Java Spring Security - `@AuthenticationPrincipal`]]
7. [[Java Spring Security - Security configuration]]
8. [[Java Spring Security - Defining security rules (`SecurityFilterChain`)]]
	1. [[Java Spring Security - `SecurityFilterChain` - Filters]]
9. [[Java Spring Security - `UserDetailsService` - Loading user data]]
10. [[Java Spring Security - `User` (`UserDetails`) class]]
11. [[Java Spring Security - `PasswordEncoder`]]
12. [[Java Spring Security - User entity and repository]]
13. [[Java Spring Security - `OncePerRequestFilter`]]
# Authentication with JWT and a custom filter
1. [[Java Spring Security - Authentication with JWT and a custom filter]]
	1. Classes:
		1. [[Java Spring Security - Authentication with JWT and a custom filter - `SecurityConfig`]]
		2. [[Java Spring Security - Authentication with JWT and a custom filter - `JwtService`]]
		3. [[Java Spring Security - Authentication with JWT and a custom filter - `UserRepository`]]
		4. [[Java Spring Security - Authentication with JWT and a custom filter - `UserDetailsService`]]
		5. [[Java Spring Security - Authentication with JWT and a custom filter - ]]
		6. [[Java Spring Security - Authentication with JWT and a custom filter - ]]
		7. [[Java Spring Security - Authentication with JWT and a custom filter - ]]
	2. Flow overview:
		1. [[Java Spring Security - Authentication with JWT and a custom filter - `SecurityFilterChain`]]
		2. [[Java Spring Security - Authentication with JWT and a custom filter - JWT filter]]
		3. [[Java Spring Security - Authentication with JWT and a custom filter - Providing user data in a route using `@AuthenticationPrincipal`]]
		4. [[Java Spring Security - Authentication with JWT and a custom filter - Registration & login routes]]
# Questions
- 
# Other topics to explore
Those topics were suggested by ChatGPT. For most of them I have already notes. Those topics need to be reviewed to determine which ones to learn.

1. Authentication and authorization fundamentals
	General concepts
	├─ 1.1 Authentication vs authorization
	├─ 1.2 Authentication and authorization lifecycle
	└─ 1.3 Principals, credentials, roles and authorities
2. Spring Security architecture and core components
	General Spring Security mechanisms
	├─ 2.1 SecurityFilterChain and HttpSecurity
	├─ 2.2 Spring Security filter chain
	├─ 2.3 Authentication interface and Authentication objects	
	├─ 2.4 AuthenticationManager and AuthenticationProvider	
	├─ 2.5 UserDetails and UserDetailsService	
	├─ 2.6 SecurityContext and SecurityContextHolder	
	├─ 2.7 PasswordEncoder and password hashing	
	└─ 2.8 GrantedAuthority, roles and permissions
3. Authentication architectures
	Different ways of implementing authentication
	3.1 Stateless JWT authentication with a custom filter	
	Your current Todo application architecture
	├─ 3.1.1 Architecture overview and authentication flows	
	├─ 3.1.2 Registration and login implementation	
	├─ 3.1.3 JWT generation and validation	
	├─ 3.1.4 Custom JWT authentication filter	
	├─ 3.1.5 Mapping JWT claims to an authenticated principal	
	└─ 3.1.6 Security configuration for stateless authentication
	3.2 Session-based authentication	
	Server-side sessions and session cookies	
	3.3 HTTP Basic authentication	
	Username and password sent with HTTP requests	
	3.4 OAuth 2.0 and OpenID Connect authentication	
	Delegated authentication and external identity providers	
	3.5 JWT authentication using Spring OAuth2 Resource Server	
	Using Spring's built-in JWT resource server support instead of a custom filter
4. JWT and token-based authentication
	General token-related knowledge, reusable across architectures
	├─ 4.1 JWT structure and claims	
	├─ 4.2 JWT signing and signature verification	
	├─ 4.3 Access tokens and refresh tokens	
	├─ 4.4 Token expiration and revocation	
	└─ 4.5 Secure token storage and transmission
5. Authorization
	Controlling access to application resources
	├─ 5.1 Request-level authorization	
	├─ 5.2 Method-level authorization	
	├─ 5.3 Role-based access control (RBAC)	
	├─ 5.4 Permission-based access control	
	└─ 5.5 Resource ownership and access control
6. Security configuration and web security
	├─ 6.1 CSRF protection	
	├─ 6.2 CORS configuration	
	├─ 6.3 Session management and stateless applications	
	├─ 6.4 Security headers	
	└─ 6.5 Exception handling and authentication entry points
7. Production security considerations
	├─ 7.1 Password security	
	├─ 7.2 Brute-force protection and rate limiting	
	├─ 7.3 Account locking and disabling	
	├─ 7.4 Secret and signing-key management	
	└─ 7.5 Security testing
