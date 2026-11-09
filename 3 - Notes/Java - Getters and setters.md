Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Getters and setters are methods used to access and modify an object's private fields.

They are commonly used to implement encapsulation: keeping fields private and controlling how other classes interact with them by using public methods.

For example:
```java
public class User {
    private String name;

    public String getName() {
        return name;
    }
    
    public String setName(name) {
        this.name = name;
    }
}
```

now we can access and change the `name` attribute only through methods:
```java
User user = new User();
user.setName("Alex")
String name = user.getName(); // returns Alex

// this gives error - we can't access this attribute directly because it is private
String name = user.name 
```
# Why not make fields public?
Getters and setters allow you to control access and validate values.

For example:
```java
public void setAge(int age) {
    if (age >= 0) {
        this.age = age;
    }
}
```
