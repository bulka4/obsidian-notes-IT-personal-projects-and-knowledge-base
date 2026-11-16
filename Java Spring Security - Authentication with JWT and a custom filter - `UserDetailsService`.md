Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]] [[_Java_Spring_Security]]
#Java #ProgrammingLanguages #JavaSpring #JavaSpeingSecurity 

# Introduction
We prepare an implementation of the `UserDetailsService` interface ([[Java Spring Security - `UserDetailsService` - Loading user data|link]]) that will be used by the `AuthenticationManager.authenticate()` method to load user data from a database:
```java
@Service
public class CustomUserDetailsService implements UserDetailsService {
    private final UserRepository userRepository;

    public CustomUserDetailsService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    @Override
    public UserDetails loadUserByUsername(String email) throws UsernameNotFoundException {
        var user = userRepository.findByEmail(email)
            .orElseThrow(() -> new UsernameNotFoundException("User not found"));

        return User.withUsername(user.getEmail())
            .password(user.getPasswordHash())
            .authorities("USER")
            .build();
    }
}
```
