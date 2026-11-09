Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
`@Column` configures how the Java field maps to a database column:
```java
@Column(nullable = false, length = 200)
private String title;
```
- `nullable = false`: the column cannot contain SQL `NULL`.
- `length = 200`: specifies a maximum column length of 200 characters.