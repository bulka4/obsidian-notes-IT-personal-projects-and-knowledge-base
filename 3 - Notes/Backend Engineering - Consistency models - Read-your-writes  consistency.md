Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
In a read-your-writes consistency model ([[Backend Engineering - Distributed systems - Consistency models|link]]), after a service or user makes a write (changes state), its subsequent reads are guaranteed to return the updated state, even if other services or users still see an older version.

It is:
- Common in user sessions
- Improves user experience