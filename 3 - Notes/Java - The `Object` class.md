Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
The `Object` class is the root superclass of almost all classes in Java.

This means that if you create your own class, it ultimately inherits from `Object`, even if you don't explicitly write `extends Object`.

For example, when we write:
```java
public class User {
    String name;
}
```

this is equivalent to:
```java
public class User extends Object {
    String name;
}
```
# Important methods inherited from Object
| Method        | Purpose                                               |
| ------------- | ----------------------------------------------------- |
| `toString()`  | Returns a string representation of an object          |
| `equals()`    | Checks whether two objects are considered equal       |
| `hashCode()`  | Returns a hash code used by hash-based collections    |
| `getClass()`  | Returns the runtime class of an object                |
| `clone()`     | Creates a copy of an object (subject to restrictions) |
| `wait()`      | Makes a thread wait on an object's monitor            |
| `notify()`    | Wakes one thread waiting on that object's monitor     |
| `notifyAll()` | Wakes all threads waiting on that object's monitor    |