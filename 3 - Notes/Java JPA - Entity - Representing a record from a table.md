Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
`@Entity` tells JPA that a Java class represents a database entity (record):
```java
@Entity
@Table(name = "tasks")
public class Task {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, length = 200)
    private String title;

    @Enumerated(EnumType.STRING)
    @Column(nullable = false, length = 30)
    private TaskStatus status;

    @ManyToOne(fetch = FetchType.LAZY, optional = false)
    @JoinColumn(name = "user_id", nullable = false)
    private AppUser user;

    protected Task() {}

    public Task(String title, TaskStatus status, AppUser user) {
        this.title = title;
        this.status = status;
        this.user = user;
    }

    public Long getId() { return id; }
    public String getTitle() { return title; }
    public TaskStatus getStatus() { return status; }
    public AppUser getUser() { return user; }

    public void changeStatus(TaskStatus status) {
        this.status = status;
    }
}
```

In other words, Hibernate (our JPA implementation) will map this class to a database table.

`@Table(name = "tasks")` specifies the table name.

Our database will have a table called `tasks`.
# Constructors
JPA requires an entity to have a no-argument constructor with at least protected visibility:
```java
protected Task() {}
```

Hibernate uses it when creating entity instances from database records.

Writing:
```java
public Task(String title, TaskStatus status, AppUser user) {
    this.title = title;
    this.status = status;
    this.user = user;
}
```

allows us to create a new entities ourselves:
```java
Task task = new Task(
    request.title().trim(),
    TaskStatus.todo,
    user
);
```
# Related notes
1. [[Java JPA - Entity - Primary key]]
2. [[Java JPA - Entity - Specifying columns]]
3. [[Java JPA - Entity - `@Enumerated`]]
4. [[Java JPA - Entity - Relationships (`@JoinColumn`)]]