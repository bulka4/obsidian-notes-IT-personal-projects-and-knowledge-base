Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
The `@Enumerated` option is used with Java enum ([[Java - enum|link]]):
```java
@Enumerated(EnumType.STRING)
@Column(nullable = false, length = 30)
private TaskStatus status;
```

`@Enumerated(EnumType.STRING)` tells JPA to store the enum's name as a string in the database.