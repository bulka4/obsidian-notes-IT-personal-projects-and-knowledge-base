Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
During registration & login:
- Client sends email and password to `POST /api/auth/register`
- `SecurityFilterChain` ([[Java Spring Security - Authentication with JWT and a custom filter - `SecurityFilterChain`|link]]) and Custom JWT filter (the `JwtAuthenticationFilter` class) ([[Java Spring Security - Authentication with JWT and a custom filter - JWT filter|link]]) are applied just like in case of routes that require authentication but:
	- the filter checks whether a token is provided (using `header != null && header.startsWith("Bearer ")`)
	- the token is not provided, so the filter doesn't do anything, just goes to the next filter using `filterChain.doFilter(request, response);`
- Registration or Login route from the `AuthController` REST controller class ([[Java Spring MVC - Rest Controllers - Mapping HTTP requests to Java methods (`@GetMapping`)|link]]) is executed
# Controller class
Registration and login routes are defined within the `AuthController` REST controller class ([[Java Spring MVC - Rest Controllers - Rest Controller (`@RestController`)|link]]):
```java
@RestController
@RequestMapping("/api/auth")
public class AuthController {
    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;
    private final AuthenticationManager authenticationManager;
    private final JwtService jwtService;

    public AuthController(
        UserRepository userRepository,
        PasswordEncoder passwordEncoder,
        AuthenticationManager authenticationManager,
        JwtService jwtService
    ) {
        this.userRepository = userRepository;
        this.passwordEncoder = passwordEncoder;
        this.authenticationManager = authenticationManager;
        this.jwtService = jwtService;
    }

    @PostMapping("/register")
    @ResponseStatus(HttpStatus.CREATED)
    public AuthDtos.AuthResponse register(
	    @Valid @RequestBody AuthDtos.RegisterRequest request
	) {
        String email = normalizeEmail(request.email());

        if (userRepository.existsByEmail(email)) {
            throw new ResponseStatusException(
	            HttpStatus.CONFLICT, 
	            "Email is already registered"
			);
        }

        AppUser user = userRepository.save(
            new AppUser(email, passwordEncoder.encode(request.password()))
        );

        return authResponse(user);
    }

    @PostMapping("/login")
    public AuthDtos.AuthResponse login(
	    @Valid @RequestBody AuthDtos.LoginRequest request
	) {
        String email = normalizeEmail(request.email());

        Authentication authentication = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(email, request.password())
        );

        AppUser user = userRepository
            .findByEmail(authentication.getName())
            .orElseThrow(() -> new ResponseStatusException(
	            HttpStatus.UNAUTHORIZED
			));

        return authResponse(user);
    }

    private AuthDtos.AuthResponse authResponse(AppUser user) {
        return new AuthDtos.AuthResponse(
            jwtService.generateToken(user.getId(), user.getEmail()),
            "Bearer",
            user.getEmail()
        );
    }

    private String normalizeEmail(String email) {
        return email.trim().toLowerCase();
    }
}
```
## Attributes (dependency injection)
The attributes that we use in the controller:
```java
private final UserRepository userRepository;
private final PasswordEncoder passwordEncoder;
private final AuthenticationManager authenticationManager;
private final JwtService jwtService;
```

they are all registered as beans ([[Java Spring - Bean|link]]) so Spring will automatically create and provide those objects here ([[Java Spring - Dependency injection|link]]). We don't need to manually do it like:
```java
userRepository = new UserRepository()
...
controller = new AuthController(userRepository, ...)
```

- The `PasswordEncoder` and `AuthenticationManager` classes are defined in the `SecurityConfig` - [[Java Spring Security - Authentication with JWT and a custom filter - `SecurityConfig`|link]] 
- The `JwtService` class is defined here - [[Java Spring Security - Authentication with JWT and a custom filter - `JwtService`|link]] 
- The `UserRepository` class is defined here - [[Java Spring Security - Authentication with JWT and a custom filter - `UserRepository`|link]]  
# Registration route
Registration route:
```java
public AuthDtos.AuthResponse register(
	@Valid @RequestBody AuthDtos.RegisterRequest request
) {
	String email = normalizeEmail(request.email());

	if (userRepository.existsByEmail(email)) {
		throw new ResponseStatusException(
			HttpStatus.CONFLICT, 
			"Email is already registered"
		);
	}

	AppUser user = userRepository.save(
		new AppUser(email, passwordEncoder.encode(request.password()))
	);

	return authResponse(user);
}
```

- Normalizes the email from the request using `normalizeEmail`
- Uses `userRepository` to find out whether there is already a user with the provided email
- Uses `userRepository` to save in the database data of the new user
	- Password is encoded using `passwordEncoder`
- Returns a response containing user's email and a new token generated using `authResponse`
# Login route
Login route:
```java
public AuthDtos.AuthResponse login(
	@Valid @RequestBody AuthDtos.LoginRequest request
) {
	String email = normalizeEmail(request.email());

	Authentication authentication = authenticationManager.authenticate(
		new UsernamePasswordAuthenticationToken(email, request.password())
	);

	AppUser user = userRepository
		.findByEmail(authentication.getName())
		.orElseThrow(() -> new ResponseStatusException(
			HttpStatus.UNAUTHORIZED
		));

	return authResponse(user);
}
```

- Normalizes the email from the request using `normalizeEmail`
- Authenticates the user using `authenticationManager.authenticate`
- Retrieves user data from the database using `userRepository`
- Returns a response containing user's email and a new token generated using `authResponse`
## Authentication using `authenticationManager.authenticate`
We use the `AuthenticationManager` ([[Java Spring Security - Logging in using `AuthenticationManager` and `UsernamePasswordAuthenticationToken`|link]]) to authenticate the user using provided credentials.

We use the `UsernamePasswordAuthenticationToken` class ([[Java Spring Security - `UsernamePasswordAuthenticationToken` class|link]]) to create an object (unauthenticated object of the `Authentication` class) which represents authentication request containing credentials:
```java
Authentication authentication = new UsernamePasswordAuthenticationToken(
    email,
    request.password()
);
```

and pass it to an object of the `AuthenticationManager` interface ([[Java Spring Security - `AuthenticationManager` interface|link]]) so that Spring Security attempts to authenticate the user using supplied email and password:
```java
Authentication authentication =
    authenticationManager.authenticate(
        new UsernamePasswordAuthenticationToken(
            email,
            request.password()
        )
    );
```

If authentication succeeds, then the `Authentication authentication` object represents an authenticated user.

Conceptually, the process is:
1. `AuthenticationManager` receives the authentication request.
2. An appropriate authentication provider (`AuthenticationProvider`) processes it.
	1. It is used internally inside `authenticationManager.authenticate`
3. The provider calls `UserDetailsService.loadUserByUsername()` ([[Java Spring Security - Authentication with JWT and a custom filter - `UserDetailsService`|link]])
4. It retrieves the user's password hash.
5. It uses `PasswordEncoder.matches()` to verify the password (defined in the `SecurityConfig` ([[Java Spring Security - Authentication with JWT and a custom filter - `SecurityConfig`|link]]).
6. If valid, it returns an authenticated Authentication object.
7. If invalid, authentication fails, normally with an `AuthenticationException`.

Important: `AuthenticationManager` is an abstraction. It does not necessarily perform all these operations itself. An `AuthenticationProvider` handles the actual authentication mechanism.