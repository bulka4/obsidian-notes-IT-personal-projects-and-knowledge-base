Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
In Java, we can use annotations with method parameters or class attributes (especially records ([[Java - Record class|link]])):
```java
public void greet(@SomeAnnotation String name)

public record CreateTaskRequest(
    @NotBlank @Size(max = 200) String title
) {}
```

Annotation:
- provides instructions for how to prepare or validate the `name` / `title` parameter. 
- It can run a defined method to prepare the parameter and then the `greet` method will be executed with this parameter.
- Or it can run a defined method to validate the parameter and throw an exception if the parameter is incorrect