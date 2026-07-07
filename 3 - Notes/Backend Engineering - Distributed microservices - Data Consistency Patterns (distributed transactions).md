Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Data Consistency Patterns (also called distributed transactions) are patterns that maintain consistency across distributed services without a single database transaction.

They make sure that we don't end up in a situation where some services completed their task while others failed.

Those patterns include:
1. Saga pattern - [[Backend Engineering - Distributed microservices - Saga pattern|link]] 
2. 2PC - [[Backend Engineering - Distributed microservices - 2PC|link]] 
3. TCC - [[Backend Engineering - Distributed microservices - TCC|link]] 