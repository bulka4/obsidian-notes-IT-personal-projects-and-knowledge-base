Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring_Data]]
#Java #ProgrammingLanguages #JavaSpringData 

# Introduction
Query Method Derivation is a method that allows us to create methods inside an interface and Spring Data will automatically implement their logic based on keywords that appear in this method's name, so we don't need to implement this logic on our own.

For example:
```java
public interface TaskRepository extends JpaRepository<Task, Long> {
    List<Task> findAllByUserIdOrderByIdAsc(Long userId);
    Optional<Task> findByIdAndUserId(Long id, Long userId);
}
```

Spring Data looks for keywords like `find`, `ById`, `OrderBy` and based on that generates for example a SQL query that will be executed.