Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
A marker interface is an interface without any methods.

Its purpose is to indicate that a class has some particular characteristic or should receive special treatment from the Java runtime or a framework.

Example:
```java
interface MyMarker {
}

class MyClass implements MyMarker {
}
```

The class doesn't have to implement anything.

Java has some built-in marker interfaces:
- `Serializable` – indicates that objects can participate in Java serialization.    
- `Cloneable` – indicates that an object supports cloning through `Object.clone()`.    

For example:
```java
class User implements Serializable {
    String username;
}
```

The interface itself doesn't provide the serialization implementation. It acts as a marker recognized by Java's serialization mechanism.