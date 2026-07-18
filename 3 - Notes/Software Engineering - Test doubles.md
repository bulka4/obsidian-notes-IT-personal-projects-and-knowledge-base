Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Test doubles are objects used in tests to replace real dependencies (database, API, message broker, filesystem, etc.).

Those objects can be for example:
- Class instance
- Function
- Variable / value
- module / package

Types of test doubles:

| Type      | Purpose                           | Example                                                                                                                |
| --------- | --------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Dummy** | Just passed around, never used    | Unused `User` object                                                                                                   |
| **Stub**  | Returns predefined values         | `getUser()` always returns `"Alice"`                                                                                   |
| **Fake**  | Simplified working implementation | In-memory database                                                                                                     |
| **Mock**  | Verifies interactions             | It can be e.g. a function that can record how it was used, e.g. how many times it was called, what arguments were used |
| **Spy**   | Records what happened             | Remember all method calls for later assertions                                                                         |
