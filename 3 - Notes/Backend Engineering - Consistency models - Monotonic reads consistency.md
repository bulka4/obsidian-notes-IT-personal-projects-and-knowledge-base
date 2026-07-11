Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In a monotonic reads consistency model ([[Backend Engineering - Distributed microservices - Consistency models|link]]), once a service or user has observed a particular state, all subsequent reads are guaranteed to return the same state or a newer one. 

It will never observe an older version of the data. It prevents time going “backwards” for a user.