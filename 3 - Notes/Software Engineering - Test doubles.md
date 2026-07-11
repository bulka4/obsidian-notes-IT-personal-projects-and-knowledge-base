Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Test doubles are objects used in tests to replace real dependencies (database, API, message broker, filesystem, etc.).

Types of test doubles:

| Type      | Purpose                           | Example                                        |
| --------- | --------------------------------- | ---------------------------------------------- |
| **Dummy** | Just passed around, never used    | Unused `User` object                           |
| **Stub**  | Returns predefined values         | `getUser()` always returns `"Alice"`           |
| **Fake**  | Simplified working implementation | In-memory database                             |
| **Mock**  | Verifies interactions             | Check that `sendEmail()` was called once       |
| **Spy**   | Records what happened             | Remember all method calls for later assertions |
