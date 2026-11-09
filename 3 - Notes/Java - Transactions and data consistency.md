Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Enterprise applications often involve complex business operations.

Imagine transferring money between two bank accounts:
1. Subtract money from account A.
2. Add money to account B.
3. Record the transaction.

All three operations should succeed together, or none should happen.

Java's Spring ecosystem has mature transaction management through @Transactional.
```java
@Transactional
public void transferMoney(
    Long sourceId,
    Long destinationId,
    BigDecimal amount
) {
    // Subtract from source account
    // Add to destination account
    // Record transaction
}
```


If an exception causes the transaction to roll back, the database changes can be reverted together.

Python also supports database transactions, so this isn't an exclusive Java capability. However, Spring makes this functionality particularly convenient to integrate into large applications.