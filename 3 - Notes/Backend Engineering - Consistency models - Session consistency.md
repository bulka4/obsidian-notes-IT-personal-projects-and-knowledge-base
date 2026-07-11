Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In a session consistency model ([[Backend Engineering - Distributed microservices - Consistency models|link]]), a service or user is guaranteed a consistent view of data within a single session. 

That means, that a service or a user always sees their own updates and never observes older data than they have already seen within a session.

Typically, this includes read-your-writes and monotonic reads.