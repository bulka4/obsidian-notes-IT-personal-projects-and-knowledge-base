Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
For a parent class:
```java
public class User {
    String name;
    int age;

    public void introduce() {
        System.out.println("Hi, my name is " + name);
    }
}
```

we create a child class like this:
```java
public class Admin extends User {
    public void deleteUser() {
        System.out.println("User deleted");
    }
}
```

A child class contains all the methods and attributes of a parent class.

We say that this child class is an extension (we extend) of a parent class.
# Overriding inherited methods
A child class can provide its own implementation of a method inherited from its parent.

This is called method overriding.

For example:
```java
public class User {
    public void introduce() {
        System.out.println("I am a user");
    }
}
```

```java
public class Admin extends User {

    @Override
    public void introduce() {
        System.out.println("I am an admin");
    }
}
```

Now:
```java
User user = new User();
user.introduce(); // I am a user

Admin admin = new Admin();
admin.introduce(); // I am an admin
```

The `@Override` annotation tells the compiler that you intend to override a method inherited from a parent class. It also helps catch mistakes.
# Constructors and inheritance
Constructors are not inherited. When you create a child object, the parent constructor is also executed.

Example:
```java
public class User {
    String name;

    public User(String name) {
        this.name = name;
    }
}
```

```java
public class Admin extends User {

    public Admin(String name) {
        super(name);
    }
}
```

Here, `super(name)` calls the parent class constructor.
# Access modifiers and inheritance
How access modifiers matter ([[Java - Modifiers|link]]) for inheritance:

|Modifier|Accessible in child class?|
|---|---|
|`public`|Yes|
|`protected`|Yes|
|package-private (no modifier)|Yes, if in the same package|
|`private`|No, not directly|
