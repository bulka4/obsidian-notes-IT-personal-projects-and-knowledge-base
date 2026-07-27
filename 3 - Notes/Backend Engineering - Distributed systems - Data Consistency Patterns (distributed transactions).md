Tags: [[_Backend_Engineering]]
#BackendEngineering 

# Introduction
Data Consistency Patterns (also called distributed transactions) are patterns that maintain consistency across distributed services without a single database transaction.

They make sure that we don't end up in a situation where some services completed their task while others failed.

Those patterns include:
1. Saga pattern - [[Software Engineering - Architecture patterns - Saga|link]] 
2. 2PC - [[Backend Engineering - Data Consistency Patterns - 2PC|link]] 
3. TCC - [[Backend Engineering - Data Consistency Patterns - TCC|link]] 
4. For event-driven systems:
	1. Outbox pattern - [[Backend Engineering - Data Consistency Patterns - Outbox pattern|link]] 