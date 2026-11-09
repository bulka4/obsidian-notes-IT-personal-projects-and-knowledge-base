Tags: [[__Software_Engineering]]
#SoftwareEngineering 

# Introduction
A race condition occurs when multiple concurrent operations access and modify shared data, and the final result depends on the timing or order in which those operations execute. This can refer to operations within a single application or to multiple applications.
# Examples
## Banking app
```
Initial balance = $100

Thread A: withdraw $80
Thread B: withdraw $50
```

Both threads read:
```
balance = $100
```

Then:
```
Thread A calculates: 100 - 80 = 20
Thread B calculates: 100 - 50 = 50
```

If Thread B writes last:
```
Final balance = $50
```

The system incorrectly allowed withdrawing $130 from a $100 account.
## Lost update
Two clients read the same data and update it independently. One update overwrites the other, so the other update is lost.

Example: Two users edit the same task / document.

Solutions:
- Optimistic concurrency control (version numbers) ([[Software Engineering - Concurrency patterns - Optimistic Concurrency Control (OCC)|link]]).
- Pessimistic locking (lock the record while modifying it).
## Double spending / duplicate processing
Two requests attempt to perform an operation that should happen only once.

Example: A user clicks the "Pay" button twice, or two requests arrive because the frontend retries after a timeout.

Both requests might charge the user.

Solutions:
- Idempotency keys.
- Database unique constraints.
- Atomic database operations.

An idempotency key is a unique identifier associated with an operation. If the same request is received again with the same key, the backend returns the previous result instead of performing the operation again.
## Race condition when checking and inserting
Imagine a user registering with an email address.

Two registration requests arrive simultaneously:
1. Request A checks whether the email exists. It doesn't.
2. Request B checks whether the email exists. It doesn't.
3. Request A inserts the user.
4. Request B also tries to insert the user.

Without proper protection, you might end up with duplicate accounts.

Solutions:
- Database UNIQUE constraint on email.
- Handle unique-constraint violations in the backend.
- Don't rely exclusively on checking before inserting.
## Out-of-order operations
Requests from the same client can finish in a different order from the order in which they were sent.

Example:
1. User changes task status to in_progress. Request A is sent.
2. User quickly changes it to done. Request B is sent.
3. Request B finishes first and saves done.
4. Request A finishes later and saves in_progress.

The final status is incorrect from the user's perspective.

Solutions:
- Version numbers / optimistic concurrency control.
- Request sequencing or cancellation of outdated requests.
- Serialize operations when ordering matters.

This can happen even with a single user and a single frontend.
## Duplicate background job execution
Imagine you have a background worker processing orders.

Two workers accidentally pick up the same order and both process it.

Example: Both workers send a confirmation email or generate the same invoice.

Solutions:
- Atomic job claiming.
- Distributed locks.
- Idempotent job processing.
- Database constraints to prevent duplicate results.
# How to prevent race conditions
Common techniques:
- **Locks / mutexes** → allow only one thread to access critical sections
- **Atomic operations** → operations that happen as one indivisible step
- **Immutable data** → avoid modifying shared state
- **Message passing** → avoid shared memory between components