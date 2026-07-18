Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Transaction testing verifies that a group of operations behaves as a single atomic operation ([[Software Engineering - Transactions|link]]).

It tests properties like:
- Commit → all changes are saved when successful
- Rollback → all changes are undone when something fails
- Isolation → concurrent operations do not corrupt data