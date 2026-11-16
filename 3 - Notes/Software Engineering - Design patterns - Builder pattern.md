Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
The Builder Pattern is a creational design pattern used to construct objects step by step, by calling multiple methods one by one that sets up object's attributes instead of calling a constructor method once that sets up all the parameters.

For example, without the building pattern, with constructor, we set up attributes like this:
```java
public class User {
    private String username;
    private String password;
    private String email;
    private String role;
    private boolean active;

    public User(
        String username,
        String password,
        String email,
        String role,
        boolean active
    ) {
        this.username = username;
        this.password = password;
        this.email = email;
        this.role = role;
        this.active = active;
    }
}

User user = new User(
    "john",
    "password123",
    "john@example.com",
    "USER",
    true
);
```

with the builder pattern:
```java
public class User {
    private String username;
    private String password;
    private String email;
    private String role;
    private boolean active;

    private User(Builder builder) {
        this.username = builder.username;
        this.password = builder.password;
        this.email = builder.email;
        this.role = builder.role;
        this.active = builder.active;
    }

    public static class Builder {
        private String username;
        private String password;
        private String email;
        private String role;
        private boolean active;

        public Builder username(String username) {
            this.username = username;
            return this;
        }

        public Builder password(String password) {
            this.password = password;
            return this;
        }

        public Builder email(String email) {
            this.email = email;
            return this;
        }

        public Builder role(String role) {
            this.role = role;
            return this;
        }

        public Builder active(boolean active) {
            this.active = active;
            return this;
        }

        public User build() {
            return new User(this);
        }
    }
}
```

Now we can construct the object like this:
```java
User user = new User.Builder()
    .username("john")
    .password("password123")
    .email("john@example.com")
    .role("USER")
    .active(true)
    .build();
```
# Constructor disadvantages
There are some disadvantages of using a constructor:
- You need to remember the order of parameters.
- Constructors become difficult to read when there are many parameters.
- Optional parameters can make constructors cumbersome.
- You may need multiple constructors for different combinations of parameters.
# When should you use it?
Use the Builder Pattern when:
- An object has many constructor parameters.
- Many parameters are optional.
- You want readable object creation.
- You want to validate configuration before creating an object.
- You want the resulting object to be immutable.