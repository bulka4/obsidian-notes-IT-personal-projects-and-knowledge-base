Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring_Data]]
#Java #ProgrammingLanguages #JavaSpringData 

# Introduction
```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```
- `@Id` identifies the primary key.
- `@GeneratedValue` tells JPA that the ID should be generated automatically.
- `GenerationType.IDENTITY` delegates ID generation to the database, typically using an identity/auto-increment column.