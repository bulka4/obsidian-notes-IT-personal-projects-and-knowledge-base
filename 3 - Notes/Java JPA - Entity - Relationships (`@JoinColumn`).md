Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
We can define relationships between tables (foreign keys) like this:
```java
@ManyToOne(fetch = FetchType.LAZY, optional = false)
@JoinColumn(name = "user_id", nullable = false)
private AppUser user;
```
- `@JoinColumn(name = "user_id")` specifies the foreign key column in the table where we define this column.
- `fetch = FetchType.LAZY` means Hibernate doesn't automatically retrieve the associated user whenever it loads a task. It retrieves the user when that relationship is accessed (assuming the persistence context is still available).
- `AppUser` specifies related entity (another table which the `user_id` column refers to)
	- By default, specified column refers to the primary key of the related entity