Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
A constructor has:
- The same name as the class.
- No return type (not even `void`).
- A body containing initialization logic.

```java
public class User {

    String name;
    int age;

    // Constructor
    public User() {
        name = "Unknown";
        age = 0;
    }
}
```

You call it when creating an object:
```java
User user = new User();
```
# Constructor with parameters
You can pass arguments to a constructor:
```java
public class User {

    String name;
    int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

Usage:
```java
User user = new User("John", 25);
```

Here:
- `name` and `age` inside the constructor are parameters (local variables).
- `this.name` and `this.age` refer to the object's instance fields.
- `this` refers to the current object being initialized.
# Multiple constructors (overloading)
A class can have multiple constructors with different parameter lists.
```java
public class User {

    String name;
    int age;

    public User() {
        this.name = "Unknown";
        this.age = 0;
    }

    public User(String name) {
        this.name = name;
        this.age = 0;
    }

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

Now you can create objects in different ways:
```java
User user1 = new User();
User user2 = new User("John");
User user3 = new User("Alice", 30);
```
# Default constructor
If you don't define any constructor, Java automatically provides a no-argument constructor:
```java
public class User {
    String name;
}
```

You can then write:
```java
User user = new User();
```

If you define at least one constructor yourself, Java no longer generates the default constructor automatically.