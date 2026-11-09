Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
For example, instead of manually creating a repository inside a service:
```java
public class TaskService {
    private TaskRepository repository = new TaskRepository();
}
```

Spring can automatically provide the repository:
```java
@Service
public class TaskService {

    private final TaskRepository repository;

    public TaskService(TaskRepository repository) {
        this.repository = repository;
    }
}
```

Spring manages the objects (called beans) and injects their dependencies.