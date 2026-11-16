Tags: [[_Java]] [[__Programming_languages]] [[_Java_Spring]]
#Java #ProgrammingLanguages #JavaSpring 

# Introduction
`@Transactional` is a Spring annotation that tells Spring to execute a method within a database transaction.

It is part of Spring's Transaction Management functionality. It is closely related to Spring Core because Spring uses its IoC container and proxies to implement it.

A transaction is a group of operations that should be treated as one (either all operations completes or none takes effect).
# How does `@Transactional` work?
Imagine you have a service:
```java
@Service
public class TransferService {
    @Transactional
    public void transfer(Long fromId, Long toId, BigDecimal amount) {
        accountRepository.subtractBalance(fromId, amount);

        accountRepository.addBalance(toId, amount);
    }
}
```

When another Spring bean calls `transfer()`, Spring manages the transaction around the method.

Conceptually, Spring does something like this:
```java
public void transfer(Long fromId, Long toId, BigDecimal amount) {
    beginTransaction();

    try {
        accountRepository.subtractBalance(fromId, amount);
        accountRepository.addBalance(toId, amount);

        commitTransaction();
    } catch (Exception e) {
        rollbackTransaction();
        throw e;
    }
}
```

This is conceptual code, not what Spring literally generates.
# How does Spring implement this?
This is where Spring proxies come into play.

You might remember that Spring manages beans in its IoC container.

When a bean has a method annotated with `@Transactional`, Spring can create a proxy around that bean.

Instead of other beans calling the original object directly, they call the proxy.

For example:
```java
transferService.transfer(fromId, toId, amount);
```

The actual call flow is approximately:
1. Your controller calls the `TransferService` proxy.    
2. The proxy detects that `transfer()` is annotated with `@Transactional`.    
3. It starts a transaction (or joins an existing one).    
4. It invokes the actual `transfer()` method.    
5. If the method completes successfully, it commits.    
6. If an applicable exception is thrown, it rolls back.    

The proxy handles all this without you having to write transaction-management code yourself.
# When does Spring roll back a transaction?
By default, Spring rolls back when the method throws:
- `RuntimeException` or one of its subclasses.    
- `Error` or one of its subclasses.    

It does not automatically roll back for checked exceptions (such as `IOException`).

You can customize this:
```java
@Transactional(rollbackFor = Exception.class)
public void transfer() throws Exception {
    // Database operations
}
```

Now Spring will also roll back for checked exceptions covered by that rule.
# Important properties of `@Transactional`
There are a few additional concepts worth knowing.

|Property|Meaning|
|---|---|
|`propagation`|Determines what happens when a transactional method calls another transactional method|
|`isolation`|Controls how transactions interact with concurrent transactions|
|`readOnly`|Marks a transaction as read-only; can allow optimizations|
|`timeout`|Sets a transaction timeout|
|`rollbackFor`|Specifies exceptions that trigger rollback|
|`noRollbackFor`|Specifies exceptions that should not trigger rollback|

For example:
```java
@Transactional(readOnly = true)
public List<Task> getTasks() {
    return taskRepository.findAll();
}
```

This indicates that the transaction is intended for reading rather than modifying data. It is generally useful for read-only service operations, although it doesn't universally prevent writes.
# Important limitations
There are a few things to remember:

1. Self-invocation
If a method in a bean calls another `@Transactional` method in the same bean, the call normally bypasses the proxy.
```java
public void methodA() {
    methodB(); // Direct call, bypasses proxy
}

@Transactional
public void methodB() {
    // ...
}
```

The annotation on `methodB()` will not independently trigger transaction handling in this situation.

2. Transactions don't automatically cover everything.
For example, a database transaction cannot automatically roll back an email that has already been sent or an HTTP request made to another service.

3. Transactions need transaction infrastructure.
Spring needs an appropriate transaction manager, such as `JpaTransactionManager` for JPA or `DataSourceTransactionManager` for JDBC. Spring Boot often configures this automatically when the relevant dependencies are present.
# What operations can be included?
With a typical Spring application using JPA and `@Transactional`, you can include operations such as:

|Operation|Covered by database transaction?|
|---|---|
|Insert a database record|Yes|
|Update a database record|Yes|
|Delete a database record|Yes|
|Read database records|Yes|
|Execute SQL queries|Yes|
|Modify multiple database tables|Yes|
|Call another Java method|Not inherently; only its database operations may participate|
|Calculate something in Java|No transactional effect|
|Send an HTTP request|No|
|Send an email|No|
|Write a file|No|
|Publish a message to a queue|Not automatically|
## What if we include unsupported operation
If we include unsupported operation in a transaction, the code will be executed but effects will not be rolled back.