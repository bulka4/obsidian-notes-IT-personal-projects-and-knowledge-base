Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Defining to use our JWT filter
To use our own JWT filter ([[Java Spring Security - `SecurityFilterChain` - Filters|link]]), we define in the `SecurityFilterChain`:
```java
.addFilterBefore(
	jwtFilter, 
	UsernamePasswordAuthenticationFilter.class
)
```

here:
- The first argument is the filter that we want to use
- The second argument is a reference filter - used to define when to execute the first filter. The filter from the first argument will be executed before this one.

As a reference filter, we can use any filter from a defined filter ordering registry, i.e. from the `FilterOrderRegistration` class defined here - [link](https://github.com/spring-projects/spring-security/blob/main/config/src/main/java/org/springframework/security/config/annotation/web/builders/FilterOrderRegistration.java?utm_source=chatgpt.com). This registry defines orders of filters. The filter that we use as a reference, doesn't have to be used in our app, it just needs to be defined in this ordering registry.
# How JWT filter works
Our JWT filter looks like this:
```java
@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {
    private final JwtService jwtService;

    public JwtAuthenticationFilter(JwtService jwtService) {
        this.jwtService = jwtService;
    }

    @Override
    protected void doFilterInternal(
		HttpServletRequest request,
		HttpServletResponse response,
		FilterChain filterChain
    ) throws ServletException, IOException {
        String header = request.getHeader("Authorization");

        if (header != null && header.startsWith("Bearer ")) {
            String token = header.substring(7);
            try {
                Claims claims = jwtService.parseClaims(token);
                String email = claims.getSubject();
                Long userId = claims.get("userId", Number.class).longValue();

                var authentication = new UsernamePasswordAuthenticationToken(
					new AuthenticatedUser(userId, email),
					null,
					AuthorityUtils.NO_AUTHORITIES
                );
                
                SecurityContextHolder.getContext()
	                .setAuthentication(authentication);
            } catch (Exception exception) {
                SecurityContextHolder.clearContext();
                response.sendError(HttpServletResponse.SC_UNAUTHORIZED, "Invalid or expired token");
                return;
            }
        }

        filterChain.doFilter(request, response);
    }
}
```

In short, what it does is:
- Extract the token from the request
- Extract claims from the token
- create an `authentication` object representing an authenticated user using `UsernamePasswordAuthenticationToken`
- Store created `authentication` object in the Security Context using `SecurityContextHolder.getContext().setAuthentication`

Here's how each part of this code works:
## Extracting the token from the request
```java
String header = request.getHeader("Authorization");

if (header != null && header.startsWith("Bearer ")) {
    String token = header.substring(7);
}
```

Clients usually send JWTs using the following HTTP header:
```
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9...
```

`Bearer` is an authentication scheme indicating that the client possesses a token granting access.

`substring(7)` removes the `"Bearer "` prefix.
## Check if a JWT token was provided
This part:
```java
if (header != null && header.startsWith("Bearer "))
```
checks whether a JWT token was provided in the request.
### No token provided
When registering or logging in, there will be no token provided, so we just go to the next filter by executing `filterChain.doFilter(request, response);`
## Parse the provided token
When token is provided, we extract its claim and validate it ([[Java Spring Security - Parsing and validating a JWT token|link]]) using `JwtService` class ([[Java Spring Security - Authentication with JWT and a custom filter - `JwtService`|link]]):
```java
Claims claims = jwtService.parseClaims(token);
```

this code:
- Checks token validity, including expiration
- extracts token's claims (data stored in the token's payload)
## Create `UsernamePasswordAuthenticationToken` object
Now using this code:
```java
var authentication = new UsernamePasswordAuthenticationToken(
	new AuthenticatedUser(userId, email),
	null,
	AuthorityUtils.NO_AUTHORITIES
);
```

we create an object of the `UsernamePasswordAuthenticationToken` class ([[Java Spring Security - `UsernamePasswordAuthenticationToken` class|link]]) which represents an authenticated user given by the principal `AuthenticatedUser(userId, email)`.
## Save in the Security Context info about the user
Using this code ([[Java Spring Security - SecurityContextHolder|link]]):
```java
SecurityContextHolder.getContext().setAuthentication(authentication);
```

we save the principal `AuthenticatedUser(userId, email)` of the `authentication` object in the Security Context. This makes the principal (user's data) available to the rest of the code, e.g. to REST controller routes ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]) through `@AuthenticationPrincipal` ([[Java Spring Security - `@AuthenticationPrincipal`|link]]).
## Handling invalid tokens
```java
catch (Exception exception) {
    SecurityContextHolder.clearContext();

    response.sendError(
        HttpServletResponse.SC_UNAUTHORIZED,
        "Invalid or expired token"
    );

    return;
}
```

If parsing or validation fails:
- Clear the security context.    
- Return HTTP 401 Unauthorized.    
- Stop processing the request.    

If the request does not contain a Bearer token, the filter continues the chain without setting authentication.

The subsequent security configuration determines whether that request is allowed.
## Continue executing the remaining filters
This code - `filterChain.doFilter(request, response);` specifies to continue executing the remaining filters defined in the security filter chain (`SecurityFilterChain` ([[Java Spring Security - Defining security rules (`SecurityFilterChain`)|link]])).
# Related notes
1. [[Java Spring Security - `OncePerRequestFilter`]]