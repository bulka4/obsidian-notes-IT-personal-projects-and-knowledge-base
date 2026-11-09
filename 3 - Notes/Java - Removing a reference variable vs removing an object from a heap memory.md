Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
When we create an object:
```java
public void createUser() {
    User user = new User();
}
```

then once the `createUser` method finishes, the `user` reference variable ([[Java - Data types - Primitive and Reference variables|link]]) is deleted from the stack memory ([[Java - Heap and stack memory|link]]) but the `User` object it references can be still in the heap memory.

When an object (e.g. `User`) has no remaining references, it becomes eligible for garbage collection ([[Java - Memory garbage collector|link]]).