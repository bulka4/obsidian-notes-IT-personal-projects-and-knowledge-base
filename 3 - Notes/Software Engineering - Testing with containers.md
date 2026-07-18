Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Testing with containers means using containers (usually Docker) to create isolated, reproducible environments for tests.

Instead of depending on software installed on a developer's machine, tests start the required services inside containers.

For example, it can contain a database to test an integration with it.
# Benefits
This method gives us:
- Reproducibility - Every developer and CI pipeline gets the same environment
- Isolation - Tests do not affect your local machine or other tests.
- Easy setup of dependencies - We can start services needed for testing, e.g. databases, message brokers, caches, external APIs
# Testcontainers
A popular approach is using libraries like Testcontainers.

They allow tests to programmatically start containers, for example:
```java
@Test
void testDatabase() {
    PostgreSQLContainer db = new PostgreSQLContainer();

    db.start();

    // run test using this database
}
```
# Use cases
This is mostly used for integration and E2E tests.