Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```
- `@Id` identifies the primary key.
- `@GeneratedValue` tells JPA that the ID should be generated automatically.
- `GenerationType.IDENTITY` delegates ID generation to the database, typically using an identity/auto-increment column.