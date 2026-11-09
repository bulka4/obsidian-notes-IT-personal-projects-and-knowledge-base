Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
In Java, variable scope determines where a variable can be accessed in your code.
# Local variable (method scope)
Variables declared inside a method are accessible only within that method, from their declaration until the end of the enclosing block.

```java
public void calculate() {
    int x = 10;

    System.out.println(x); // OK
}

public void print() {
    System.out.println(x); // ERROR: x doesn't exist here
}
```
# Block scope
Variables declared inside a block `{}` are accessible only within that block.
```java
public void calculate() {
    if (true) {
        int x = 10;
        System.out.println(x); // OK
    }

    System.out.println(x); // ERROR
}
```

This also applies to loops.
# Instance variables (object scope)
Variables declared inside a class but outside methods belong to individual objects.
```java
public class User {
    String name;          // package-private
    private int age;      // private
    public String email;  // public

    public void setName(String name) {
        this.name = name;
    }

    public void printName() {
        System.out.println(name);
    }
}
```

Each object has its own copy:
```java
User user1 = new User();
User user2 = new User();

user1.setName("John");
user2.setName("Alice");
```

Here:
- `user1.name` is `"John"`.
- `user2.name` is `"Alice"`.

Instance variables exist as long as their objects remain reachable (subject to garbage collection).

We can use different access modifiers (like for methods - [[Java - Methods|link]]) when declaring an instance variable, to define from where it can be accessed:
- `public` – accessible from anywhere (subject to module visibility).
- `protected` – accessible within the same package and by subclasses in other packages.
- `private` – accessible only within the declaring class.
- No modifier (package-private) – accessible only within the same package.
# Static variables (class scope)
Variables declared with `static` belong to the class rather than individual objects.
```java
public class User {
    static int userCount = 0;

    public User() {
        userCount++;
    }
}
```

Usage:
```java
User user1 = new User();
User user2 = new User();

System.out.println(User.userCount); // 2
```

There is one shared static variable for the class, rather than a separate copy for every object.